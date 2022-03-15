# Snyk Container 보안 기본 사항

컨테이너는 응용 프로그램을 위한 표준 패키징 형식을 제공하지만 컨테이너 이미지는 불분명할 수 있으므로 포함된 소프트웨어 및 취약점을 식별하는 데 문제가 발생할 수 있습니다.

Snyk Container:

* 이러한 취약점을 신속하게 찾고 해결할 수 있는 도구 및 통합 기능을 제공합니다.
* 처음부터 보안이 내장된 이미지를 만들 수 있습니다.

컨테이너 이미지 스캔에서 취약점에 대해 이미지를 스캔하는 방법에 대해 자세히 알아보십시오.

## Snyk Container 통합

![](../../../.gitbook/assets/projects.png)

컨테이너 이미지 보안 문제를 해결하기 위해 Snyk Container는 프로젝트를 Snyk으로 가져오는 다양한 통합을 제공합니다. 이는 사용자와 고객을 위한 다양한 워크플로우를 지원합니다.

주요 통합은 다음과 같습니다.

* [CLI](https://docs.snyk.io/snyk-container/snyk-cli-for-container-security): 로컬에서 스캔 또는 구축한 이미지 테스트에 유용합니다.
* SCM: Snyk은 Git 저장소에서 직접 Dockerfile을 탐지하고 기본 이미지를 덜 취약한 이미지로 업데이트하기 위한 권장 사항을 제공할 수 있습니다.
* CI: 게이트 역할을 할 수 있습니다.(예: 심각도가 높은 새로운 취약점에 대한 빌드를 깨는 것)
* Container registries: 많은 이미지를 테스트하거나 CI 파이프라인을 수정할 수 없는 경우에 유용합니다.
* [Kubernetes](https://support.snyk.io/hc/en-us/articles/360003916138-Kubernetes-integration-overview): 컨테이너 레지스트리와 유사하지만 Snyk이 취약점 또는 그룹 프로젝트의 우선 순위를 지정하는 데 사용할 수 있는 실행 워크로드에 대한 컨텍스트가 더 많습니다.

사용하는 통합은 요구사항 및 워크플로우에 따라 다릅니다. 하나의 통합으로 시작한 후 나중에 다른 통합으로 이동하거나 팀이 확장됨에 따라 통합을 조합하여 사용할 수 있습니다.

예를 들어 CI 통합을 사용하여 이미지를 작성할 때 개발 팀에 빠른 피드백을 제공하고, Kubernetes 통합을 사용하여 프로덕션에서 실행 중인 이미지에 대한 확신을 제공하는 것이 일반적입니다.

[container security](https://snyk.io/learn/container-security/)를 통해 자세한 내용을 확인할 수 있습니다.
