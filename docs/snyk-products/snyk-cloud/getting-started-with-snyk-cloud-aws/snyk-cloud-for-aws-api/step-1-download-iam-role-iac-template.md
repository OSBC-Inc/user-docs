# 1단계: IAM 역할 IaC 템플릿 다운로드 (API)

Snyk Cloud 환경을 생성하기 전에 AWS(Amazon Web Services)의 리소스 구성을 스캔하기 위해 Snyk가 가정할 수 있는 읽기 전용 **IAM(Identity & Access Management)** 역할을 선언하는 IaC(Infrastructure as Code) 템플릿을 다운로드해야 합니다.

이 IaC 템플릿을 사용하여 [2단계: Snyk IAM role 생성](../snyk-cloud-for-aws-web-ui/step-2-create-the-snyk-iam-role.md)에서 역할을 프로비저닝합니다.

[Terraform HCL](https://www.terraform.io/language/syntax/configuration) 또는 [AWS CloudFormation](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/Welcome.html) 템플릿 형식을 선택할 수 있습니다. IAM 권한은 동일하므로 작업하기 편한 형식을 선택하십시오.

## IaC 템플릿 검색

[Snyk API](https://apidocs.snyk.io/?version=2022-12-21%7Ebeta#post-/orgs/-org\_id-/cloud/permissions)에서 IaC 템플릿을 검색하려면 조직 관리자 역할이 있는 조직 수준 [서비스 계정](https://docs.snyk.io/features/user-and-group-management/structure-account-for-high-application-performance/service-accounts#set-up-a-service-account)에 대한 API 토큰이 필요합니다.

1. [Snyk 웹 UI](https://app.snyk.io) **Settings (톱니바퀴 아이콘) > General > Organization ID** 로 이동하여 조직 ID를 복사하십시오.
2. `INPUT-TYPE` 을 Terraform용 `tf` 또는 CloudFormation용 `cf`로 대체하여 아래 형식으로 Snyk API에 요청을 보냅니다:

```
curl -X POST \
'https://api.snyk.io/rest/orgs/YOUR-ORGANIZATION-ID/cloud/permissions?version=2022-12-21~beta' \
-H 'Authorization: token YOUR-API-TOKEN' \
-H 'Content-Type:application/vnd.api+json' -d '{
    "data": {
        "attributes": {
            "type": "INPUT-TYPE",
            "platform": "aws"
        },
        "type": "permissions"
    }
}'
```

{% hint style="info" %}
위의 예제는 [curl](https://curl.se/) 사용하지만 [Postman](https://www.postman.com/) [HTTPie](https://httpie.io/) 같은 API 클라이언트를 사용할 수 있습니다
{% endhint %}

## API 응답 이해

응답은 아래와 같은 JSON 문서입니다. (길이에 맞게 잘림)

Terraform 구성을 사용한 응답 예시:

```json
{
  "jsonapi": {
    "version": "1.0"
  },
  "data": {
    "id": "00000000-0000-0000-0000-000000000000",
    "type": "permissions",
    "attributes": {
      "data": "data \"aws_iam_policy_document\"<...>",
      "type": "tf"
    }
  }
}
```

CloudFormation 템플릿을 사용한 응답 예시

```json
{
  "jsonapi": {
    "version": "1.0"
  },
  "data": {
    "id": "00000000-0000-0000-0000-000000000000",
    "type": "permissions",
    "attributes": {
      "data": "AWSTemplateFormatVersion:<...>",
      "type": "cf"
    }
  }
}
```

## JSON 이스케이프 해제

위 출력의 `data.attributes.data` 필드는 IAM 역할 및 정책과 함께 Terraform 또는 CloudFormation 템플릿을 포함하는 이스케이프 처리된 JSON 문자열입니다.

템플릿을 사용하여 리소스를 프로비저닝하기 전에 JSON의 이스케이프를 해제해야 합니다. 이것은 다음과 같은 방식으로 수행할 수 있습니다:

* [jq 사용](step-1-download-iam-role-iac-template.md#use-jq)
* [콘텐츠를 수동으로 변환](step-1-download-iam-role-iac-template.md#transform-the-content-manually)

**`jq` 사용**

1. [jq](https://stedolan.github.io/jq/download/) 를다운로드 및 설치하십시오.
2.  템플릿 검색 중 API 요청을 제출할 때 명령 끝에 다음을 추가하십시오:

    ```
    | jq -r .data.attributes.data > snyk_iac_template
    ```

    이렇게 하면 올바른 형식의 템플릿이 현재 작업 디렉토리의`snyk_iac_template` 파일에 저장됩니다.
3. `.tf` 확장자(Terraform) 또는 `.yaml` (CloudFormation)을 사용하여 파일 이름을 변경하십시오.

### 콘텐츠를 수동으로 변환

1. API 응답의`data.attributes.data` 값에서 처음과 맨 끝에 있는 큰따옴표를 제외한 내용을 복사하십시오.  `data \"aws_iam_policy_document\"` (Terraform) 또는 `AWSTemplateFormatVersion` (CloudFormation)로 시작하는 긴 문자열로 끝나야 합니다.
2. 문자열을 [FreeFormatter.com](https://www.freeformatter.com/json-escape.html) 과 같은 도구에 붙여넣어 JSON의 이스케이프를 해제하십시오.
3. Save the unescaped CloudFormation output as a new `.tf` file (Terraform) or `.yaml` file (CloudFormation).

## 선택 사항: IAM 역할 이름 변경

기본적으로 Snyk IAM 역할의 이름은 `snyk-cloud-role`입니다. 조직에 특정 역할 명명 요구사항이 있는 경우 선택적으로 Terraform 또는 CloudFormation 템플릿에서 이름을 변경할 수 있습니다.

**Terraform**의 경우 역할 이름은 19행에 있습니다.

`name     = "snyk-cloud-role"`

**CloudFormation**의 경우 역할 이름은 7행에 있습니다.

&#x20;  `RoleName: snyk-cloud-role`

## 다음 단계

다음 단계는 다운로드한 템플릿을 사용하여 Snyk Cloud에 대한 IAM 역할 및 정책을 생성하는 것입니다.
