# 자체 호스팅된 git을 통해 Snyk Code (브로커 포함)

{% hint style="info" %}
이 기능은 현재 베타 버전입니다. 참여에 관심이 있으시다면 CSM에 문의하시기 바랍니다.
{% endhint %}

기본적으로 Snyk Code를 로컬 git 서버에 연결할 수 있습니다. 이를 통해 GitHub Enterprise 또는 BitBucket Server와 같은 자체 호스팅된 git 공급자를 사용하는 고객은 자사 코드에서 잠재적인 취약점을 찾고 우선 순위를 지정하고 수정할 수 있습니다.

## Snyk Code 액세스 구성 요소

* **Broker  server**: Snyk SaaS 백엔드에서 실행
* **Broker client**: 인프라에 배포된 [Docker image](https://hub.docker.com/r/snyk/broker/)입니다.
* **Code agent**: 인프라에 배포된 또 다른 [Docker image](https://hub.docker.com/r/snyk/code-agent/) 입니다. 참고: Code agent는 [Snyk Broker](https://docs.snyk.io/integrations/snyk-broker) v4.108.0 이상의 버전에서만 지원됩니다. Broker client가 실행 중인 경우 최신 업데이트를 가져오십시오.

**Broker client** 및 **code agent** 구성 요소가 인프라에 배포되어 안전한 방식으로 로컬 저장소를 복제하고 관련 정보를 Snyk에 전송하는 두 개의 개별 서비스가 생성됩니다.

Broker client는 Agent에 연결 세부 정보를 제공합니다. Agent는 이러한 세부 정보를 사용하여 로컬 git 저장소에 연결하고 관련 파일을 복제합니다. 그리고 callback을 사용하여 중개된 통신을 통해 결과를 보냅니다. Broker client가 Broker ID를 사용하여 Snyk 환경에서 실행되는 Broker Server에 연결할 때 다음과 같은 중개된 통신이 발생합니다:

![](../../../.gitbook/assets/local-git.png)

자세한 내용은 [Snyk Broker](https://docs.snyk.io/integrations/snyk-broker/broker-introduction) 설명서를 참조하십시오.

## 설정

### 전제 조건

설치 프로세스를 시작하기 전에 Broker client 및 Code agent를 실행하기 위한 최소 요구 사항을 지원하는 서버가 있는지 확인하십시오:

* CPU: 1개의 가상 CPU
* 메모리: 2Gb (노드 메모리 설정에 반영되어야 함)
* 디스크 공간: 2Gb (사용 가능한 디스크 크기에 따라 복제 가능한 최대 저장소 크기가 결정됨)
* 네트워크: 코드 업로드 성능은 느린 인터넷 연결의 영향을 받습니다.

### **Broker client** 설정

Code agent는 broker client에 종속됩니다. 특정 SCM에 대한 broker를 설정하는 방법에 대한 자세한 내용은 [How to install and configure your Snyk Broker client](../../../features/integrations/snyk-broker/how-to-install-and-configure-your-snyk-broker-client.md)에 대한 지침을 따르십시오.

이미 실행 중인 broker client가 있는 경우 다음 추가 요구 사항을 고려하십시오:

* Code agent는 [Snyk Broker](https://docs.snyk.io/integrations/snyk-broker) v4.108.0 이상 버전에서만 지원되므로 최신 버전을 먼저 가져와야 합니다.
* Code agent에 전체 저장소를 복제할 수 있는 권한이 필요합니다. broker에 전달된 SCM 토큰에 해당 권한이 있는지 확인하십시오.

### 네트워크 설정

broker client와 broker agent를 모두 실행하려면 둘 사이에 네트워크 연결을 설정해야 합니다. 원하는 경우 Ngrok와 같은 도구를 사용하여 하나의 컨테이너 연결을 노출할 수 있지만 이 설명은 도커 브리지 네트워크에 초점을 맞추고 있습니다.

**`docker network create <network>`** 실행

예를 들어:

```
docker network create mySnykBrokerNetwork
```

**`docker network ls`**를 실행하여 생성되었음을 확인할 수 있으며, 다음과 같은 결과가 표시됩니다:

```
  NETWORK ID     NAME                 DRIVER     SCOPE
  d1353a2b0f66   mySnykBrokerNetwork  bridge     local
```

### Code Agent 설정

먼저 code agent 이미지를 가져옵니다:

```
docker pull snyk/code-agent
```

code agent를 구성하려면 다음 환경 변수가 필요합니다:

* **SNYK\_TOKEN -** CLI에서 사용하는 snyk token을 참조하십시오. 자세한 내용은 [Authenticate the CLI with your account](../../../features/snyk-cli/install-the-snyk-cli/authenticate-the-cli-with-your-account.md#authenticate-using-your-api-token)을 참조하십시오.
* **PORT** - code agent가 연결을 허용하는 로컬 포트이며, 기본값은 3000입니다.

**code-agent**를 실행하려면**:**

```
docker run --name code-agent \
     -p 3000:3000 \
     -e PORT=3000 -e SNYK_TOKEN=<token> --network mySnykBrokerNetwork \
     snyk/code-agent
```

이 예에서는 다음을 수행합니다:

* We set the current container to use the new network we created **--network mySnykBrokerNetwork**
* We gave the current container a name **--name code-agent**. It will be used to define the **GIT\_CLIENT\_URL** for the broker client that we will run next.

### Broker 설정 확장

Extend your broker setup with the following arguments:

```
-e GIT_CLIENT_URL=http://<code agent container>:<code agent port>
--network <name of created network>
```

For example, to extend an existing broker client configured for Gitlab, run:

```
docker run \
   -p 8001:8000 \
   -e BROKER_TOKEN= \
   -e GITLAB_TOKEN= \
   -e GITLAB= \
   -e PORT=8000 \
   -e GIT_CLIENT_URL=http://code-agent:3000 \
   --network mySnykBrokerNetwork \
   snyk/broker:gitlab
```

In this example:

* We set the current container to use the new network we created **--network mySnykBrokerNetwork**
* In **GIT\_CLIENT\_URL** we used the name we defined in the code-agent container as the host here.

If you have a running Snyk broker with a custom whitelist (**accept.json**), then ensure the following rule is present in the whitelist:

```
{
  "//": "used to redirect requests to snyk git client",
  "method": "any",
  "path": "/snykgit/*",
  "origin": "${GIT_CLIENT_URL}"
}
```

(The rule is present by default, so only needed if you override the rule with a custom whitelist.)

## 고급 설정

### 스니펫 코드 활성화

To enable code snippets, additional rules must be added to **accept.json**.

See [https://github.com/snyk/broker#custom-approved-listing-filter](https://github.com/snyk/broker#custom-approved-listing-filter) for detailed instructions how to extend **accept.json**.

For GitHub:

```
{
  "//": "needed to load code snippets",
  "method": "GET",
  "path": "/repos/:name/:repo/contents/:path",
  "origin": "https://${GITHUB_TOKEN}@${GITHUB_API}"
}
```

For Gitlab:

```
{
  "//": "needed to load code snippets",
  "method": "GET",
  "path": "/api/v4/projects/:project/repository/files/:path",
  "origin": "https://${GITLAB}"
}
```

For BitBucket Server:

```
{
    "//": "needed to load code snippets",
      "method": "GET",
      "path": "/projects/:project/repos/:repo/browse*/:file",
      "origin": "https://${BITBUCKET_API}",
      "auth": {
        "scheme": "basic",
        "username": "${BITBUCKET_USERNAME}",
        "password": "${BITBUCKET_PASSWORD}"
      }
}
```

For Azure Repos:

```
{
      "//": "needed for code snippets",
      "method": "GET",
      "path": "/:owner/_apis/git/repositories/:repo/items",
      "origin": "https://${AZURE_REPOS_HOST}/${AZURE_REPOS_ORG}",
      "auth": {
        "scheme": "basic",
        "token": "${BROKER_CLIENT_VALIDATION_BASIC_AUTH}"
      }
}
```

{% hint style="info" %}
After these snippets are added, all content from the repository can be accessed through Snyk broker.
{% endhint %}

### 프록시 지원

For instructions how to run Broker client through a proxy, see [https://github.com/snyk/broker](https://github.com/snyk/broker). Make sure that requests to the Code agent are not sent through the proxy, by passing `NO_PROXY=<code agent container>`, for example:

```
-e HTTP_PROXY=http://my.proxy.address:8080
-e HTTPS_PROXY=http://my.proxy.address:8080
-e NO_PROXY=code-agent
```

For code agent, add the following environment variables to the **docker run** command:

```
-e HTTP_PROXY=http://my.proxy.address:8080
-e HTTPS_PROXY=http://my.proxy.address:8080
```

To disable certificate verification, e.g., in the case of self-signed certificates, add to the code-agent **docker run** command:

```
-e NODE_TLS_REJECT_UNAUTHORIZED=0
```
