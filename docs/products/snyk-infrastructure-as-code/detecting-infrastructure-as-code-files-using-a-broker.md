# 브로커를 사용하여 infrastructure as code 파일 감지

비공개로 호스팅되는 Git 저장소를 사용하는 경우 Snyk Broker를 사용하여 저장소에 Snyk를 연결할 수 있습니다. 자세한 내용은 [full broker documentation for setup](../../features/integrations/snyk-broker/set-up-snyk-broker.md)을 참조하세요.

이 문서에는 Infrastructure as Code 파일에 필요하는 추가 구성에 대해 설명합니다.

## Configuration 작성

저장소의 특정 파일에 대한 브로커 액세스 권한을 부여해야 합니다. 이를 위해서는 특정 API 사용 권한이 필요합니다. 이러한 API 권한은 사용 중인 소스 제어 시스템에 따라 다릅니다. 아래 구성은 파일 확장자 `.yaml`, `.yml` 및 `.json`에 대한 것으로, 브로커가 잠재적인 Kubernetes 및 CloudFormation 파일에 액세스할 수 있지만 필요에 따라 조정하십시오. 예를 들어, Terraform HCL 파일을 검색하기 위해 `.tf` 파일에 대한 구성을 추가할 수 있습니다.

1. [Broker 저장소](https://github.com/snyk/broker/tree/master/client-templates)에서 소스 제어 시스템에 적합한 Accept.json 샘플 파일을 찾아 다운로드합니다.
2. 이름을 `accept.json`으로 바꾸고 SCM에 해당하는 아래 규칙을 JSON 파일의 **private** array에 추가하세요.
3. [Configuring the broker](scan-cloudformation-files/detecting-cloudformation-configuration-files-using-a-broker.md) 지침을 따릅니다.

## GitHub & GitHub Enterprise rules

```
{
  "//": "used to determine Infrastructure as Code issues",
  "method": "GET",
  "path": "/repos/:name/:repo/contents/:path*/*.yaml",
  "origin": "https://${GITHUB_TOKEN}@${GITHUB_API}"
},
{
  "//": "used to determine Infrastructure as Code issues",
  "method": "GET",
  "path": "/repos/:name/:repo/contents/:path*%2F*.yaml",
  "origin": "https://${GITHUB_TOKEN}@${GITHUB_API}"
},
{
  "//": "used to determine Infrastructure as Code issues",
  "method": "GET",
  "path": "/repos/:name/:repo/contents/:path*/*.yml",
  "origin": "https://${GITHUB_TOKEN}@${GITHUB_API}"
},
{
  "//": "used to determine Infrastructure as Code issues",
  "method": "GET",
  "path": "/repos/:name/:repo/contents/:path*%2F*.yml",
  "origin": "https://${GITHUB_TOKEN}@${GITHUB_API}"
},
{
  "//": "used to determine Infrastructure as Code issues",
  "method": "GET",
  "path": "/repos/:name/:repo/contents/:path*/*.json",
  "origin": "https://${GITHUB_TOKEN}@${GITHUB_API}"
},
{
  "//": "used to determine Infrastructure as Code issues",
  "method": "GET",
  "path": "/repos/:name/:repo/contents/:path*%2F*.json",
  "origin": "https://${GITHUB_TOKEN}@${GITHUB_API}"
},
{
  "//": "used to determine Infrastructure as Code issues",
  "method": "GET",
  "path": "/repos/:name/:repo/contents/:path*/*.tpl",
  "origin": "https://${GITHUB_TOKEN}@${GITHUB_API}"
},
{
  "//": "used to determine Infrastructure as Code issues",
  "method": "GET",
  "path": "/repos/:name/:repo/contents/:path*%2F*.tpl",
  "origin": "https://${GITHUB_TOKEN}@${GITHUB_API}"
},
```

## Bitbucket rules

```
{
  "//": "used to determine Infrastructure as Code issues",
  "method": "GET",
  "path": "/projects/:project/repos/:repo/browse*/*.yaml",
  "origin": "https://${BITBUCKET_API}",
  "auth": {
    "scheme": "basic",
    "username": "${BITBUCKET_USERNAME}",
    "password": "${BITBUCKET_PASSWORD}"
  }
},
{
  "//": "used to determine Infrastructure as Code issues",
  "method": "GET",
  "path": "/projects/:project/repos/:repo/browse*%2F*.yaml",
  "origin": "https://${BITBUCKET_API}",
  "auth": {
    "scheme": "basic",
    "username": "${BITBUCKET_USERNAME}",
    "password": "${BITBUCKET_PASSWORD}"
  }
},
{
  "//": "used to determine Infrastructure as Code issues",
  "method": "GET",
  "path": "/projects/:project/repos/:repo/browse*/*.yml",
  "origin": "https://${BITBUCKET_API}",
  "auth": {
    "scheme": "basic",
    "username": "${BITBUCKET_USERNAME}",
    "password": "${BITBUCKET_PASSWORD}"
  }
},
{
  "//": "used to determine Infrastructure as Code issues",
  "method": "GET",
  "path": "/projects/:project/repos/:repo/browse*%2F*.yml",
  "origin": "https://${BITBUCKET_API}",
  "auth": {
    "scheme": "basic",
    "username": "${BITBUCKET_USERNAME}",
    "password": "${BITBUCKET_PASSWORD}"
  }
},
{
  "//": "used to determine Infrastructure as Code issues",
  "method": "GET",
  "path": "/projects/:project/repos/:repo/browse*/*.json",
  "origin": "https://${BITBUCKET_API}",
  "auth": {
    "scheme": "basic",
    "username": "${BITBUCKET_USERNAME}",
    "password": "${BITBUCKET_PASSWORD}"
  }
},
{
  "//": "used to determine Infrastructure as Code issues",
  "method": "GET",
  "path": "/projects/:project/repos/:repo/browse*%2F*.json",
  "origin": "https://${BITBUCKET_API}",
  "auth": {
    "scheme": "basic",
    "username": "${BITBUCKET_USERNAME}",
    "password": "${BITBUCKET_PASSWORD}"
  }
},
{
  "//": "used to determine Infrastructure as Code issues",
  "method": "GET",
  "path": "/projects/:project/repos/:repo/browse*/*.tpl",
  "origin": "https://${BITBUCKET_API}",
  "auth": {
    "scheme": "basic",
    "username": "${BITBUCKET_USERNAME}",
    "password": "${BITBUCKET_PASSWORD}"
  }
},
{
  "//": "used to determine Infrastructure as Code issues",
  "method": "GET",
  "path": "/projects/:project/repos/:repo/browse*%2F*.tpl",
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
  "//": "used to determine Infrastructure as Code issues",
  "method": "GET",
  "path": "/api/v4/projects/:project/repository/files*/*.yaml",
  "origin": "https://${GITLAB}"
},
{
  "//": "used to determine Infrastructure as Code issues",
  "method": "GET",
  "path": "/api/v4/projects/:project/repository/files*%2F*.yaml",
  "origin": "https://${GITLAB}"
},
{
  "//": "used to determine Infrastructure as Code issues",
  "method": "GET",
  "path": "/api/v4/projects/:project/repository/files*/*.yml",
  "origin": "https://${GITLAB}"
},
{
  "//": "used to determine Infrastructure as Code issues",
  "method": "GET",
  "path": "/api/v4/projects/:project/repository/files*%2F*.yml",
  "origin": "https://${GITLAB}"
},
{
  "//": "used to determine Infrastructure as Code issues",
  "method": "GET",
  "path": "/api/v4/projects/:project/repository/files*/*.json",
  "origin": "https://${GITLAB}"
},
{
  "//": "used to determine Infrastructure as Code issues",
  "method": "GET",
  "path": "/api/v4/projects/:project/repository/files*%2F*.json",
  "origin": "https://${GITLAB}"
},
{
  "//": "used to determine Infrastructure as Code issues",
  "method": "GET",
  "path": "/api/v4/projects/:project/repository/files*/*.tpl",
  "origin": "https://${GITLAB}"
},
{
  "//": "used to determine Infrastructure as Code issues",
  "method": "GET",
  "path": "/api/v4/projects/:project/repository/files*%2F*.tpl",
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

**Note**: 이를 통해 Snyk은 모든 `.yaml`, `.yml` 또는 `.json` 파일을 쿼리할 수 있습니다. 더 정확해지려면 위의 예제의 경로를 특정 프로젝트나 파일 레이아웃으로 더 제한하도록 변경할 수 있습니다.

## Azure repo

```
{
  "public": [
    {
      "//": "used for pushing up webhooks from Azure",
      "method": "POST",
      "path": "/webhook/azure-repos/:webhookId"
    }
  ],
  "private": [
    {
      "//": "get list of projects for given organisation",
      "method": "GET",
      "path": "/_apis/projects",
      "origin": "https://${AZURE_REPOS_HOST}/${AZURE_REPOS_ORG}",
      "auth": {
        "scheme": "basic",
        "token": "${BROKER_CLIENT_VALIDATION_BASIC_AUTH}"
      }
    },
    {
      "//": "get specific repository for given organisation",
      "method": "GET",
      "path": "/:owner/_apis/git/repositories/:repo",
      "origin": "https://${AZURE_REPOS_HOST}/${AZURE_REPOS_ORG}",
      "auth": {
        "scheme": "basic",
        "token": "${BROKER_CLIENT_VALIDATION_BASIC_AUTH}"
      }
    },
    {
      "//": "get list of repositories for given organisation",
      "method": "GET",
      "path": "/:owner/_apis/git/repositories",
      "origin": "https://${AZURE_REPOS_HOST}/${AZURE_REPOS_ORG}",
      "auth": {
        "scheme": "basic",
        "token": "${BROKER_CLIENT_VALIDATION_BASIC_AUTH}"
      }
    },
    {
      "//": "get list of refs",
      "method": "GET",
      "path": "/:owner/_apis/git/repositories/:repo/refs",
      "origin": "https://${AZURE_REPOS_HOST}/${AZURE_REPOS_ORG}",
      "auth": {
        "scheme": "basic",
        "token": "${BROKER_CLIENT_VALIDATION_BASIC_AUTH}"
      }
    },
    {
      "//": "search through repositories of given organisation",
      "method": "GET",
      "path": "_apis/git/repositories",
      "origin": "https://${AZURE_REPOS_HOST}/${AZURE_REPOS_ORG}",
      "auth": {
        "scheme": "basic",
        "token": "${BROKER_CLIENT_VALIDATION_BASIC_AUTH}"
      }
    },
    {
      "//": "create hook",
      "method": "POST",
      "path": "/_apis/hooks/subscriptions",
      "origin": "https://${AZURE_REPOS_HOST}/${AZURE_REPOS_ORG}",
      "auth": {
        "scheme": "basic",
        "token": "${BROKER_CLIENT_VALIDATION_BASIC_AUTH}"
      }
    },
    {
      "//": "delete hook",
      "method": "DELETE",
      "path": "/_apis/hooks/subscriptions/:subscriptionId",
      "origin": "https://${AZURE_REPOS_HOST}/${AZURE_REPOS_ORG}",
      "auth": {
        "scheme": "basic",
        "token": "${BROKER_CLIENT_VALIDATION_BASIC_AUTH}"
      }
    },
    {
      "//": "get file content. restrict by file types",
      "method": "GET",
      "path": "/:owner/_apis/git/repositories/:repo/items",
      "origin": "https://${AZURE_REPOS_HOST}/${AZURE_REPOS_ORG}",
      "valid": [
        {
          "queryParam": "path",
          "values": [
            "**/package.json",
            "**%2Fpackage.json",
            "**/yarn.lock",
            "**%2Fyarn.lock",
            "**/package-lock.json",
            "**%2Fpackage-lock.json",
            "**/Gemfile",
            "**%2FGemfile",
            "**/Gemfile.lock",
            "**%2FGemfile.lock",
            "**/pom.xml",
            "**%2Fpom.xml",
            "**/*req*.txt",
            "**%2F*req*.txt",
            "**/requirements/*.txt",
            "**%2Frequirements%2F*.txt",
            "**/build.gradle",
            "**%2Fbuild.gradle",
            "**/gradle.lockfile",
            "**%2Fgradle.lockfile",
            "**/build.sbt",
            "**%2Fbuild.sbt",
            "**/.snyk",
            "**%2F.snyk",
            "**/packages.config",
            "**%2Fpackages.config",
            "**/*.csproj",
            "**%2F*.csproj",
            "**/*.vbproj",
            "**%2F*.vbproj",
            "**/*.fsproj",
            "**%2F*.fsproj",
            "**/project.json",
            "**%2Fproject.json",
            "**/Gopkg.toml",
            "**%2FGopkg.toml",
            "**/Gopkg.lock",
            "**%2FGopkg.lock",
            "**/vendor.json",
            "**%2Fvendor.json",
            "**/composer.lock",
            "**%2Fcomposer.lock",
            "**/composer.json",
            "**%2Fcomposer.json",
            "**/project.assets.json",
            "**%2Fproject.assets.json",
            "**/Podfile",
            "**%2FPodfile",
            "**/Podfile.lock",
            "**%2FPodfile.lock",
            "**/go.mod",
            "**%2Fgo.mod",
            "**/go.sum",
            "**%2Fgo.sum",
            "**/Dockerfile",
            "**%2FDockerfile"
          ]
        },
        {
          "queryParam": "recursionLevel",
          "values": ["none"]
        },
        {
          "queryParam": "download",
          "values": ["true"]
        },
        {
          "queryParam": "includeContent",
          "values": ["true"]
        }
      ],
      "auth": {
        "scheme": "basic",
        "token": "${BROKER_CLIENT_VALIDATION_BASIC_AUTH}"
      }
    },
    {
      "//": "get list of files for given repository",
      "method": "GET",
      "path": "/:owner/_apis/git/repositories/:repo/items",
      "origin": "https://${AZURE_REPOS_HOST}/${AZURE_REPOS_ORG}",
      "valid": [
        {
          "queryParam": "recursionLevel",
          "values": ["full"]
        },
        {
          "queryParam": "download",
          "values": ["false"]
        },
        {
          "queryParam": "includeContent",
          "values": ["false"]
        }
      ],
      "auth": {
        "scheme": "basic",
        "token": "${BROKER_CLIENT_VALIDATION_BASIC_AUTH}"
      }
    },
    {
      "//": "get list of commits for given repository",
      "method": "GET",
      "path": "/:owner/_apis/git/repositories/:repo/commits",
      "origin": "https://${AZURE_REPOS_HOST}/${AZURE_REPOS_ORG}",
      "auth": {
        "scheme": "basic",
        "token": "${BROKER_CLIENT_VALIDATION_BASIC_AUTH}"
      }
    },
    {
      "//": "update status of given commit",
      "method": "POST",
      "path": "/:owner/_apis/git/repositories/:repo/commits/:commitId/statuses",
      "origin": "https://${AZURE_REPOS_HOST}/${AZURE_REPOS_ORG}",
      "auth": {
        "scheme": "basic",
        "token": "${BROKER_CLIENT_VALIDATION_BASIC_AUTH}"
      }
    },
    {
      "//": "update status of given pull request",
      "method": "POST",
      "path": "/:owner/_apis/git/repositories/:repo/pullRequests/:pullRef/statuses",
      "origin": "https://${AZURE_REPOS_HOST}/${AZURE_REPOS_ORG}",
      "auth": {
        "scheme": "basic",
        "token": "${BROKER_CLIENT_VALIDATION_BASIC_AUTH}"
      }
    },
    {
      "//": "find PR for given repository",
      "method": "GET",
      "path": "/:owner/_apis/git/repositories/:repo/pullrequests",
      "origin": "https://${AZURE_REPOS_HOST}/${AZURE_REPOS_ORG}",
      "auth": {
        "scheme": "basic",
        "token": "${BROKER_CLIENT_VALIDATION_BASIC_AUTH}"
      }
    },
    {
      "//": "create new PR in given repository",
      "method": "POST",
      "path": "/:owner/_apis/git/repositories/:repo/pullrequests",
      "origin": "https://${AZURE_REPOS_HOST}/${AZURE_REPOS_ORG}",
      "auth": {
        "scheme": "basic",
        "token": "${BROKER_CLIENT_VALIDATION_BASIC_AUTH}"
      }
    },
    {
      "//": "update existing PR in given repository",
      "method": "PATCH",
      "path": "/:owner/_apis/git/repositories/:repo/pullrequests/:pullRef",
      "origin": "https://${AZURE_REPOS_HOST}/${AZURE_REPOS_ORG}",
      "auth": {
        "scheme": "basic",
        "token": "${BROKER_CLIENT_VALIDATION_BASIC_AUTH}"
      }
    },
    {
      "//": "push new commit in given repository",
      "method": "POST",
      "path": "/:owner/_apis/git/repositories/:repo/pushes",
      "origin": "https://${AZURE_REPOS_HOST}/${AZURE_REPOS_ORG}",
      "auth": {
        "scheme": "basic",
        "token": "${BROKER_CLIENT_VALIDATION_BASIC_AUTH}"
      }
    },
    {
      "//": "used to redirect requests to snyk git client",
      "method": "any",
      "path": "/snykgit/*",
      "origin": "${GIT_CLIENT_URL}"
    }
  ]
}
```
