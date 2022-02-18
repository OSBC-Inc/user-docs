# 파이프라인 내에서 IaC custom rules 통합

Custom rule을 관리, 배포 및 적용하는 데 이상적인 시나리오는 [GitHub Actions](https://github.com/features/actions)와 같은 CI/CD를 사용하는 것입니다.

### 개요

이 예시는 보안 팀이 수행하는 과정입니다.

* Rules를 Github 저장소에 저장합니다.
* Github Action을 사용하여 파이프라인에 서로 다른 development-time steps를 추가합니다.
* Custom rules를 사용하여 변경 사항을 차단하는 Github Action 파이프라인을 실행하도록 다른 Github 저장소를 구성합니다.

이 예에서는 [snyk/custom-rules-example](https://github.com/snyk/custom-rules-example) 저장소를 사용합니다. 이 저장소에는 SDK를 시작하는 동안 작성된 모든 Custom rules가 포함되어있습니다.

#### 목표

파이프라인을 다음과 같이 구성하려고 합니다.

* 새로운 Rule이나 기존 Rule의 변경 사항이 기존 기능을 손상시키지 안흔ㄴ지 확인합니다.
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
설정에서 `main` branch를 구성해야 합니다. -> 먼저 branch를 설정하여 아무도 `main`branch에 직접 push할수 없도록 합니다.
{% endhint %}

### Snyk IaC GitHub Action

Another way to test the rules is by testing the contract with the [Snyk CLI](../../../features/snyk-cli/) by using the [Snyk IaC GitHub Action](https://github.com/snyk/actions/tree/master/iac), making sure the generated bundle can be read by the CLI.

To do this, you will need a step for installing the Snyk CLI and a `SNYK_TOKEN`, which can be found in your Snyk Account Settings.

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

You can also expand these tests to use [Shellspec](https://github.com/shellspec/shellspec) and verify that the desired vulnerabilities get triggered, but we recommend using the unit tests for this.

### Publishing the custom rules

Once a PR passes its checks from the previous section and gets merged into the `main` branch, you can publish our rules to an OCI registry. This allows you to configure a separate pipeline, to download the custom rules bundle from this location, and run the custom rules in order to catch misconfigurations.

For this, we will add another workflow under `.github/workflows` called `publish.yml`:

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

It looks similar to the previous workflow, but there are a few things to note about this one:

* We configured it to run only on `main` branches, so that it runs when PRs are merged.
* We added a step to authenticate with Docker Hub, our chosen OCI registry. For a list of supported registries read about [pushing bundles](getting-started-with-the-sdk/pushing-a-bundle.md). Use the [docker/login-action](https://github.com/docker/login-action) GitHub Action to do that and make sure to configure the GitHub secrets under `Settings` -> `Secrets`.
* We added a step to run `snyk-iac-rules build` followed by `snyk-iac-rules push`, which will publish our generated custom rules bundle to an OCI registry.

#### Versioning rules

If we want to release an experimental version of the custom rules without affecting all our CI/CD pipelines, we can use tagging to version our bundles.

So, we can start trialing bundle `v2-beta` while still using `v1` in most of our services:

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
Make sure that the OCI\_REGISTRY\_NAME configured in the GitHub Secrets does not already contain the tag or the protocol if you want to use this workflow.
{% endhint %}

### Enforcing the custom rules

After publishing the custom rules to an OCI registry, you can configure a separate pipeline to use these rules. One way to do this is by using the [public Group IaC Settings API](https://snykv3.docs.apiary.io/#reference/group-settings/infrastructure-as-code/update-infrastructure-as-code-settings).

This means configuring the GitHub Action above with another job for updating Snyk to use the configured custom rules bundle:

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

This API call will update the chosen Snyk group and all the organizations underneath it to use the configured custom rules bundle.

{% hint style="info" %}
For now, if we want to configure an organization to use a different bundle, such as the `v2-beta` one, we are limited to using the Snyk Settings page. There we can either configure a new bundle or disable custom rules so that we can use environment variables in our CI/CD pipeline to run the custom rules.
{% endhint %}

In a different repository, all you have to do is authenticate with one of the organizations underneath this group and add the Snyk IaC GitHub Action to a workflow:

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

The result is that the GitHub action will fail until the generated misconfigurations have been resolved:

```
Testing example.tf...


Infrastructure as code issues:
  ✗ IAM Role missing one of the required tags: owner, description or type [Medium Severity] [CUSTOM-RULE-8]
    introduced by input > resource > aws_iam_role[new_role] > tags

  ✗ Vendor or Service must have either owneralternate or ticketgroup or both tags. [Medium Severity] [CUSTOM-RULE-9]
    introduced by input > resource > aws_iam_role[new_role] > tags
```

### Configuring the custom rules

Additionally, if using an API or the Snyk Settings page seem too restrictive, we also provide a way to configure the custom rules by using the environment variables.

You can use the Snyk IaC GitHub Action with the `SNYK_CFG_OCI_REGISTRY_URL`, `SNYK_CFG_OCI_REGISTRY_USERNAME`, and `SNYK_CFG_OCI_REGISTRY_PASSWORD` environment variables to scan your configuration files for any custom rules which may have been breached.

The GitHub Action reads these environment variables and pulls down the bundle pushed in the previous step to the configured OCI registry. The GitHub action will look similar to this:

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
