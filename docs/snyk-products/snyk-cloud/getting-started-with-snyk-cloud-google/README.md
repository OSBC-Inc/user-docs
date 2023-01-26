# Snyk Cloud 시작하기: Google

Snyk Cloud는 [Google Cloud](https://cloud.google.com/) 프로젝트의 인프라 구성을 스캔하여 취약성으로 이어질 수 있는 구성 오류를 예상하고 감지합니다.

다음 방법을 사용하여 Google Cloud 계정을 Snyk에 온보딩할 수 있습니다:

* [Snyk 웹 UI](snyk-cloud-for-google-web-ui/)
* [Snyk API](snyk-cloud-for-google-api/)

## 전제 조건

Snyk Cloud 사용을 시작하기 위해 다음이 필요합니다:

* Snyk 비즈니스 또는 사업 [계획](https://snyk.io/plans/)
* Snyk 담당자가 할당한 적절한 기능 플래그가 있는 새 Snyk 조직
* Snyk 그룹 관리자 또는 조직 관리자 [역할](https://docs.snyk.io/features/user-and-group-management/managing-users-and-permissions/managing-permissions)
* 조직 관리자 역할이 있는 조직 수준 [서비스 계정](https://docs.snyk.io/features/user-and-group-management/structure-account-for-high-application-performance/service-accounts#set-up-a-service-account)&#x20;
* 읽기 전용 Google 서비스 계정을 만들 수 있는 권한이 있는 [Google Cloud](https://cloud.google.com/) 프로젝트 및 연결된 사용자 인증 정보에 대한 액세스
* Snyk용 Google 서비스 계정을 생성하기 위한 [Google 자격 증명으로 구성된](https://registry.terraform.io/providers/hashicorp/google/latest/docs/guides/getting\_started) [Terraform CLI](https://www.terraform.io/downloads) 대한 엑세스
* **API 전용:** [curl](https://curl.se/), [HTTPie](https://httpie.io/), [Postman](https://www.postman.com/) 같은 API 클라이언트
* **API 전용 (선택 사항)**: Terraform 템플릿 서비스 계정을 포함한 JSON을 이스케이프 해제하기 위한 [jq](https://stedolan.github.io/jq/)
