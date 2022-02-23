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

* Broker server: Snyk SaaS backend에서 실행
* Broker client & Container Registry Agent: 인프라에 배포된 두 개의 Docker 이미지가 두 개의 개별 서비스를 생성하여 안전한 방식으로 컨테이너 레지스트리를 샘플링하고 허용된 정보를 Snyk에 보내는 역할을 합니다.

Broker client는 Agent에 연결 세부 정보를 제공합니다. Agent는 이러한 세부 정보를 사용하여 컨테이너 레지스트리에 연결하고 이미지를 스캔하고 콜백을 사용하여 중개된 통신을 통해 스캔 결과를 보냅니다. Broker client가 Broker ID를 사용하여 Snyk 환경에서 실행되는 Broker server에 연결할 때 중개된 통신이 발생합니다. 자세한 내용은 [Snyk Broker](https://docs.snyk.io/integrations/snyk-broker) 설명서를 참조하십시오.

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
The integration pattern using broker with open source container registries from the above list is designed for users who require images to be scanned in their own environment, instead of inside the Snyk service\*\*.\*\*\
If such a requirement is not relevant for you, you do not need the architecture described in this article, and can integrate to it in the standard way from the integrations page.
{% endhint %}

#### 설정 전제 조건

* Broker Client machine system requirements: 1 CPU, 256MB of RAM.
* Container registry agent machine system requirements should be (given MAX\_ACTIVE\_OPERATIONS=1):
  * CPU: 1 vcpu
  * Memory: 2Gb (should be reflected in node memory setting)
  * Storage: 5Gb
* Docker configured to pull components images from Docker Hub
* Connection between broker and agent
* Broker Client image can be found for download [here](https://hub.docker.com/r/snyk/broker/tags?page=1\&ordering=last\_updated\&name=container-registry-agent)
* Container Registry Agent image can be found for download [here](https://hub.docker.com/r/snyk/container-registry-agent/tags?page=1\&ordering=last\_updated)

{% hint style="info" %}
**Scaling to adjust scan capacity**

With the above configuration of 1 vCPU and 2GB RAM, scanning capacity would be approximately 160 images of \~350MB in one go. You can scale this up based on your image sizes, and in case you have a specific use case that doesn't allow scaling and doesn't fit the limitations, please contact our support team.
{% endhint %}

## 원격 연결 설정

### broker client 실행

The Broker Client image can be pulled from Docker Hub using the link provided above in the settings prerequisites.

There are different environment variable that are required to configure the Broker Client:

{% hint style="info" %}
**Note:**

For **DigitalOcean**, **GCR**, **Google Artifact Registry** and **Artifactory**, there are a few values to notice. For **ECR**, additional setup is required. [Specifications](snyk-integration-to-self-hosted-container-registries.md#container-registry-specific-configurations) to follow.
{% endhint %}

* `BROKER_TOKEN` - The Snyk Broker token, obtained from your Container registry integration (provided by Snyk support).
* `BROKER_CLIENT_URL` - The URL of your broker client (including scheme and port) used by the container registry agent to call back to Snyk through the brokered connection, for example: "[http://my.broker.client:8000](http://my.broker.client:8000)".
* `CR_AGENT_URL` - The URL of your container registry agent, to which the broker client will route the requests, for example: "[http://my.container-registry-agent](http://my.container-registry-agent)".
* `CR_TYPE` - The container registry type as listed in supporter registries, for example: "docker-hub", "gcr", "artifactory-cr".
* `CR_BASE` - The hostname of the container registry api to connect to, for example: "cr.host.com".
* `CR_USERNAME` - The username for authenticating to container registry api.
* `CR_PASSWORD` - The password for authenticating to container registry api.
* `CR_TOKEN` - Authentication token for DigitalOcean container registry.
* `PORT` - The local port at which the Broker client accepts connections. Default is 7341.

Run the broker client container with relevant configuration:

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

### 컨테이너 레지스트리 에이전트 실행

The Container Registry Agent image can be pulled from Docker Hub using the link provided above in the settings prerequisites. To run the image you can use a single environment variable for specifying the port:

```
docker run --restart=always \
       -p 8081:8081 \
       -e SNYK_PORT=8081 \
       snyk/container-registry-agent:latest
```

### 컨테이너 레지스트리별 구성

The following container Registries require specific environment variables and/or setup.

#### **DigitalOcean**

To set up Broker Client for **DigitalOcean**,`CR_USERNAME` and `CR_PASSWORD` are not required. Instead, you need to specify `CR_TOKEN` - authentication token for DigitalOcean container registry.

#### **GCR and Google Artifact Registry**

To set up the Broker Client for those container registries, all the above applies. The only thing to note is that `CR_USERNAME` value is permanent and should be `_json_key`, and the `CR_PASSWORD` value should be the JSON key used to authenticate to google.

#### **Artifactory**

In case you are using **Repository path** as your Docker access method, the container registry hostname in `CR_BASE` variable should be set in this structure: \*\*\*\* `<your artifactory host>/artifactory/api/docker/<artifactory-repo-name>`

#### **ECR**

![A high-level architecture of the brokered ECR integration](<../../../.gitbook/assets/untitled (1).png>)

**Required AWS Resource**

ECR setup requires two kinds of IAM resources to be created:

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
