# 파이프라인 내에서 IaC custom rules 통합

Custom rule을 관리, 배포 및 적용하는 데 이상적인 시나리오는 [GitHub Actions](https://github.com/features/actions)와 같은 CI/CD를 사용하는 경우입니다.

### 개요

이 예시는 보안 팀이 수행하는 과정입니다.

* Rules를 Github 저장소에 저장합니다.
* Github Action을 사용하여 파이프라인에 서로 다른 development-time steps를 추가합니다.
* Custom rules를 사용하여 변경 사항을 차단하는 Github Action 파이프라인을 실행하도록 다른 Github 저장소를 구성합니다.

이 예에서는 [snyk/custom-rules-example](https://github.com/snyk/custom-rules-example) 저장소를 사용합니다. 이 저장소에는 SDK를 시작하는 동안 작성된 모든 Custom rules가 포함되어있습니다.

#### 목표

파이프라인을 다음과 같이 구성하려고 합니다.

* 새로운 Rule이나 기존 Rule의 변경 사항이 기존 기능을 손상시키지 않는지 확인합니다.
* Rule은 OCI 레지스트리의 `main`에 게시합니다.
* 다른 파이프라인에서 Custom rules를 사용합니다.
* (선택 사항)환경 변수를 사용하여 Custom rules를 구성합니다.

### Github Action을 사용하여 PR check 추가

PR check의 예시는 [https://github.com/snyk/custom-rules-example/pull/5](https://github.com/snyk/custom-rules-example/pull/5)에서 `my_rule`이라는 새로운 Rule을 추가하는 것을 확인할 수 있습니다.

(**note**: [Rule 작성](getting-started-with-the-sdk/writing-a-rule.md) 시 공개된 Rule과 동일합니다)

이 Rule이 예상대로 작동하는지 확인하기 위해 단위 테스트를 시행했습니다. PR check의 일부로 단위 테스트를 실행하기 위해 이전에 `test.yml`이라고 하는 `.github/workflows`에서 GitHub Action을 구성했습니다.

{% code title=".github/workflows/test.yml" %}
```
name: Test Custom Rules

on:
  push:
    branches:
      - '**'        # matches every branch
      - '!main'     # excludes main

jobs:
  unit_test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2

      - uses: actions/setup-node@v1
        with:
          node-version: 15

      - name: Install snyk-iac-rules
        run: npm i -g snyk-iac-rules

      - name: Run unit tests
        run: snyk-iac-rules test
```
{% endcode %}

이 워크플로우에 대한 몇 가지 주의 사항은 다음과 같습니다.

* PR이 열려 있을 때 실행되도록 `main`이 아닌 모든 branch에서 실행되도록 구성했습니다.
* Node.js 환경을 설정하는 단계를 추가하여 [npm](install-the-sdk.md#install-the-sdk-with-npm)을 사용하여 `snyk-iac-rules` SDK를 설치할 수 있도록 하였습니다.
* `snyk-iac-rules test`를 실행하기 위한 단계를 추가했는데, 테스트 중 하나라도 실패하면 PR 검사가 실패합니다.

{% hint style="info" %}
설정에서 **main branch**를 구성해야 합니다. -> 먼저 branch를 설정하여 아무도 **main branch**에 직접 push할 수 없도록 합니다.
{% endhint %}

### Snyk IaC GitHub Action

Rule을 테스트하는 또 다른 방법은 [Snyk IaC Github Action](https://github.com/snyk/actions/tree/master/iac)을 사용하여 [Snyk CLI](../../../features/snyk-cli/)에서 테스트하여 생성된 bundle을 CLI에서 읽을 수 있는지 확인하는 것입니다.

이를 실행하려면 Snyk CLI 및 `SNYK_TOKEN` 설치 단계가 필요하며, 이 단계는 Snyk 계정 설정에서 확인할 수 있습니다.

{% code title=".github/workflows/test.yml" %}
```
jobs:
  contract_test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2

      - uses: actions/setup-node@v1
        with:
          node-version: 15

      - name: Install snyk-iac-rules
        run: npm i -g snyk-iac-rules

      - name: Build bundle
        run: snyk-iac-rules build .

      - name: Run contract with Snyk to check Infrastructure as Code files for issues
        continue-on-error: true
        uses: snyk/actions/iac@master
        env:
          SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}
        with:
          args: --rules=bundle.tar.gz
```
{% endcode %}

[Shellspec](https://github.com/shellspec/shellspec)을 사용하도록 이러한 테스트를 확장하고 원하는 취약점이 나타나는지 확인할 수 있지만 단위 테스트를 사용하는 것이 좋습니다.

### Custom rules 게시

PR이 이전 섹션에서 검사를 통과하고 `main` branch로 병합하면 OCI 레지스트리에서 Rule을 게시할 수 있습니다. 이를 통해 별도의 파이프라인을 구성하고, Custom rules bundle을 다운로드하고 Custom rules를 실행하여 잘못된 구성을 탐지할 수 있습니다.

이를 위해 `publish.yml`이라는 다른 워크플로우를 `.github/workflows`에 추가합니다.

{% code title=".github/workflows/publish.yml" %}
```
name: Publish Custom Rules

on:
  push:
    branches:
      - 'main'

jobs:
  publish:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2

      - uses: actions/setup-node@v1
        with:
          node-version: 15

      - name: Install snyk-iac-rules
        run: npm i -g snyk-iac-rules
        
      - name: Build bundle
        run: snyk-iac-rules build .
        
      - name: Login to Docker Hub
        uses: docker/login-action@v1
        with:
          username: ${{ secrets.OCI_REGISTRY_USERNAME }}
          password: ${{ secrets.OCI_REGISTRY_PASSWORD }}

      - name: Publish rules
        run: snyk-iac-rules push --registry $OCI_REGISTRY_URL bundle.tar.gz
        env:
          OCI_REGISTRY_URL: "${{ secrets.OCI_REGISTRY_NAME }}:v1"
```
{% endcode %}

이전 워크플로우와 비슷해 보이지만 이 워크플로우에 대해 몇 가지 유의할 사항이 있습니다.

* PR이 병합할 때 실행되도록 main branch에서만 실행하도록 구성했습니다.
* 선택한 OCI 레지스트리인 Docker Hub 인증 단계를 추가했습니다. 지원하는 레지스트리 목록을 확인하려면 [pushing a bundle](getting-started-with-the-sdk/pushing-a-bundle.md)을 참조하세요. [docker/login-action](https://github.com/docker/login-action) GitHub Action을 사용하여 이를 수행하고 `Settings` -> `Secrets`에서 Github 암호를 구성해야 합니다.
* 생성한 Custom rules bundle을 OCI 레지스트리에 게시하는 `snyk-iac-rules build`에 이어 `snyk-iac-rules push`를 실행하는 단계를 추가했습니다.

#### 버전 지정 규칙

모든 CI/CD 파이프라인에 영향을 미치지 않고 Custom rules의 실험 버전을 릴리스하려면 태그 지정을 사용하여 bundle을 버전화할 수 있습니다.

따라서 대부분의 서비스에서 `v1`을 사용하면서 bundle `v2-beta`를 평가판으로 사용할 수 있습니다.

{% code title=".github/workflows/publish.yml" %}
```
      - name: Publish experimental rules
        run: snyk-iac-rules push --registry $OCI_REGISTRY_URL bundle.tar.gz
        env:
          OCI_REGISTRY_URL: "${{ secrets.OCI_REGISTRY_NAME }}:v1"
      - name: Publish rules
        run: snyk-iac-rules push --registry $OCI_REGISTRY_URL bundle.tar.gz
        env:
          OCI_REGISTRY_URL: "${{ secrets.OCI_REGISTRY_NAME }}:v2-beta"
```
{% endcode %}

{% hint style="info" %}
이 워크플로우를 사용하려면 GitHub Secrets에 구성된 OCI\_REGISTRY\_NAME에 태그 또는 프로토콜이 이미 포함되어 있는지 확인하십시오.
{% endhint %}

### Custom rules 적용

Custom rules를 OCI 레지스트리에 게시한 후 이러한 규칙을 사용하도록 별도의 파이프라인을 구성할 수 있습니다. 이를 위해 [public Group IaC Settings API](https://snykv3.docs.apiary.io/#reference/group-settings/infrastructure-as-code/update-infrastructure-as-code-settings)를 사용합니다.

구성한 Custom rules bundle을 사용하도록 Snyk을 업데이트하는 다른 작업으로 위의 Github Action을 구성합니다.

```
      - name: Update Snyk
        run: |
          curl --location --request PATCH 'https://api.snyk.io/v3/groups/<group id>/settings/iac/?version=2021-11-03~beta' \
          --header 'Content-Type: application/vnd.api+json' \
          --header 'Authorization: token ${{ secrets.SNYK_TOKEN }}' \
          --data-raw '{
            "data": {
                  "type": "iac_settings",
                  "attributes": {
                    "custom_rules": {
                      "oci_registry_url": "registry-1.${{ secrets.OCI_REGISTRY_NAME }}",
                      "oci_registry_tag": "v1",
                      "is_enabled": true
                    }
                }
            }
          }'
```

이 API 호출은 구성한 Custom rules bundle을 사용하도록 선택한 Snyk 그룹과 아래의 모든 조직을 업데이트합니다.

{% hint style="info" %}
현재 `v2-beta`와 같은 다른 bundle을 사용하도록 조직을 구성할 경우 Snyk Settings 페이지를 사용하도록 제한합니다. CI/CD 파이프라인에서 환경 변수를 사용하여 Custom rules를 실행할 수 있도록 새로운 bundle을 구성하거나 Custom rules를 사용하지 않도록 설정할 수 있습니다.
{% endhint %}

다른 저장소에서 그룹 아래 조직 중 하나를 인증하고 Snyk IaC Github Action을 워크플로우에 추가합니다.

```
name: Snyk Infrastructure as Code Custom Rules

on:
  push:

jobs:
  snyk-iac-security:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2

      - name: Run Snyk to check Infrastructure as Code files for issues
        continue-on-error: false
        uses: snyk/actions/iac@master
        env:
          SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}
```

그 결과 생성한 잘못된 구성이 해결될 때까지 Github Action이 실패합니다.

```
Testing example.tf...


Infrastructure as code issues:
  ✗ IAM Role missing one of the required tags: owner, description or type [Medium Severity] [CUSTOM-RULE-8]
    introduced by input > resource > aws_iam_role[new_role] > tags

  ✗ Vendor or Service must have either owneralternate or ticketgroup or both tags. [Medium Severity] [CUSTOM-RULE-9]
    introduced by input > resource > aws_iam_role[new_role] > tags
```

### Custom rules 구성

또한 API 또는 Snyk Settings 페이지를 사용하는것이 너무 제한적일 경우 환경 변수를 사용하여 Custom rules를 구성할 수 있는 방법도 제공합니다.

Snyk IaC Github Action은 `SNYK_CFG_OCI_REGISTRY_URL`, `SNYK_CFG_OCI_REGISTRY_USERNAME`, `SNYK_CFG_OCI_REGISTRY_PASSWORD` 환경 변수와 함께 사용할 수 있습니다.

Github Action은 이러한 환경 변수를 읽고 이전 단계에서 push된 bundle을 구성된 OCI 레지스트리로 풀다운합니다. Github Action은 다음과 비슷하게 표시합니다.

```
name: Snyk Infrastructure as Code Custom Rules

on:
  push:

jobs:
  snyk-iac-security:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2

      - name: Run Snyk to check Infrastructure as Code files for issues
        continue-on-error: false
        uses: snyk/actions/iac@master
        env:
          SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}
          SNYK_CFG_OCI_REGISTRY_URL: ${{ secrets.OCI_REGISTRY_URL }}
          SNYK_CFG_OCI_REGISTRY_USERNAME: ${{ secrets.OCI_REGISTRY_USERNAME }}
          SNYK_CFG_OCI_REGISTRY_PASSWORD: ${{ secrets.OCI_REGISTRY_PASSWORD }}
```
