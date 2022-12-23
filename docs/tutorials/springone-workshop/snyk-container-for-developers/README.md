# Snyk Containers

## Snyk Containers

Snyk Container는 취약점을 수정하기 위한 개발자 친화적인 접근 방식입니다. Snyk Container는 개발자가 컨테이너 취약성을 해결하는 최선의 방법을 식별할 수 있도록 수정 조언을 제공하여 조직을 지원합니다.

* 기본 이미지 선택 - 컨테이너의 목표는 코드와 해당 종속성만 배송하는 것일 수 있습니다. 그러나 현실은 운영 체제 라이브러리 및 기타 도구가 결국 컨테이너에 저장된다는 것입니다. Snyk 컨테이너는 취약성을 크게 줄일 수 있는 대체 기본 이미지 옵션을 식별합니다.
* 코딩 및 CLI - 코드를 Commit하고 컨테이너 다운스트림을 푸시하기 전에 조기에 자주 스캔하여 Issue를 식별합니다.
* CI/CD 게이팅 - Jenkins, CircleCI 및 Azure Pipelines와 같은 CI/CD 도구와의 통합은 자동화된 Snyk 테스트를 추가하여 취약성이 빌드 프로세스를 통과하지 못하도록 방지합니다.
* 컨테이너 레지스트리 통합 - 저장된 컨테이너 이미지에서 문제를 찾고 Docker Hub, AWS ECR, Azure ACR, Google GCR 및 JFrog Artifactory와 같은 널리 사용되는 컨테이너 레지스트리에서 지속적인 보호를 보장합니다.

### Workshop 연습

다음 단계를 완료합니다:

1. Docker Hub에서 Snyk UI로 컨테이너 이미지를 가져옵니다.
2. 컨테이너 이미지 스캔 결과를 검토하고 Dockerfile 수정 조언을 추가합니다.
