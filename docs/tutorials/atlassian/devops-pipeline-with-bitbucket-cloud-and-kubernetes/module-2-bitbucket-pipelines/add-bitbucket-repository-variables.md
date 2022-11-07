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
* AWS Identity & Access Management User [key and secret](https://docs.aws.amazon.com/IAM/latest/UserGuide/id\_credentials\_access-keys.html) for secure authenticated interactions with the AWS API: `AWS_ACCESS_KEY_ID` & `AWS_SECRET_ACCESS_KEY`
  * These are secured variables.
  * These are the API keys for your access into AWS.
* AWS region you will be deploying to: `AWS_DEFAULT_REGION`
  * This is not a secured variable.
  * This is a region to where your ECR registry is accessible from. For example - us-east-1.
* Amazon ECR [URL](https://docs.aws.amazon.com/AmazonECR/latest/userguide/Registries.html) for your repository: `AWS_ECR_URI`
  * This is not a secured variable.
  * This is the private ECR URI for your repository of this form: [https://aws\_account\_id.dkr.ecr.region.amazonaws.com](https://aws\_account\_id.dkr.ecr.region.amazonaws.com)
* Container image name: `IMAGE`
  * This is not a secured variable.
  * This is the name of your image, such as java-goof.
* Amazon EKS name of your cluster: `AWS_EKS_CLUSTER`
  * This value is not a secured variable.
  * This is the name of your EKS cluster.
  * This workshop does not cover the EKS cluster, but you may set this value if you continue with the example and add a deployment to a cluster.

변수를 구성했으면 이제 파이프라인을 검토하고 다음 섹션에서 실행을 트리거할 수 있습니다.
