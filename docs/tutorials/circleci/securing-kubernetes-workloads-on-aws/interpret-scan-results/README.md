# 스캔 결과 해석

[`Projects`](https://solutions.snyk.io/snyk-academy/open-source/import-scm-project) 페이지에는 추가된 모든 프로젝트의 인벤토리와 결과에 대한 높은 수준의 요약이 포함됩니다. 특정 프로젝트를 확장하여 발견된 취약점에 대한 세부 정보와 이를 수정하는 방법에 대한 지침을 볼 수 있습니다. 예제에서는 **세 가지** 통합을 구성하려고 합니다.

1. [GitHub](https://support.snyk.io/hc/en-us/articles/360004032117-GitHub-integration)를 통한 소스 코드 관리
2. [Amazon ECR(Elastic Container Registry)](https://support.snyk.io/hc/en-us/articles/360003947077-Amazon-Elastic-Container-Registry-ECR-add-images-to-Snyk)을 사용한 컨테이너 레지스트리
3. [Kubernetes](https://support.snyk.io/hc/en-us/articles/360003947117-Adding-Kubernetes-workloads-for-security-scanning)의 클라우드 네이티브 애플리케이션

## Source Code Management

Git 저장소를 스캔하면 애플리케이션 오픈 소스 종속성에서 잠재적인 취약점이 발견됩니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/circleci\_source\_scan.png)

## Container Registry

개인 레지스트리에서 컨테이너 이미지를 스캔하면 기본 이미지를 분석하고 알려진 취약성을 줄이기 위한 업그레이드 권장 사항을 제공합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/circleci\_ecr\_scan.png)

## Kubernetes

Kubernetes 통합을 활성화하면 배포에서 잘못된 보안 구성을 수정하는 데 대한 통찰력과 지침이 제공됩니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/circleci\_eks\_scan.png)
