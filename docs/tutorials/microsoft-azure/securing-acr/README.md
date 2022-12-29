# ACR 보안

## 환영합니다

이 워크숍은 [Snyk](https://snyk.io/)을 사용하여 [Microsoft AKS](https://azure.microsoft.com/en-us/services/kubernetes-service/)에서 실행되는 [Microsoft Azure](https://azure.microsoft.com/en-us/) Workload를 보호하기 위한 샘플 패턴 및 참조 아키텍처를 제공하는 **Securing AKS** 모듈을 기반으로 합니다. 이제 이러한 학습을 확장하고 [Microsoft Container Registry(ACR)](https://azure.microsoft.com/en-us/services/container-registry/)에서 컨테이너 이미지 스캔을 다룹니다. 지원 인프라 배포, 샘플 응용 프로그램 및 Microsoft Azure에 대한 다양한 Snyk Integration 구성을 안내하는 단계별 예제와 샘플 코드를 제공합니다.

## 전제 조건

이 실습에서 연습을 완료하려면 [Microsoft Azure](https://azure.microsoft.com/) 및 [Snyk](https://snyk.io/) 계정이 모두 필요하고 **Securing AKS** 모듈을 성공적으로 완료해야 합니다.

* [무료 Microsoft Azure 계정](https://azure.microsoft.com/en-us/free)을 만드십시오.
* [무료 Snyk 계정](https://snyk.io/login)을 만드십시오.
* **Securing AKS**를 완료하거나 작동하는 AKS 클러스터를 실행합니다.

## 구조

이 모듈을 마치면 샘플 컨테이너 이미지를 저장하는 ACR의 기능적 인스턴스를 갖게 됩니다. 다음 참조 아키텍처는 빌드할 항목을 나타냅니다:

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-acr.jpg)
