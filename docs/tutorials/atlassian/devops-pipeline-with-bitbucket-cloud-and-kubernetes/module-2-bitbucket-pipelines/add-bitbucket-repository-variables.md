---
description: Tailor your workshop with details specific to you
---

# Bitbucket 저장소 변수 추가

이 섹션에서는 인스턴스에 대한 워크샵을 사용자 정의하기 위해 변수를 추가합니다. 아래에 변수 이름과 보안 변수 여부를 나열하고 그 용도를 설명합니다.

### 저장소 변수 추가

Bitbucket에서 파이프라인을 활성화하면 매개변수화된 작업을 허용하기 위해 [저장소 변수](../../../getting-started/atlassian-integrations/atlassian-bitbucket-pipeline-variables.md)를 추가해야 합니다.

저장소에 변수를 추가하려면 권한이 필요합니다.

파이프라인 정의를 검토할 때 코드를 스캔하고 AWS 서비스에 결과를 게시하기 위한 변수 참조가 표시되며 다음은 필요한 저장소 변수입니다.

* Snyk 계정 인증을 위한 Snyk API 토큰: `SNYK_TOKEN`. 다음 단계에서 통합을 활성화한 후 이 변수로 다시 돌아올 것입니다.
* 이 값은 보안 변수입니다.
* 생성한 서비스 계정 API 토큰입니다.
* AWS Identity & Access Management AWS API와의 안전한 인증 상호 작용을 위한 사용자 키 및 암호: `AWS_ACCESS_KEY_ID` & `AWS_SECRET_ACCESS_KEY`
  * 이것은 보안 변수입니다.
  * 이는 AWS에 액세스하기 위한 API 키입니다.
* 배포할 AWS 리전: `AWS_DEFAULT_REGION`
  * 이것은 보안 변수가 아닙니다.
  * ECR 레지스트리에 액세스할 수 있는 지역입니다. 예: us-east-1.
* 저장소의 Amazon ECR [URL](https://docs.aws.amazon.com/AmazonECR/latest/userguide/Registries.html): `AWS_ECR_URI`
  * 이것은 보안 변수가 아닙니다.
  * 이것은 이 양식의 저장소에 대한 개인 ECR URI입니다.: [https://aws\_account\_id.dkr.ecr.region.amazonaws.com](https://aws\_account\_id.dkr.ecr.region.amazonaws.com)
* 컨테이너이미지 이름: `IMAGE`
  * 이것은 보안 변수가 아닙니다.
  * 이것은 java-goof와 같은 이미지의 이름입니다.
* 클러스터의 Amazon EKS 이름: `AWS_EKS_CLUSTER`
  * 이것은 보안 변수가 아닙니다.
  * 이것은 EKS 클러스터의 이름입니다.
  * 이 워크숍에서는 EKS 클러스터를 다루지 않지만 예제를 계속 진행하면서 클러스터에 배포를 추가하는 경우 이 값을 설정할 수 있습니다.

변수를 구성했으면 이제 파이프라인을 검토하고 다음 섹션에서 실행을 트리거할 수 있습니다.
