# Snyk Cloud 시작하기: AWS

Snyk Cloud는 [Amazon Web Services (AWS)](https://aws.amazon.com/) 공급자 계정의 인프라 구성을 검색하고 취약성으로 이어질 수 있는 구성 오류를 감지합니다.

다음 방법을 사용하여 AWS 계정을 Snyk에 온보딩할 수 있습니다.

* [Snyk 웹 UI](snyk-cloud-for-aws-web-ui/)
* [Snyk API](snyk-cloud-for-aws-api/)

## 전제 조건

Snyk Cloud 사용을 시작하려면 다음이 필요합니다:

* Snyk 비즈니스 또는 사업 [계획](https://snyk.io/plans/)
* Snyk 담당자가 할당한 적절한 기능 플래그가 있는 새 조직
* Snyk 그룹 관리자 또는 조직 관리자 [역할](https://docs.snyk.io/features/user-and-group-management/managing-users-and-permissions/managing-permissions)
* 조직 관리자 역할이 있는 조직 수준 [서비스 계정](https://docs.snyk.io/features/user-and-group-management/structure-account-for-high-application-performance/service-accounts#set-up-a-service-account)
* 읽기 전용 IAM 역할을 생성할 수 있는 권한이 있는 [AWS](https://aws.amazon.com/) 계정 및 연결된 자격 증명에 대한 액세스
* [Terraform CLI](https://www.terraform.io/downloads), [AWS CLI](https://aws.amazon.com/cli/), 또는 [AWS Management Console](https://console.aws.amazon.com) 에 액세스하여 Terraform 또는 AWS Cloudformation을 통해 Snyk에 대한 IAM 역할 생성
  * [Terraform](https://registry.terraform.io/providers/hashicorp/aws/latest/docs#authentication-and-configuration) 또는 [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-quickstart.html) 를 사용하는 경우 AWS 자격 증명으로 구성해야 합니다. 에 대한 지침을 확인하십시오.
* **API 전용:** [curl](https://curl.se/), [HTTPie](https://httpie.io/), [Postman](https://www.postman.com/)과 같은 API 클라이언트
