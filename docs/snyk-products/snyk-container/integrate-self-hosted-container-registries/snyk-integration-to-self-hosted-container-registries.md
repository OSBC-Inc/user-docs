# 자체 호스팅된 컨테이너 레지스트리에 대한 Snyk 통합

{% hint style="info" %}
**기능 사용 여부**\
이 기능은 Enterprise 플랜에서 사용할 수 있습니다. 자세한 내용은 [pricing plans](https://snyk.io/plans/)를 참조하십시오.
{% endhint %}

Snyk은 호스팅하는 개인 컨테이너 레지스트리에 통합할 수 있으며 해당 레지스트리 컨테이너 이미지를 더 잘 보호할 수 있습니다.

{% hint style="warning" %}
이 기능이 작동하려면 인프라에 두 개의 별도 컨테이너를 배포하여 두 개의 개별 서비스를 생성해야 합니다.
{% endhint %}

{% hint style="info" %}
호스팅된 컨테이너 레지스트리를 활성화하고 구성하려면 [Support team에 문의하십시오.](https://support.snyk.io/hc/en-us/requests/new)
{% endhint %}

## 소개

개인 컨테이너 레지스트리와 통합하면 다음을 수행할 수 있습니다.

* 액세스 토큰과 같은 중요한 데이터를 사설 네트워크에 보관하고 해당 정보를 Snyk과 공유하지 않습니다.
* Snyk에서 네트워크에 대한 제어된 액세스를 제공하여 Snyk 액세스와 Snyk에서 수행할 수 있는 작업을 제한합니다.

## 자체 호스팅 컨테이너 레지스트리 솔루션 구성 요소

* Broker Server: Snyk SaaS backend에서 실행
* Broker Client & Container Registry Agent: 인프라에 배포된 두 개의 Docker 이미지가 두 개의 개별 서비스를 생성하여 안전한 방식으로 컨테이너 레지스트리를 샘플링하고 허용된 정보를 Snyk에 보내는 역할을 합니다.

Broker Client는 Agent에 연결 세부 정보를 제공합니다. Agent는 이러한 세부 정보를 사용하여 컨테이너 레지스트리에 연결하고 이미지를 스캔하고 콜백을 사용하여 중개된 통신을 통해 스캔 결과를 보냅니다. Broker Client가 Broker ID를 사용하여 Snyk 환경에서 실행되는 Broker Server에 연결할 때 중개된 통신이 발생합니다. 자세한 내용은 [Snyk Broker](https://docs.snyk.io/integrations/snyk-broker) 설명서를 참조하십시오.

![](../../../.gitbook/assets/mceclip0-8-.png)

#### 지원되는 컨테이너 레지스트리

* Artifactory (type: artifactory-cr)
* Harbor (type: harbor-cr)
* Azure (type: acr)
* GCR (type: gcr)
* ECR (type: ecr)
* Google Artifact Registry (type: google-artifact-cr)
* Docker Hub (type: docker-hub)
* Quay (type: quay-cr)
* Nexus (type: nexus-cr)
* GitHub (type: github-cr)
* DigitalOcean (type: digitalocean-cr)
* GitLab (type: gitlab-cr)

{% hint style="info" %}
**Note**\
위 목록의 오픈소스 컨테이너 레지스트리가 있는 broker를 사용하는 통합 패턴은 Snyk service\*\*.\*\*가 내부가 아닌 자체 환경에서 이미지를 스캔해야 하는 사용자를 위해 설계되었습니다.\
이러한 요구사항이 귀사와 관련이 없는 경우 이 문서에서 설명하는 아키텍처는 필요하지 않으며 Integration 페이지에서 표준 방식으로 통합할 수 있습니다.
{% endhint %}

#### 설정 전제 조건

* Broker Client 시스템 요구 사항: 1 CPU, 256MB RAM.
* Container Registry Agent 시스템 요구 사항은 다음과 같아야 합니다.(MAX\_ACTIVE\_OPERATIONS=1 제공)
  * CPU: 1 vcpu
  * Memory: 2Gb(노드 메모리 설정에 반영되어야 함)
  * Storage: 5Gb
* Docker Hub에서 components images를 가져오도록 구성된 Docker
* Broker와 Agent 간의 연결
* Broker Client 이미지는 [여기](https://hub.docker.com/r/snyk/broker/tags?page=1\&ordering=last\_updated\&name=container-registry-agent)에서 다운로드할 수 있습니다.
* Container Registry Agent 이미지는 [여기](https://hub.docker.com/r/snyk/container-registry-agent/tags?page=1\&ordering=last\_updated)에서 다운로드할 수 있습니다.

{% hint style="info" %}
**Scaling을 통한 스캔 용량 조절**

위와 같이 vCPU 1개와 RAM 2GB를 사용할 경우, 스캔 용량은 한 번에 최대 350MB의 약 160개 이미지입니다. 이미지 크기에 따라 이 기능을 확장할 수 있으며, 확장이 허용되지 않거나 제한에 맞지 않는 사용 사례가 있는 경우 지원 팀에 문의하십시오.
{% endhint %}

## 원격 연결 설정

### Broker Client 실행

Broker Client 이미지는 위의 설정 전제 조건에 제공된 링크를 사용하여 Docker Hub에서 가져올 수 있습니다.

Broker Client를 구성하는 데 필요한 환경 변수는 다음과 같습니다.

{% hint style="info" %}
**참고**

**DigitalOcean**, **GCR**, **Google Artifact Registry** 및 **Artifactory**의 경우 몇가지 주의해야 할 값이 있습니다. **ECR**의 경우 추가 설정이 필요합니다. [Specifications](snyk-integration-to-self-hosted-container-registries.md#container-registry-specific-configurations)를 따르십시오.
{% endhint %}

* `BROKER_TOKEN` - 컨테이너 레지스트리 통합을 통해 얻은 Snyk Broker 토큰(Snyk Support에서 제공)
* `BROKER_CLIENT_URL` - Container Registry Agent가 중개된 연결을 통해 Snyk에 콜백하기 위해 사용하는 Broker Client의 URL(scheme 및 port 포함), 예: "[http://my.broker.client:8000](http://my.broker.client:8000)".
* `CR_AGENT_URL` - Broker Client가 requests를 라우팅할 Container Registry Agent의 URL, 예: "[http://my.container-registry-agent](http://my.container-registry-agent)".
* `CR_TYPE` - 지원되는 레지스트리에 나열된 컨테이너 레지스트리 유형, 예: "docker-hub", "gcr", "artifactory-cr".
* `CR_BASE` - 연결할 컨테이너 레지스트리 API의 hostname, 예: "cr.host.com".
* `CR_USERNAME` - 컨테이너 레지스트리 API에 인증하기 위한 사용자 이름
* `CR_PASSWORD` - 컨테이너 레지스트리 API에 인증하기 위한 비밀번호
* `CR_TOKEN` - DigitalOcean 컨테이너 레지스트리에 대한 인증 토큰
* `PORT` - Broker Client가 연결을 허용하는 로컬 포트, 기본값은 7341.

아래와 같이 Broker Client 컨테이너를 실행합니다.

```
docker run --restart=always \
       -p 8000:8000 \
       -e BROKER_TOKEN="<secret-broker-token>" \
       -e BROKER_CLIENT_URL="<broker-client-url>" \
       -e CR_AGENT_URL="<container-registry-agent-url>" \
       -e CR_TYPE="<container-registry-type>" \
       -e CR_BASE="<container-registry-hostname>" \
       -e CR_USERNAME="<username>" \
       -e CR_PASSWORD="<password>" \
       -e PORT=8000 \
       snyk/broker:container-registry-agent
```

### Container Registry Agent 실행

Container Registry Agent 이미지는 위의 설정 전제 조건에서 제공된 링크를 사용하여 Docker Hub에서 가져올 수 있습니다. 이미지를 실행하려면 단일 환경 변수를 사용하여 포트를 지정할 수 있습니다.

```
docker run --restart=always \
       -p 8081:8081 \
       -e SNYK_PORT=8081 \
       snyk/container-registry-agent:latest
```

### 컨테이너 레지스트리별 구성

다음 컨테이너 레지스트리에는 특정 환경 변수 및/또는 설정이 필요합니다.

#### **DigitalOcean**

**DigitalOcean**용 Broker Client를 설정하는 데 `CR_USERNAME`과 `CR_PASSWORD`가 필요하지 않습니다. 대신 DigitalOcean 컨테이너 레지스트리에 대한 인증 토큰을 지정해야 합니다.(`CR_TOKEN`)

#### **GCR** 및 **Google Artifact Registry**

이러한 컨테이너 레지스트리에 대해 Broker Client를 설정하려면 위의 모든 사항이 적용됩니다. 주목해야 할 유일한 점은 `CR_USERNAME` 값은 영구적이며 `_json_key` 값이어야 하며 `CR_PASSWORD`는 google 인증에 사용되는 JSON key여야 합니다.

#### **Artifactory**

**Repository path**를 Docker 액세스 방법으로 사용하는 경우 CR\_BASE 변수의 컨테이너 레지스트리 hostname을 다음 구조로 설정해야 합니다. \*\*\*\* `<your artifactory host>/artifactory/api/docker/<artifactory-repo-name>`

#### **ECR**

![중개된 ECR 통합의 상위 수준 아키텍처](<../../../.gitbook/assets/untitled (1).png>)

**필수 AWS 리소스**

ECR을 설정하려면 두 가지 종류의 IAM 리소스를 만들어야 합니다.

* Container Registry Agent IAM Role / IAM User: 컨테이너 레지스트리 에이전트가 ECR에 대한 액세스 권한이 있는 교차 계정 역할을 가정하는 데 사용하는 IAM Role / IAM User입니다. 다음과 같은 권한이 있어야 합니다. `"sts:AssumeRole"`
*   Snyk ECR Service Role: ECR에 대한 액세스 권한이 있는 IAM Role. 컨테이너 레지스트리 에이전트 IAM Role / IAM User가 ECR에 대한 읽기 전용 액세스 권한을 얻는 것으로 가정합니다.\
    다음 권한이 있어야 합니다.

    ```
    [
      "ecr:GetLifecyclePolicyPreview",
      "ecr:GetDownloadUrlForLayer",
      "ecr:BatchGetImage",
      "ecr:DescribeImages",
      "ecr:GetAuthorizationToken",
      "ecr:DescribeRepositories",
      "ecr:ListTagsForResource",
      "ecr:ListImages",
      "ecr:BatchCheckLayerAvailability",
      "ecr:GetRepositoryPolicy",
      "ecr:GetLifecyclePolicy"
    ]
    ```

**ECR 설정 단계**

단일 Container Registry Agent 인스턴스가 다른 계정에 있는 ECR 저장소에 액세스할 수 있도록 위의 리소스를 다음과 같이 사용할 수 있습니다.

1.  **(한 번만 실행하는 단계)** Container Registry Agent IAM Role / IAM User를 만들어 Container Registry Agent를 실행하는 데 사용합니다. [여기](https://docs.aws.amazon.com/sdk-for-javascript/v2/developer-guide/setting-credentials-node.html)에 설명된 방법 중 하나를 사용하여 IAM Role / IAM User를 Container Registry Agent에 제공할 수 있습니다.

    **각 ECR 계정에 대해 별도의 broker 인스턴스를 사용하여 각 ECR 계정에 대해 다음 단계를 실행합니다.**
2. ECR이 있는 AWS 계정에서 ECR에 대한 읽기 액세스 권한을 가진 Snyk ECR Service Role을 만들고 이전 단계에서 만든 특정 Container Registry Agent IAM Role / IAM User만 이 역할을 맡을 수 있도록 trust relationship을 편집합니다.
3. Container Registry Agent IAM Role / IAM User이 Snyk ECR Service Role(s)만 맡을 수 있도록 제한합니다.
4. Broker Client에 ECR 영역과 함께 Snyk ECR Service Role의 Role ARN을 제공합니다. Broker Client는 이 Role ARN을 Container Registry Agent로 전달하고 Container Registry Agent는 이를 인수하여 ECR에 액세스합니다. 다음과 같은 환경 변수가 필요합니다.
   * CR\_ROLE\_ARN=\<SnykEcrServiceRole의 ARN 역할>
   * CR\_REGION=\<ECR의 AWS 지역>
   * CR\_EXTERNAL\_ID=<선택 사항, trust relationship 조건에서 찾은 외부 ID>

중개된 ECR 설정에 대한 자세한 내용을 보려면 [여기](setting-up-the-container-registry-agent-for-a-brokered-ecr-integration.md)를 클릭하십시오.

## 시스템 구성 및 사용 검사

`/systemcheck` endpoint를 사용하여 Broker Client, Container Registry Agent 및 Container Registry 간의 연결을 확인할 수 있습니다.

이를 사용하기 위해 다음 환경 변수를 Broker Client에 제공합니다.\
`BROKER_CLIENT_VALIDATION_URL=<agent-url>/systemcheck`

브로커 클라이언트의 `/systemcheck` endpoint를 호출하면 브로커 클라이언트에 제공된 인증 정보로 `BROKER_CLIENT_VALIDATION_URL`을 사용하여 `/systemcheck` endpoint 컨테이너 레지스트리 에이전트에 요청을 합니다. 그러면 Container Registry Agent가 컨테이너 레지스트리에 request를 생성하여 연결을 확인할 것입니다.

{% hint style="info" %}
**Note**\
중개된 통합이 작동하려면 /systemcheck endpoint가 **반드시 필요한 것은 아닙니다.** 자세한 내용은 다음 웹사이트에서 확인할 수 있습니다. [https://github.com/snyk/broker#systemcheck](https://github.com/snyk/broker#systemcheck)
{% endhint %}

## 디버깅 방법

`LOG_LEVEL` 환경 변수를 원하는 수준(debug/info/warn/error)으로 설정하여 Container Registry Agent 및 Broker Client 로그의 수준을 변경할 수 있습니다.

자세한 디버깅을 위해 `DEBUG=*` 환경 변수를 사용하여 Container Registry Agent를 실행할 수 있습니다. 이렇게 하면 Node [Debug](https://www.npmjs.com/package/debug) package의 로그를 출력할 수 있습니다. Debug package Container Registry Agent의 여러 package에 사용되며, 그 중에는 HTTP requests를 만드는 데 사용되는 [Needle](https://www.npmjs.com/package/needle) package가 있습니다. `DEBUG=needle`를 설정하여 Needle에서만 디버그 로그를 출력할 수 있습니다.

{% hint style="danger" %}
**경고**\
프로덕션 환경에서는 타사 도구의 디버깅 옵션을 사용하지 않는 것이 좋습니다. Snyk에서 유지 관리하지 않는 중요한 정보가 로그에 기록될 수 있기 때문입니다. 예를 들어 HTTP requests의 헤더 정보가 있습니다.
{% endhint %}

**이미지 보안**

이제 개인 저장소에서 직접 컨테이너 이미지 스캔을 시작할 수 있습니다. 자세한 내용은 [컨테이너 레지스트리에서 이미지 스캔](https://docs.snyk.io/snyk-container/jfrog-artifactory-image-scanning/configuring-your-jfrog-artifactory-container-registry-integration)(Artifactory 예시)를 참조하십시오.
