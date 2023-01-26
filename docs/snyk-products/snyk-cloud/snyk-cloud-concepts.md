# Snyk Cloud 개념

Snyk Cloud에는[ Snyk 핵심 개념](https://github.com/snyk/user-docs/blob/main/docs/products/snyk-cloud/broken-reference/README.md)과 별개로 여러가지 고유한 개념이 있습니다.

## 환경

Snyk Cloud **환경**은 Amazon Web Services(AWS) 계정, Azure 구독 또는 Google Cloud 프로젝트와 동일한 구성 개념입니다.

Snyk [프로젝트](broken-reference/)와 달리 환경은 [리소스](snyk-cloud-concepts.md#resources)로 알려진 스캔 가능한 실체를 포함하고 있습니다. 리소스는 서로 연관될 수 있습니다. 한 리소스는 다른 리소스의 하위 또는 동위 리소스일 수 있습니다. 리소스에는 테스트할 수 있는 속성도 있으며, 이 속성은 잘못 구성되어 Snyk Cloud 문제를 생성할 수 있습니다. 이것이 환경과 리소스가 프로젝트와 다른 점입니다.

Snyk Cloud 환경에는 클라우드 공급자에 대한 통합 설정도 포함합니다. 예를 들어 각 환경은 다른 AWS 계정과의 통합을 나타낼 수 있습니다.

&#x20;[`/cloud/environments`](https://apidocs.snyk.io/?version=2022-12-21%7Ebeta#get-/orgs/-org\_id-/cloud/environments) Snyk 엔드포인트를 사용하여 모든 환경 목록을 검색하고 선택적으로 이름 및 스캔 상태와 같은 속성별로 필터링합니다.

현재 지원되는 공급자:

* [Amazon Web Services](https://aws.amazon.com/)
* [Google Cloud](https://cloud.google.com/)

## 리소스

**리소스** 는 AWS S3 버킷, Identity & Access Management (IAM) 역할 또는 Virtual Private Cloud (VPC) 흐름 로그와 같은 클라우드 인프라 독립체입니다.

각 스캔에서 Snyk는 환경에 있는 각 리소스의 구성 속성을 기록합니다.

[`/cloud/resources`](https://apidocs.snyk.io/?version=2022-12-21%7Ebeta#get-/orgs/-org\_id-/cloud/resources) Snyk API 엔드포인트를 사용하여 조직의 모든 리소스 목록을 검색하고 선택적으로 환경 ID, 리소스 ID 또는 리소스 유형과 같은 속성으로 필터링할 수 있습니다.

지원되는 리소스 유형 목록은 다음을 참조하십시오:

* [지원되는 AWS 리소스](supported-aws-resources-for-snyk-cloud.md)
* [지원되는Google 리소스](supported-google-resources-for-snyk-cloud.md)

## 규칙

보안 **규칙**은 보안 문제로 이어질 수 있는 구성 오류에 대해 클라우드 인프라 및 코드형 인프라(IaC)를 검사합니다. Snyk Cloud 환경과 Snyk IaC 프로젝트 모두에 적용할 수 있는 [미리 정의된 규칙](https://snyk.io/security-rules/cloud)이 있습니다.

예시 규칙: "S3 버킷에 모든 퍼블릭 액세스 차단 옵션이 활성화되어 있지 않습니다." Snyk은 AWS S3 버킷의 구성을 스캔하여 규칙에 실패하는지확인하므로 데이터 위반에 취약합니다.

## 이슈

클라우드 **이슈**는 리소스 및 규칙과 연관된, 보안 문제로 이어질 수 있는 구성 오류를 나타냅니다. 예를 들어 AWS S3 버밋은 "S3 버킷에 모든 블록 퍼블릭 액세스 옵션이 활성화되어 있지 않습니다."라는 규칙에 대해 테스트할 수 있습니다. 버킷이 규칙에 실패하면 Snyk은 클라우드 이슈를 엽니다.

Snyk은 이슈를 생성한 후, 구성 오류가 수정될 때까지 문제를 열어 둡니다.

Snyk 웹 UI에서 조직의 이슈를 볼 수 있습니다. [Snyk 웹 UI에서 클라우드 이슈 보기](snyk-cloud-issues/view-cloud-issues-in-the-snyk-web-ui.md)를 참조하십시오.

## 컴플라이언스 표준 <a href="#docs-internal-guid-e2e38027-7fff-9271-f2c0-e23677542f6e" id="docs-internal-guid-e2e38027-7fff-9271-f2c0-e23677542f6e"></a>

컴플라이언스 표준은 조직이 IT 시스템과 인프라를 보호하기 위한 지침과 제어를 설정하는 프레임워크입니다. 컴플라이언스 표준은 "버전화"되어있으며, 다양한 단계에서 버전이 생성됩니다. 예시: NIST 800-53(vRev5), CIS AWS Foundations Benchmark (v1.4.0). Snyk은 [클라우드 컴플라이언스 이슈 레포트](../../manage-issues/snyk-reports/reporting-beta-2022/available-snyk-reports.md#cloud-compliance-issues-report)를 제공합니다.

## 컴플라이언스 컨트롤 <a href="#docs-internal-guid-11e1473c-7fff-ea66-c8f4-16a826a82e6b" id="docs-internal-guid-11e1473c-7fff-ea66-c8f4-16a826a82e6b"></a>

컴플라이언스 컨트롤은 조직이 시스템 또는 인프라를 보호하는 방법을 규정하는 컴플라이언스 표준의 특정 권장 사항 또는 지침입니다. 예: control 2.1.5  CIS AWS Foundation Benchmark (v1.4.0)의 컨트롤 2.1.5는"S3 버킷이 '공개 액세스 차단(버킷 설정)으로 구성되어 있는지 확인" 입니다. 이 제어를 준수하기 위해 조직은 모든 S3 버킷에 대해 "퍼블릭 액세스 차단" 설정을 활성화합니다.

## 컴플라이언스 매핑

Snyk은 보안 [규칙](snyk-cloud-concepts.md#undefined-2)을 컴플라이언스 컨트롤에 "매핑"합니다. 즉, 각 규칙은 하나 이상의 컨트롤과 연결되고 각 제어는 하나 이상의 규칙과 연결됩니다.

예를 들어 CIS AWS Foundations Benchmark (v1.4.0)의 컨트롤 2.1.5 는 "S3 버킷이 '퍼블릭 액세스 차단(버킷 설정)'으로 구성되어 있는지 확인"이며 보안 규칙[ SNYK-CC-00195](https://snyk.io/security-rules/cloud/SNYK-CC-00195/s3-bucket-does-not-have-all-block-public-access-options-enabled/), "S3 버킷에 모든 블록 공용 액세스 옵션이 활성화 되어 있지 않습니다" 에 매핑됩니다.
