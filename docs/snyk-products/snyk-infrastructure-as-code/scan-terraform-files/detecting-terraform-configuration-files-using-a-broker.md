# 브로커를 사용하여 Terraform 구성 파일 탐지

비공개로 호스팅되는 Git 저장소를 사용하는 경우 Snyk Broker를 사용하여 저장소에 Snyk를 연결할 수 있습니다. 자세한 내용은 [full broker documentation for setup](../../../features/integrations/snyk-broker/set-up-snyk-broker.md)을 참조하십시오. 다음은 Terraform 파일에 필요한 추가 구성에 대해 자세히 설명합니다.

## Configuration 작성

Terraform 스캔 기능을 사용하려면 저장소에서 `.tf` 파일에 액세스해야 합니다. 이를 위해서는 특정 API 사용 권한이 필요합니다. 이러한 API 권한은 사용 중인 소스 제어 시스템에 따라 다릅니다.

1. [Broker 저장소](https://github.com/snyk/broker/tree/master/client-templates)에서 소스 제어 시스템에 적합한 Accept.json 샘플 파일을 찾아 다운로드합니다.
2. 이름을 `accept.json`으로 바꾸고 SCM에 해당하는 아래 규칙을 JSON 파일의 **private** array에 추가하십시오.
3. [브로커 구성](detecting-terraform-configuration-files-using-a-broker.md#undefined)을 진행합니다.

## GitHub rules

```
{
  "//": "used to determine Terraform issues",
  "method": "GET",
  "path": "/repos/:name/:repo/contents/:path*/*.tf",
  "origin": "https://${GITHUB_TOKEN}@${GITHUB_API}"
},
{
  "//": "used to determine Terraform issues",
  "method": "GET",
  "path": "/repos/:name/:repo/contents/:path*%2F*.tf",
  "origin": "https://${GITHUB_TOKEN}@${GITHUB_API}"
},
```

## Bitbucket rules

```
{
  "//": "used to determine Terraform issues",
  "method": "GET",
  "path": "/projects/:project/repos/:repo/browse*/*.tf",
  "origin": "https://${BITBUCKET_API}",
  "auth": {
    "scheme": "basic",
    "username": "${BITBUCKET_USERNAME}",
    "password": "${BITBUCKET_PASSWORD}"
  }
},
{
  "//": "used to determine Terraform issues",
  "method": "GET",
  "path": "/projects/:project/repos/:repo/browse*%2F*.tf",
  "origin": "https://${BITBUCKET_API}",
  "auth": {
    "scheme": "basic",
    "username": "${BITBUCKET_USERNAME}",
    "password": "${BITBUCKET_PASSWORD}"
  }
},
```

## GitLab rules

```
{
  "//": "used to determine Terraform issues",
  "method": "GET",
  "path": "/api/v4/projects/:project/repository/files*/*.tf",
  "origin": "https://${GITLAB}"
},
{
  "//": "used to determine Terraform issues",
  "method": "GET",
  "path": "/api/v4/projects/:project/repository/files*%2F*.tf",
  "origin": "https://${GITLAB}"
},
```

## 브로커 구성

브로커는 ACCEPT 환경 변수의 Accept.json 파일(위의 규칙이 추가됨)에 대한 경로를 사용합니다. 아래에서 GitHub 브로커에게 전달한 예를 볼 수 있습니다.

```
docker run --restart=always \
  -p 8000:8000 \
  -e BROKER_TOKEN=secret-broker-token \
  -e GITHUB_TOKEN=secret-github-token \
  -e PORT=8000 \
  -e BROKER_CLIENT_URL=https://my.broker.client:8000 \
  -e ACCEPT=/private/accept.json
  -v /local/path/to/private:/private \
  snyk/broker:github-com
```

**Note**: 이를 통해 Snyk은 모든 .tf 파일을 쿼리할 수 있습니다. 더 정확해지려면 위의 예제의 경로를 특정 프로젝트나 파일 레이아웃으로 더 제한하도록 변경할 수 있습니다.
