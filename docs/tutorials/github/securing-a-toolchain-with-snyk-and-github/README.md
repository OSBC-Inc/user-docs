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

저장소는 다음과 같이 구성됩니다.

* 코드의 배포 준비 상태를 나타내는 PROD Branch입니다.
* 우리가 작업할 기본 Branch인 개발 Branch.
* Part 1 에 사용될 oss-actions Branch..
* Part 2 에 사용될 container-actions Branch.
* Part 3 에 사용될 iac-actions Branch.

### GitHub Actions Workflows

기존 Workflow로 저장소를 포크하면 GitHub는 기본적으로 GitHub Actions를 비활성화합니다. GitHub Actions를 활성화하려면 Actions 탭을 클릭한 다음 "Enable my Workflows"를 클릭합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-actionson.png)

`.github.workflows` 폴더에는 `develop` 및 `PROD` 분기에 대한 CI 워크플로가 포함되어 있습니다. 브레이킹 체인지가 도입되지 않도록 코드가 Branch로 푸시될 때 앱을 다시 빌드하고 테스트합니다. 실습 전체에서 이러한 파일에 추가하여 GitHub Actions로 더 많은 작업을 수행할 것입니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-devworkflows.png)

준비가 되면 Part 1 로 이동하여 시작하십시오!
