# ACR Integration 구성

## 서비스 주체 만들기

레지스트리에 [서비스 주체](https://docs.microsoft.com/en-us/azure/active-directory/develop/app-objects-and-service-principals)를 할당하는 것이 좋습니다. 이 항목에 대한 자세한 내용은 [Azure 컨테이너 레지스트리로 인증](https://docs.microsoft.com/en-us/azure/container-registry/container-registry-authentication) 설명서를 검토하세요.

이 프로세스를 단순화하기 위해 복제된 저장소의 `scripts/` 디렉토리에서 샘플 `bash` 스크립트를 찾을 수 있습니다. 터미널에서 `pwd`를 입력하고 결과에 `$HOME/snyk-azure-resources/`가 표시되는지 확인하여 복제된 저장소의 루트에 있는지 확인합니다.

그런 다음 다음 명령을 입력하여 디렉토리를 변경해 보겠습니다:

```bash
cd scripts/
```

여기에서 간단한 `ls -a` 명령이 내용을 표시하고 해당 디렉토리에서 `create-acr-service-principal.sh` 스크립트를 볼 수 있습니다. [Microsoft Visual Studio Code](https://code.visualstudio.com/)와 같은 선호하는 편집기에서 이 파일을 열고 내용을 검토할 수 있습니다.

다음과 같이 표시됩니다:

```bash
#!/bin/bash

# Modify for your environment.
# ACR_NAME: The name of your Azure Container Registry
# SERVICE_PRINCIPAL_NAME: Must be unique within your AD tenant
ACR_NAME=${1}
SERVICE_PRINCIPAL_NAME=acr-service-principal

# Obtain the full registry ID for subsequent command args
ACR_REGISTRY_ID=$(az acr show --name $ACR_NAME --query id --output tsv)

# Create the service principal with rights scoped to the registry.
# Default permissions are for docker pull access. Modify the '--role'
# argument value as desired:
# acrpull:     pull only
# acrpush:     push and pull
# owner:       push, pull, and assign roles
SP_PASSWD=$(az ad sp create-for-rbac --name http://$SERVICE_PRINCIPAL_NAME --scopes $ACR_REGISTRY_ID --role acrpull --query password --output tsv)
SP_APP_ID=$(az ad sp show --id http://$SERVICE_PRINCIPAL_NAME --query appId --output tsv)

# Output the service principal's credentials; use these in your services and
# applications to authenticate to the container registry.
echo "Service principal ID: $SP_APP_ID"
echo "Service principal password: $SP_PASSWD"
```

스크립트를 실행하려면 현재 작업 디렉터리에서 스크립트를 호출하고 다음과 같이 ACR 이름 `mysnykcontainerregistry`를 매개 변수로 전달합니다:

```bash
./create-acr-service-principal.sh mysnykcontainerregistry
```

성공적으로 완료되면 다음과 유사한 결과가 표시됩니다:

```
Creating a role assignment under the scope of "/subscriptions/<guid>/resourceGroups/mySnykACRResourceGroup/providers/Microsoft.ContainerRegistry/registries/mySnykContainerRegistry"
  Retrying role assignment creation: 1/36
Service principal ID: <guid>
Service principal password: <guid>
```

Take note of the values for `Service principal ID` and `Service principal password`. You will need these to configure the integration in the following steps so **DO NOT** close or clear your terminal window.

`Service principal` ID 및 `Service principal` 암호 값을 기록해 둡니다. 다음 단계에서 Integration을 구성하려면 이것이 필요하므로 터미널 창을 닫거나 **지우지 마십시오**.

## Integration 활성화

Snyk 웹 콘솔에서 `Integrations`로 이동합니다. `ACR`을 검색하고 선택합니다. 타일을 클릭합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk\_integrations\_07.png)

다음 다이어그램에 설명된 단계를 따르고 ACR 인스턴스에 대한 `Service principal` ID `Service principal` 암호 및 `loginServer` 값을 제공합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk\_integrations\_06.png)

설정을 저장하는 것을 잊지 마십시오!
