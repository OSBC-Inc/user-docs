# 자체 호스팅된 컨테이너 레지스트리에 대한 Snyk 통합

{% hint style="info" %}
**Feature availability**\
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
**참고**\
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
**Scaling to adjust scan capacity**

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

![A high-level architecture of the brokered ECR integration](<../../../.gitbook/assets/untitled (1).png>)

**필수 AWS 리소스**

ECR을 설정하려면 두 가지 종류의 IAM 리소스를 만들어야 합니다.

* Container Registry Agent IAM Role / IAM User: an IAM Role / IAM User the Container Registry Agent uses to assume a cross-account role with access to ECR. It should have the following permissions: `"sts:AssumeRole"`
*   Snyk ECR Service Role: an IAM Role with access to ECR which is assumed by the Container Registry Agent IAM Role / IAM User to gain read-only access to ECR.\
    It should have the following permissions:

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

**Setup steps for ECR**

The above resources can be used as follows, so that a single Container Registry Agent instance can access ECR repositories located in different accounts\*\*:\*\*

1.  **(Run this step once only)** Create the Container Registry Agent IAM Role / IAM User and use it to run the Container Registry Agent. The IAM Role / IAM User could be provided to the Container Registry Agent using one of the methods described [here](https://docs.aws.amazon.com/sdk-for-javascript/v2/developer-guide/setting-credentials-node.html).

    **Run the following steps for each of your ECR accounts, using a separate broker instance for each ECR account:**
2. In the AWS account where your ECR reside, create the Snyk ECR Service Role with read access to your ECR, and edit the trust relationship to allow this role to be assumed only by the specific Container Registry Agent IAM Role / IAM User created in the previous step.
3. Restrict the Container Registry Agent IAM Role / IAM User to only be allowed to assume the your Snyk ECR Service Role(s).
4. Provide the Broker Client with the Role ARN of the Snyk ECR Service Role together with the ECR region. The Broker Client passes this Role ARN to the Container Registry Agent, and the Container Registry Agent will assume it, to access your ECR. The following environment variables are needed:
   * CR\_ROLE\_ARN=\<the role ARN of SnykEcrServiceRole>
   * CR\_REGION=\<AWS Region of ECR>
   * CR\_EXTERNAL\_ID=\<Optional. An external ID found in the trust relationship condition>

For detailed information about the brokered ECR setup, click [here](setting-up-the-container-registry-agent-for-a-brokered-ecr-integration.md).

## 시스템 구성 및 사용 검사

You can use the `/systemcheck` endpoint to verify connectivity between the Broker Client, the Container Registry Agent, and your container registry.

In order to use it, provide the following environment variable to the broker client:\
`BROKER_CLIENT_VALIDATION_URL=<agent-url>/systemcheck`

When calling the `/systemcheck` endpoint of the broker client, it will use the `BROKER_CLIENT_VALIDATION_URL` to make a request to the `/systemcheck` endpoint Container Registry Agent's, with the credentials provided to the broker client. The Container Registry Agent will then make a request to the container registry to validate connectivity.

{% hint style="info" %}
**Note:**\
The /systemcheck endpoint is **not mandatory** for the brokered integration to function. More information can be found here: [https://github.com/snyk/broker#systemcheck](https://github.com/snyk/broker#systemcheck)
{% endhint %}

## 디버깅 방법

The `LOG_LEVEL` environment variable can be set to the desired level (debug/info/warn/error), in order to change the level of the Container Registry Agent and Broker Client logs.

For more verbose debugging, the Container Registry Agent can be run with the `DEBUG=*` environment variable. This allows printing the logs of the Node [Debug](https://www.npmjs.com/package/debug) package. The Debug package is used by several packages in the Container Registry Agent, among them is the [Needle](https://www.npmjs.com/package/needle) package, which is used for making HTTP requests. Printing debug logs specifically from Needle can be done by setting `DEBUG=needle`.

{% hint style="danger" %}
**Warning:**\
Using the debugging options of third-party tools is not recommended for production environments, as it may result in logging sensitive information in logs that are not maintained by Snyk. For example, header information of HTTP requests.
{% endhint %}

**Secure your images:**

You can now start scanning your container images directly from your private registry. See [scanning images from container registry](https://docs.snyk.io/snyk-container/jfrog-artifactory-image-scanning/configuring-your-jfrog-artifactory-container-registry-integration) (Artifactory example) for more details.
