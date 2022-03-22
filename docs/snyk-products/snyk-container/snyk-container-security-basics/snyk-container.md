# Snyk Container 통합

Snyk Container는 프로젝트를 Snyk으로 가져오기 위한 다양한 통합을 제공합니다. 이러한 통합은 사용자와 고객을 위한 다양한 워크플로우를 지원합니다.

![](../../../.gitbook/assets/projects.png)

사용하는 통합은 요구 사항 및 워크플로우에 따라 다릅니다. 하나의 통합으로 시작하여 나중에 다른 통합으로 이동하거나 팀이 성장함에 따라 통합을 조합하여 사용할 수 있습니다.

예를 들어 이미지를 빌드할 때 CI 통합을 사용하여 개발 팀에 빠른 피드백을 제공한 다음 Kubernetes 통합을 사용하여 운영 환경에서 실행 중인 이미지에 대한 보안을 보장하는 것이 일반적입니다.

### 사용 가능한 통합

주요 통합은 다음과 같습니다.

* **CLI**: 로컬에서 스캔 또는 빌드한 이미지 테스트에 유용합니다. [컨테이너 보안을 위한 Snyk CLI](../snyk-cli-for-container-security/)를 참조하십시오.
* SCM: Snyk은 Git 저장소에서 직접 Dockerfile을 탐지하고 기본 이미지를 덜 취약한 이미지로 업데이트하기 위한 권장 사항을 제공할 수 있습니다. [Dockerfile 스캔](../scan-your-dockerfile/)을 참조하십시오.
* CI: 게이트 역할을 할 수 있습니다.(예: 심각도가 높은 새로운 취약점에 대한 빌드를 실패시키는 것)
* Container registries: 많은 이미지를 테스트하거나 CI 파이프라인을 수정할 수 없는 경우에 유용합니다.
* [Kubernetes](https://support.snyk.io/hc/en-us/articles/360003916138-Kubernetes-integration-overview): 컨테이너 레지스트리와 유사하지만 Snyk이 취약점 또는 그룹 프로젝트의 우선순위를 지정하는 데 사용할 수 있는 실행 워크로드에 대한 컨텍스트가 더 많습니다.

보다 자세한 사항은 [이미지 스캔 information library](../image-scanning-library/)를 참조하십시오.
