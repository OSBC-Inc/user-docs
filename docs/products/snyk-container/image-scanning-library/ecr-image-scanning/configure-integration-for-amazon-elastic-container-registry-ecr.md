# Amazon Elastic Container Registry (ECR) 통합 구성

하나의 Amazon ECR 레지스트리와 Snyk 조직 간의 통합을 활성화하고 이미지 보안 관리를 시작합니다. 여러 레지스트리와 통합하려면 각 레지스트리에 대해 고유한 조직을 생성합니다.

**프로세스 자동화**

계정간 액세스를 설정하여 Snyk의 Amazon ECR 통합을 원클릭 배포로 활성화할 수 있습니다. 이 옵션은 [AWS Quick Start](https://github.com/aws-quickstart/quickstart-snyk-security)로 제공되며 수동으로 구성할 필요가 없습니다.

![](../../../../.gitbook/assets/quickstart-snyk-security-ecr.png)

통합을 완료하려면 Snyk **Organization ID**와 AWS IAM [role ARN](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference\_identifiers.html#identifiers-arns)이 필요합니다. ARN 역할은 AWS CloudFormation Console의 Output 탭에서 제공합니다.

![](../../../../.gitbook/assets/cloudformation-launch-stack.png)

**수동 프로세스**

통합을 사용하도록 설정하려면 먼저 읽기 전용 AWS IAM(Identity and Access Management)역할을 생성해야합니다 역할은 허용된 Snyk 할당 조직 ID 목록을 지정하여 조직별로 Snyk에대한 레지스트리의 모든 저장소에 대한 읽기 전용 액세스를 위임합니다.

그런 다음 추가 조직을 통합할 때 필요에 따라서 추가 조직 ID를 추가할 수 있습니다.

다음 단계에 따라 통합을 설정하세요.

* [enable-permissions-to-access-amazon-elastic-container-registry-ecr-for-the-first-time.md](enable-permissions-to-access-amazon-elastic-container-registry-ecr-for-the-first-time.md "mention")
* [add-additional-organizations-to-your-aws-iam-role-for-snyk-authentication.md](add-additional-organizations-to-your-aws-iam-role-for-snyk-authentication.md "mention")
* [amazon-elastic-container-registry-ecr-configure-your-integration-with-snyk.md](amazon-elastic-container-registry-ecr-configure-your-integration-with-snyk.md "mention")
