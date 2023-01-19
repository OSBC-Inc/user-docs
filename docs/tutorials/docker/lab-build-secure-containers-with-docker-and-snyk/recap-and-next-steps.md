# 요약 및 다음 단계

## 축하합니다!

이 실습의 끝에 도달했습니다. 대단한 여정이었습니다! 실습을 진행하면서 Snyk와 Docker가 함께 소프트웨어 제공 관행을 위한 안전한 지속적 통합 및 지속적 제공 패러다임을 촉진하는 데 어떻게 도움이 되는지 확인하셨기를 바랍니다.‌

이 실습이 마음에 드셨기를 바랍니다. 아래에서 귀하가 달성한 내용을 요약하고 Snyk에서 더 많은 가치를 얻는 데 도움이 되는 추가 리소스를 제공합니다.‌

## Snyk Container <a href="#snyk-container" id="snyk-container"></a>

Snyk Container를 사용하여 선택한 기본 이미지로 인해 발생한 문제를 찾았습니다. Dockerfile을 Snyk으로 가져오고 애플리케이션에 대해 덜 취약한 기본 이미지를 선택했습니다.

컨테이너로 작업하는 경우 다음과 같은 몇 가지 리소스를 확인해 볼 가치가 있습니다:

### Container Registry와 Integration

Snyk은 Container Registry와 통합하여 Snyk으로 스캔할 컨테이너 이미지를 쉽게 가져올 수 있습니다. Docker Hub, [ocker Hub](https://support.snyk.io/hc/en-us/articles/360003916058-Configure-integration-for-Docker-Hub), [Azure Container Registry](https://support.snyk.io/hc/en-us/articles/360003915958-Configure-integration-for-ACR), [Google Container Registry](https://support.snyk.io/hc/en-us/articles/360003916118-Configure-integration-for-GCR), [Artifactory Container Registry](https://support.snyk.io/hc/en-us/articles/360003915998-Configuring-your-JFrog-Artifactory-container-registry-integration) 및 [AWS Elastic Container Registry](https://support.snyk.io/hc/en-us/articles/360003916078-Configure-integration-for-Amazon-Elastic-Container-Registry-ECR-)를 지원합니다.

### Kubernetes Integration

Snyk Container의 확장인 Kubernetes Monitor는 실행 중인 워크로드에서 컨테이너 취약성을 식별할 수 있습니다. 자세한 내용은 [Snyk Kubernetes Integration Overview](https://support.snyk.io/hc/en-us/articles/360003916138-Kubernetes-integration-overview)를 확인하십시오.

## Snyk Open Source <a href="#snyk-open-source" id="snyk-open-source"></a>

Snyk Open Source를 사용하여 샘플 애플리케이션의 Open Source구성 요소에서 취약점을 찾았습니다. GitHub Integration을 구성하고 Fix Pull Requests을 생성하고 릴리스 프로세스에 게이트를 구축하여 문제가 Production branch로 전달되지 않도록 했습니다.‌

우리가 다루지 않은 몇 가지 사항:

### Automatic Dependency Upgrade Pull Requests <a href="#automatic-dependency-upgrade-pull-requests" id="automatic-dependency-upgrade-pull-requests"></a>

종속성을 업그레이드하기 위해 취약점이 게시될 때까지 기다려야 하는 이유는 무엇입니까? Snyk은 [사용자를 대신하여 Pull Requests를 자동으로 열도록](https://support.snyk.io/hc/en-us/articles/360006581898-Upgrading-dependencies-with-automatic-PRs) 구성하여 종속성을 최신 상태로 정상 상태로 유지할 수 있습니다.‌

### 수정된 GitHub Account을 사용하여 Snyk Pull Requests 열기

Snyk을 사용하면 수정 및 업그레이드 PR이 열리는 [특정 GitHub 계정을 구성](https://support.snyk.io/hc/en-us/articles/360010843797-Opening-fix-and-upgrade-pull-requests-from-a-fixed-GitHub-account-)할 수 있습니다. 우리의 연구에 따르면 Fix PR이 Merge될 가능성이 높아집니다. 확인해보세요!

## Snyk Infrastructure as Code

Snyk Infrastructure as Code를 사용하여 Kubernetes 배포 매니페스트에서 구성 Issue를찾아 수정했습니다. 다음은 Snyk IaC에 대해 다루지 않은 몇 가지 사항입니다.

### IaC Rule Severity 구성

Infrastructure as Code 규칙은 획일적인 것이 아닙니다. 워크로드마다 보안 요구 사항과 허용 오차가 다르기 때문에 Snyk IaC가 애플리케이션 구성에 점수를 매기는 방법을 변경할 수 있습니다. 문서에서 [IaC 규칙의 심각도 점수를 조정](https://support.snyk.io/hc/en-us/articles/360006402818#UUID-c1919782-6bfa-b84b-a638-3913cee39fc5)하는 방법을 알아보세요.

### 테라포밍 지원

이 실습에서는 다루지 않았지만 Snyk은 구성 문제에 대해 Terraform 파일을 스캔할 수도 있습니다. Terraform 지원에 대해 자세히 알아보려면 [Terraform 파일에서 Issue를 스캔하고 수정](https://support.snyk.io/hc/en-us/articles/360010916577-Scan-and-fix-security-issues-in-your-Terraform-files)하는 방법을 확인하세요.
