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

### Add the Snyk Gate to the develop branch

We'll create a Pull Request to add `snyk-gate.yml` to the `develop` branch. To open a Pull Request, first navigate to Pull Requests -> New Pull Request.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-newpr.png)

{% hint style="danger" %}
GitHub defaults to the upstream Snyk-Partners repo as the Base Repository as shown in the image below. Be sure to change that to your fork.
{% endhint %}

![Your PR should not look like this!](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-prcompare.png)

In the **Comparing Changes** window, select the `develop` branch from your forked repo as the base repository, and the `oss-actions` as the head repository, then open the PR.

![Ensure your fork is selected as the base repo before opening the PR.](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-oss-pr.png)

You should see that this PR adds the `snyk-gate.yml` file to the `develop` branch.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-oss-pr-1-.png)

After input a name, description, and click **Create Pull Request** you'll be asked to **Merge Pull Request.**

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-mergepr.png)

## Step 3: Test the Security Gate

To test this, open a New Pull Request. This time, set `PROD` as the Base, and `develop` as the Head.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-mainpr.png)

In the Pull Request details, the Snyk Security Gate fails as expected because `develop` still contains the High Severity Vulnerabilities identified earlier.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-snykgateworks.png)

You'll also notice two Snyk checks, `license/snyk` and `security/snyk`. These are making sure no **new** security or license issues are introduced. These **incremental** checks pass because we haven't introduced any risks that weren't already present.

{% hint style="info" %}
Learn more about this functionality by reading [Snyk checks on Pull Requests](https://support.snyk.io/hc/en-us/articles/360006581938-Snyk-checks-on-pull-requests).
{% endhint %}

You now have a Snyk Security Gate! While you can merge at your discretion, Snyk fails this check to alert that there are unresolved, **Fixable,** **High** **Severity** risks. Leave the Pull Request open for now; in the next section, we'll secure our `develop` branch, clear this gate, and secure the PROD-ready version of our code!
