# Azure Pipelines 보안

## 환영합니다

이 실습은 [Snyk](https://snyk.io/)을 사용하여 [Microsoft Azure](https://azure.microsoft.com/en-us/) Workload를 보호하기 위한 샘플 패턴 및 참조 아키텍처를 제공하는 **Securing AKS** 및 **Securing ACR** 모듈을 기반으로 합니다. 이제 이러한 학습을 확장하고 [Azure Repos](https://azure.microsoft.com/en-us/services/devops/repos/)에서 소스 코드 스캔을 다룹니다. Microsoft Azure Repos는 [Microsoft Azure DevOps Services](https://azure.microsoft.com/en-us/solutions/devops/)의 일부입니다. 지원 인프라 배포, 샘플 응용 프로그램 및 Microsoft Azure에 대한 다양한 Snyk Integration 구성을 안내하는 단계별 예제와 샘플 코드를 제공합니다.

## 전제 조건

이 실습의 연습을 완료하려면 [Microsoft Azure DevOps](https://azure.microsoft.com/en-us/services/devops/), [Microsoft Azure](https://azure.microsoft.com/) 및 [Snyk](https://snyk.io/) 계정이 필요합니다. 이 모듈의 콘텐츠는 이전 실습의 연속으로 사용하거나 Snyk을 Azure Pipelines와 통합하는 방법에 대한 독립 실행형 예제로 사용할 수 있습니다.

* [무료 Microsoft Azure 계정](https://azure.microsoft.com/en-us/free)을 만드십시오.
* [무료 Snyk 계정](https://snyk.io/login)을 만드십시오.
* **선택 사항:** **Securing AKS**를 완료하거나 작동하는 AKS 클러스터를 실행합니다.
* **선택 사항:** **Securing ACR**를 완료하거나 이미지를 포함하는 ACR 레지스트리를 보유하십시오.
* **선택 사항:** **Securing Azure Repos**를 완료하거나 기존 저장소가 있습니다.
* [무료 Microsoft Azure DevOps 계정](https://azure.microsoft.com/en-us/services/devops/)을 만듭니다.
