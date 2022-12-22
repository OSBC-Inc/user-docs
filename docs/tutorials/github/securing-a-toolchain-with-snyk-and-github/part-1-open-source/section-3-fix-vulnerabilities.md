---
description: >-
  보안 게이트가 설치되고 위험에 대해 경고하는 경우 개발 Branch에서 문제를 수정하여 수정 사항을 PROD Branch로 다운스트림할 수
  있습니다.
---

# Section 3: 취약점 수정

Section 1에서 구성한 GitHub Integration을 통해 Snyk은 Pull Request를 열어 종속성을 취약하지 않은 버전으로 업그레이드하여 수정을 가속화할 수 있습니다.

## Step 1: 취약점을 더 자세히 탐색

Log into Snyk, and go into the `gh-actions-academy` project imported earlier. Scroll down to see the list of vulnerabilities present, ordered by [our proprietary Priority Score](https://snyk.io/blog/snyk-priority-score/). For each Vulnerability, Snyk displays:

* The module that introduced it and, in the case of transitive dependencies, its direct dependency,
* Details on the path and proposed fixes, as well as the specific vulnerable functions

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-vuln.png)

## Step 2: Create a Fix Pull Request in Snyk

When using the GitHub integration, and if a fix is available, Snyk can automatically upgrade the vulnerable dependency to a non-vulnerable version through a Pull Request. Click on "Fix this vulnerability" to do so.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-fixvuln.png)

On the next screen, you'll be able to confirm the issue to fix with this PR.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-prconfirm.png)

Looks good! Go ahead and open the PR.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-propen.png)

Once it's ready, you'll be taken to the PR in GitHub, where you can review the changes in the file diff view:

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-prdiff.png)

We see that CI checks completed successfully, assuring us we didn't introduce a breaking change.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-prchecks.png)

Now, go ahead and merge the PR! You can also delete the branch. Back in Snyk, we can appreciate that our `package.json` file has 1 less High Severity Vulnerability.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-postpr.png)

## Step 3: Fix the rest of the Vulnerabilities

Let's fast track to a clean `develop` branch with another Pull Request. This time, from the `all-fixes` branch into `develop`.

### How we arrived at a clean branch

The `all-fixes` branch was created by using the [Snyk Wizard](https://support.snyk.io/hc/en-us/articles/360003851357-Manage-vulnerability-results-with-the-Snyk-CLI-wizard) against our `develop` branch. If you'd rather do this yourself, `git clone` the repo to your workstation and run `snyk wizard` against it. We recommend pushing changes into a new branch so you can continue the workshop from there.

### Open a Pull Request!

Create a New Pull Request from `all-fixes` to `develop`. This introduces some changes:

* The creation of a `.snyk` file, which is used to track changes made by `Snyk Wizard`.
* Updated `package.json` and `package-lock.json` files with updated dependencies.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-allfixpr.png)

You can explore these changes in the Comparing Changes view to learn more. When ready, finish creating and Merge the Pull Request.

## Step 4: Re-visit the PR created in Step 2

If you left the Pull Request from Section 2 open, you can re-visit it in the Pull Requests tab.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-postfixes.png)

When the workflows re-run, this time, the Snyk Security gate and CI jobs should complete successfully.

{% hint style="warning" %}
Open Source vulnerabilities are disclosed every day. If the Snyk Gate fails, at least one new High Severity vulnerability has been disclosed since this was written. If this happens, Repeat steps 1 and 2 above to open a Pull Request that fixes the remaining issues.
{% endhint %}

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-postfixchecks.png)

Merge in the changes, and feel good that your `PROD` branch is free from Open Source Vulnerabilities! 🏆

You made it to the end of Part 1! Congratulations! Proceed to Part 2 to see how Snyk Container can help you keep this application secure as you package it in a container.
