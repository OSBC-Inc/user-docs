# 시작하기

## 배경

**Securing AKS with Snyk**에서 우리는 [매니페스트](https://kubernetes.io/docs/concepts/cluster-administration/manage-deployment/) 템플릿을 사용하여 Microsoft AKS(Azure Kubernetes Service)에서 실행되는 Kubernetes 클러스터에 애플리케이션을 신속하게 배포하는 방법을 배웠습니다. 그런 다음 **Securing ACS with Snyk**에서 Dockerfile을 사용하여 컨테이너 이미지를 빌드하고 나중에 사용할 수 있도록 ACR에 안전하게 저장하는 방법을 배웠습니다. 이를 통해 우리가 사용할 리소스와 해당 리소스를 사용할 위치를 정의할 수 있으므로 애플리케이션에 대한 더 많은 가시성과 제어가 가능했습니다. 그러나 Snyk에서 스캔한 컨테이너 이미지를 조사했을 때 다음 경고를 발견했습니다:

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk\_scan\_06.png)

이 모듈에서는 컨테이너 이미지 빌드에 대한 모범 사례를 확장합니다. 우리는 Snyk를 활용하여 Kubernetes 클러스터를 보호하고 ACR과 같은 개인 레지스트리를 스캔하는 방법을 가르친 이전 모듈을 기반으로 구축할 것입니다. 전체 워크플로의 포괄적인 보안을 제공하기 위해 소스 코드 관리 시스템 보안에 대한 규범적 지침을 제공합니다.

## Azure DevOps CLI

**Microsoft Azure** 시리즈의 기본 **시작하기** 섹션에서 Azure CLI 설정에 대해 다루었습니다. 이제 Azure CLI용 Azure DevOps 확장을 추가하여 보다 간소화된 방식으로 작업할 수 있습니다.

터미널에서 다음 명령을 실행합니다:

```bash
az extension add --name azure-devops
```

성공적으로 설치되었다는 확인 메시지가 표시되어야 합니다. 다음으로 [Azure DevOps 계정](https://azure.microsoft.com/en-us/services/devops/)을 만든 후 조직이 있어야 합니다. [Azure DevOps 포털](https://aex.dev.azure.com/)에서 찾을 수 있는 위치는 다음 사진을 참조하세요.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/azure\_devops\_01.png)

자세한 지침은 [가입, Azure DevOps Quickstart에 로그인](https://docs.microsoft.com/en-us/azure/devops/user-guide/sign-up-invite-teammates?view=azure-devops)을 참조하세요. 조직은 `https://dev.azure.com/MyOrganizationName` 형식이어야 합니다. 이제 터미널에서 `az login`을 실행하여 터미널에 로그인하고 다음 명령을 실행하여 `organization` 값으로 CLI를 구성하겠습니다:

```bash
az devops configure --defaults organization=https://dev.azure.com/MyOrganizationName/
```

{% hint style="info" %}
`MyOrganizationName`을 올바른 값으로 대체해야 합니다.
{% endhint %}
