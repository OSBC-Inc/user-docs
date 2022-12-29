# Azure 서비스 프로비저닝

## 배경

Azure에 대한 다양한 Snyk Integration 지점을 이해하기 위해 몇 가지 지원 리소스를 배포하고 구성할 것입니다. 이 연습의 목표는 Snyk Workload를 보호하는 방법을 보여주는 것입니다. 학습 환경에서 사용하기 위한 기본 패턴을 제공합니다. Azure에 대해 자세히 알아보고 자세히 알아보려면 Microsoft의 [교육 모듈](https://docs.microsoft.com/en-us/learn/browse/?products=azure)을 참조하는 것이 좋습니다.

## ACR(Azure Container Registry) 배포

다음 예제는 CLI를 사용하여 ACR을 배포하기 위한 [Azure Quickstart](https://docs.microsoft.com/en-us/azure/container-registry/container-registry-get-started-azure-cli)를 기반으로 합니다. Azure CLI를 사용하여 Azure Container Registry 인스턴스를 배포한 다음 컨테이너 이미지에 태그를 지정하고 레지스트리에 푸시합니다.

### 리소스 그룹 만들기

배포하고 관리할 리소스를 논리적으로 구성하기 위해 [Azure 리소스 그룹](https://docs.microsoft.com/en-us/learn/modules/control-and-organize-with-azure-resource-manager/2-principles-of-resource-groups)을 만드는 것으로 시작합니다. 여기서는 리소스가 Azure에서 실행될 위치도 정의합니다. 이 경우에는 eastus 위치에 배포합니다. 터미널에서 다음 명령을 실행합니다:

```bash
az group create --name mySnykACRResourceGroup --location eastus
```

성공적으로 완료되면 다음과 유사한 출력이 표시됩니다:

```javascript
{
  "id": "/subscriptions/<guid>/resourceGroups/mySnykACRResourceGroup",
  "location": "eastus",
  "managedBy": null,
  "name": "mySnykACRResourceGroup",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null,
  "type": "Microsoft.Resources/resourceGroups"
}
```

아래 그림과 같이 Azure Portal에서 리소스 그룹 생성의 유효성을 검사할 수도 있습니다:

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/azure\_resource\_groups\_05.png)

### ACR 인스턴스 만들기

다음으로 최근에 만든 `mySnykACSResourceGroup`에 `mySnykContainerRegistry`라는 레지스트리를 만듭니다.

```bash
az acr create \
--resource-group mySnykACRResourceGroup \
--name mySnykContainerRegistry \
--sku Basic
```

배포가 완료되면 CLI는 레지스트리에 대한 세부 정보가 포함된 긴 JSON 응답을 반환합니다. 나중에 인증에 필요하므로 `loginServer` 값을 기록해 두는 것이 좋습니다.

```javascript
{- Finished ..
  "adminUserEnabled": false,
  "creationDate": "<timestamp>",
  "dataEndpointEnabled": false,
  "dataEndpointHostNames": [],
  "encryption": {
    "keyVaultProperties": null,
    "status": "disabled"
  },
  "id": "/subscriptions/<guid>/resourceGroups/mySnykACRResourceGroup/providers/Microsoft.ContainerRegistry/registries/mySnykContainerRegistry",
  "identity": null,
  "location": "eastus",
  "loginServer": "mysnykcontainerregistry.azurecr.io",
  "name": "mySnykContainerRegistry",
  "networkRuleSet": null,
  "policies": {
    "quarantinePolicy": {
      "status": "disabled"
    },
    "retentionPolicy": {
      "days": 7,
      "lastUpdatedTime": "<timestamp>",
      "status": "disabled"
    },
    "trustPolicy": {
      "status": "disabled",
      "type": "Notary"
    }
  },
  "privateEndpointConnections": [],
  "provisioningState": "Succeeded",
  "resourceGroup": "mySnykACRResourceGroup",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "status": null,
  "storageAccount": null,
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

Azure Portal 내에서 이를 볼 수도 있습니다:

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/azure\_resource\_groups\_06.png)

### 레지스트리에 로그인

`docker push` 또는 `docker pull`과 같은 작업을 수행하기 전에 레지스트리에 로그인해야 합니다. 이렇게 하려면 다음 명령을 실행합니다.

```bash
az acr login --name mySnykContainerRegistry
```

이 명령은 올바른 값을 제공한 경우 `Login Succeeded`를 반환합니다.
