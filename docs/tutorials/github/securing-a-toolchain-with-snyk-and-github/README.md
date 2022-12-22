# Snyk 및 GitHub로 Toolchain 보안

## 실습 정보

> **난이도**: 중급
>
> **소요 시간:** 60 분

실습은 세 부분으로 구성되어 있으며 순서대로 완료해야 합니다. 각각은 다른 Snyk 제품을 다룹니다.

1. Part 1 에서는 샘플 앱의 오픈 소스 취약성을 수정하는 방법을 다룹니다.
2. Part 2 에서는 파이프라인에 Dockerfile 및 Container Security Scanning을 추가합니다.
3. Part 3 에서는 Deployment YAML 및 Infrastructure as Code Scans를 추가합니다.

### 전제 조건

* GitHub 계정. 필요한 경우 [GitHub에서 무료로 가입](https://github.com/join)하세요.
* Snyk 계정. 필요한 경우 [snyk.io에서 무료로 가입](https://app.snyk.io/login)하세요.

또한 샘플 애플리케이션으로 GitHub Repo를 분기해야 합니다.

{% embed url="https://github.com/snyk-partners/gh-actions-academy" %}

### Branch Structure

The Repo is structured as follows:

* A _PROD_ branch that represents the deploy-ready state of the code.
* A _develop_ branch that is the default branch we'll be working with.
* A _oss-actions_ branch that will be used for Part 1.
* A _container-actions_ branch that will be used for Part 2.
* A _iac-actions_ branch that will be used for Part 3.

### GitHub Actions Workflows

When you fork a Repo with existing workflows, GitHub disables GitHub Actions by default. To enable GitHub Actions, click on the Actions Tab, and then "Enable my Workflows".

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-actionson.png)

The `.github.workflows` folder contains CI workflows for the `develop` and `PROD` branches. These rebuild and test the app when code is pushed to the branch, to ensure no breaking changes are introduced. We'll add onto these files throughout the Lab to do more with GitHub Actions.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-devworkflows.png)

When ready, head on to Part 1 and get started!
