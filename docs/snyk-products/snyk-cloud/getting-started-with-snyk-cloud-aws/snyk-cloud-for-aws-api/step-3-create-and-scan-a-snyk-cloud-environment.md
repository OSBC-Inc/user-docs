# 3단계: Snyk Cloud 환경 생성 및 스캔 (API)

{% hint style="info" %}
**개요**\
Snyk Cloud IAM 역할을 만들었습니다. 이제 Snyk Cloud 환경을 생성하고 스캔할 수 있습니다.
{% endhint %}

Snyk Cloud 환경을 생성 및 스캔하기 위해 [Snyk API](https://apidocs.snyk.io/?version=2022-12-21%7Ebeta#post-/orgs/-org\_id-/cloud/environments) 에 요청을 전송하려면 API 요청 본문에 역할의 ARN(Amazon Resource Name)을 제공해야 합니다.

## 역할 ARN 찾기

[역할 ARN 찾기](../snyk-cloud-for-aws-web-ui/step-3-create-and-scan-a-snyk-cloud-environment-web-ui.md#find-the-role-arn)의 단계를 따르고 여기로 돌아와 Snyk API 요청을 전송하는 방법을 알아보십시오.

## Snyk API 요청 전송

역할 ARN이 있다면 Snyk API에 아래와 같은 형식으로 요청을 전송해 Snyk Cloud 환경을 생성하십시오.

```
curl -X POST \
'https://api.snyk.io/rest/orgs/YOUR-ORGANIZATION-ID/cloud/environments?version=2022-12-21~beta' \
-H 'Authorization: token YOUR-API-TOKEN' \
-H 'Content-Type:application/vnd.api+json' -d '{
  "data": {
    "attributes": {
      "kind": "aws",
      "name": "Example AWS Environment",
      "options": {
        "role_arn": "YOUR-ROLE-ARN"
      }
    },
    "type": "environment"
  }
}'
```

{% hint style="info" %}
위의 예시는  [curl](https://curl.se/) 사용하지만 [Postman](https://www.postman.com/) 이나 [HTTPie](https://httpie.io/) 같은  모든API 클라이언트를 사용할 수 있습니다.
{% endhint %}

## API 응답 이해

응답은 새로 생성된 Snyk Cloud 환경에 관한 세부 정보가 포함된 JSON 문서입니다. 예를 들어:

```json
{
  "jsonapi": {
    "version": "1.0"
  },
  "data": {
    "id": "3b7ccff9-8900-4e54-0000-1234abcd1234",
    "type": "environment",
    "attributes": {
      "name": "Example AWS Environment",
      "options": {
        "role_arn": "arn:aws:iam::123412341234:role/snyk-cloud-role"
      },
      "native_id": "123412341234",
      "properties": {
        "account_id": "123412341234",
        "account_alias": "example"
      },
      "kind": "aws",
      "revision": 1,
      "created_at": "2022-07-31T00:50:49Z",
      "status": "in_progress",
      "updated_at": "2022-07-31T00:50:49Z"
    },
    "relationships": {
      "organization": {
        "data": {
          "id": "d70c1768-5675-0000-1234-abcd1234abcd",
          "type": "organization"
        },
        "links": {
          "related": "/orgs/d70c1768-5675-0000-1234-abcd1234abcd?version=2022-12-21~beta"
        }
      }
    }
  }
}
```

은 환경이 생성되었을 때 자동으로 스캔을 트리거합니다.

참고:  JSON 출력의 `data.attributes.status` 필드는`in_progress`로 설정됩니다. 이는 Snyk이 환경을 생성하고 스캔을 시작했다는 것을 의미합니다.

## 스캔 완료 여부 확인

선택적으로, 환경 세부 정보를 얻기 위해 아래 형식으로 다른 API 요청을 전송하여 스캔이 완료되었는지 확인합니다. 환경 ID는 환경을 생성할 때 JSON 출력의 `data.id`필드에서 확인할 수 있습니다.

```
curl -X GET \
  'https://api.snyk.io/rest/orgs/YOUR-ORGANIZATION-ID/cloud/environments?id=YOUR-ENVIRONMENT-ID&version=2022-12-21~beta' \
  -H 'Authorization: token YOUR-API-TOKEN'
```

JSON 출력의`data.attributes.status` 필드가  `success`로 설정되었다면 Snyk이 환경 스캔을 완료한 것입니다.

환경을 다시 스캔하기 위해선[ Snyk Cloud 환경 스캔](../../scan-a-snyk-cloud-environment.md) 참조하십시오.

## 다음 단계

이제 Snyk 웹 UI에서 구성 오류 문제를 볼 수 있습니다. 자세한 내용은 [Snyk Cloud 이슈](../../snyk-cloud-issues/)를 참조하십시오.
