---
description: >-
  Production-ready Branch에 높은 심각도 위험이 더 이상 발생하지 않도록 저장소의 GitHub Actions
  Workflow에 Snyk Security Gate를 추가해 보겠습니다.
---

# Section 2: Stop the Bleeding

이 섹션에서는 [Snyk GitHub Action](https://github.com/snyk/actions)을 사용하는 Security Gate를 소개합니다. Snyk 작업은 GitHub 검사에 실패할 수 있으며 Repo 활동으로 인해 위험이 발생할 때 경고하여 문제를 조기에 발견하는 데 도움이 됩니다.

## Step 1: Snyk Token 생성

Snyk Action을 사용하려면 Snyk API 토큰을 생성하고 GitHub Secret으로 저장해야 합니다.

### Snyk 토큰 검색

다음 두 가지 방법 중 하나로 API 토큰을 찾을 수 있습니다.

* Snyk CLI가 있는 경우 `snyk config get api`를 실행하여 검색합니다.
* [Snyk UI](https://app.snyk.io/account)에서 계정 설정 페이지로 이동하여 검색합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-token.png)

{% hint style="info" %}
Snyk API 토큰을 확인할 수 없습니까? [Snyk API 토큰 취소 및 재생성을 확인하십시오](https://support.snyk.io/hc/en-us/articles/360004008278-Revoking-and-regenerating-Snyk-API-tokens).
{% endhint %}

### GitHub Secrets에 Snyk 토큰 저장

Settings -> Secrets -> New Repository Secret으로 이동하여 Fork된 저장소의 Secret에 토큰을 저장합니다. Secret 이름 `SNYK_TOKEN`

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-secrets.png)

{% hint style="info" %}
Secret을 확인할 수 없습니까? [저장소에 대한 암호화된 Secret 만들기](https://docs.github.com/en/free-pro-team@latest/actions/reference/encrypted-secrets#creating-encrypted-secrets-for-a-repository)를 확인하십시오.
{% endhint %}

Snyk 토큰이 저장되면 Step 2를 계속합니다.

## Step 2: Snyk GitHub Action 추가

Workflow에 Snyk Security Gate를 추가할 시간입니다! 필요한 파일은 `oss-actions` Branch에 이미 생성되어 있습니다.

### Snyk Gate YML 파일 검사

`oss-actions` Branch로 전환하고 `.github/workflows` 폴더로 이동하여 `snyk-gate.yml`을 확인합니다. 다음 사항에 유의하십시오:

* 이는 `PROD`에 도입되는 새로운 취약성의 "stop the bleeding"하도록 설계되었기 때문에 이 Workflow는 `PROD`에 대해 PR이 열린 경우에만 실행됩니다.
* Snyk Action의 `--severity.threshold` 및 `--fail-on` 인수는 Snyk에게 `upgradable`(수정이 가능한) 심각도가 `high`인 위험이 있는 경우에만 실패하도록 지시합니다.

{% hint style="info" %}
[Snyk CLI Reference](https://support.snyk.io/hc/en-us/articles/360003812578-CLI-reference)에서 이러한 명령 및 기타 CLI 명령에 대해 자세히 알아보십시오.
{% endhint %}

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-snykgate.png)

### 개발 Branch에 Snyk Gate 추가

`develop` Branch에 `snyk-gate.yml`을 추가하기 위해 Pull Request를 생성합니다. Pull Request를 열려면 먼저 Pull Requests -> New Pull Request으로 이동합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-newpr.png)

{% hint style="danger" %}
GitHub는 아래 이미지와 같이 기본 저장소로 업스트림 Snyk-Partners 저장소를 기본으로 합니다. Fork로 변경하십시오.
{% endhint %}

![당신의 PR은 이렇게 보여서는 안됩니다!](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-prcompare.png)

**Comparing Changes** 창에서 기본 저장소로 분기된 저장소의 개발 Branch를 선택하고 헤드 저장소로 `oss-actions`를 선택한 다음 PR을 엽니다.

![PR을 열기 전에 Fork가 기본 저장소로 선택되었는지 확인하십시오.](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-oss-pr.png)

이 PR이 `snyk-gate.yml` 파일을 `develop` Branch에 추가하는 것을 볼 수 있습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-oss-pr-1-.png)

이름, 설명을 입력하고 **Create Pull Request**를 클릭하면 **Merge Pull Request**라는 메시지가 표시됩니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-mergepr.png)

## Step 3: Security Gate 테스트

이를 테스트하려면 New Pull Request를 여십시오. 이번에는 `PROD`를 Base로 설정하고 Head로 `develop`합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-mainpr.png)

Pull Request 세부 정보에서 Snyk Security Gate는 예상대로 `develop`에 앞서 식별된 높은 심각도 취약점을 포함하고 있기 때문에 실패합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-snykgateworks.png)

두 개의 Snyk 검사인 `license/snyk` 및 `security/snyk`도 확인할 수 있습니다. 이들은 **새로운** 보안 또는 라이센스 문제가 도입되지 않도록 합니다. 아직 존재하지 않는 위험을 도입하지 않았기 때문에 이러한 **점진적** 검사를 통과합니다.

{% hint style="info" %}
[Pull Request에 대한 Snyk 검사](https://support.snyk.io/hc/en-us/articles/360006581938-Snyk-checks-on-pull-requests)를 읽어 이 기능에 대해 자세히 알아보십시오.
{% endhint %}

이제 Snyk Security Gate가 생겼습니다! 재량에 따라 Merge할 수 있지만 Snyk은 이 확인에 실패하여 해결되지 않고 **수정 가능**하며 **심각도가 높은** 위험이 있음을 경고합니다. 지금은 Pull Request를 열어두세요. 다음 섹션에서는 `develop` branch를 보호하고 이 게이트를 지우고 코드의 PROD 지원 버전을 보호합니다!
