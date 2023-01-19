# Azure Functions 개요

Snyk의 Azure Function Apps 통합으로 node.js, .Net 및 Java Azure Function Apps의 배포된 코드를 모니터링하여 애플리케이션의 디펜던시에서 발견되는 알려진 취약점을 제어하고 설정한 빈도로 테스트할 수 있습니다.

각 테스트마다 Snyk은 Azure와 직접 통신하여 현재 어떤 코드가 배포되고 어떤 디펜던시가 사용되고 있는지 정확히 파악합니다. 각 디펜던시는 Snyk의 취약점 데이터베이스에 대해 테스트되어 알려진 취약점이 있는지 확인합니다.

취약점이 발견되면 즉시 조치를 취할 수 있도록 이메일 또는 슬랙을 통해 경고를 받게 됩니다.

Azure Function Apps 통합을 설정하려면 다음 작업을 수행해야 합니다.

1. 통합 페이지에서 Azure에 연결
2. Snyk에 Azure 계정 인증 정보 추가
3. 모니터링할 프로젝트를 선택하고 "**Add to Snyk**"을 클릭합니다.

## Snyk을 **Azure Functions**에 연결

Snyk이 배포된 Azure Function 앱을 모니터링하려면 Snyk을 Azure 계정에 연결해야 합니다.

이렇게 하려면 [Integrations 페이지](https://app.snyk.io/integrations)에서 Serverless로 이동하고 Azure Functions를 클릭합니다.

![](<../../../.gitbook/assets/Screenshot 2021-10-27 at 09.36.33.png>)

다음으로 Azure 서비스 주체 인증 정보를 입력하라는 메시지가 표시되는 페이지로 이동합니다.

![](<../../../.gitbook/assets/image (29).png>)

Azure 서비스 주체 인증 정보를 생성하고 찾는 방법은 다음과 같습니다.

## **Azure** 서비스 주체 생성

Snyk에게 Azure 계정에 대한 액세스 권한을 부여하려면 유효한 서비스 주체가 필요합니다.

Snyk에서 사용할 서비스 주체를 생성하려면 [Azure 포탈](https://portal.azure.com) 또는 [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)을 사용하면 됩니다.

Azure CLI 2.0을 설치한 후에는 `az` 명령에 액세스할 수 있습니다. 다음을 사용하여 계정으로 CLI를 인증합니다.

```
az login
```

인증되면 서비스 주체를 생성합니다.

#### Input:

```
az ad sp create-for-rbac --name SpNameExample --role "Website Contributor"
```

#### Output:

```
{
"appId": "f5f1ce7d-c247-42e6-91a4-ad1e7example",
"displayName": "SpNameExample",
"name": "http://SpNameExample",
"password": "97adeba6-4178-4f2b-bf5f-782b3example",
"tenant": "874186fd-a7a8-4e98-9b9e-3df00example"
}
```

위의 결과에는 Snyk 설정에 필요한 서비스 주체 이름, 비밀번호 및 tenant의 JSON 출력이 포함되어 있습니다. 여기서 Snyk 계정에 로그인하고 이름, 비밀번호 및 tenant에 붙여넣을 수 있습니다. Azure의 서비스 주체 새성에 대한 자세한 내용은 Azure의 문서인 [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli) , [포탈](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-create-service-principal-portal)에서 확인할 수 있습니다.

## **Azure Functions:** 연결 상태 확인

Azure 서비스 주체를 입력한 후 언제든지 두 곳 중 한 곳에서 연결 상태를 확인할 수 있습니다.

첫 번째는 통합 설정 페이지에서 현재 통합과 연결 상태를 볼 수 있습니다.

![](<../../../.gitbook/assets/image (25).png>)

또한 Azure Functions 통합 설정 페이지에서 직접 상태를 확인할 수 있습니다.(위에 표시된 통합 설정 페이지에서 "**Edit settings**"를 클릭하면 확인할 수 있음.) 인증 정보를 입력한 경우 Snyk이 Azure에 올바르게 연결할 수 있는지 여부를 나타내는 상자가 표시됩니다.

![](<../../../.gitbook/assets/image (31).png>)

연결할 수 없는 경우 계정 인증 정보를 다시 입력하여 올바른지 확인합니다.

![](<../../../.gitbook/assets/image (27).png>)

## **Azure Functions** 통합 비활성화

어떤 이유로든 이 통합을 비활성화하기로 결정한 경우 설정의 통합 페이지에서 이 작업을 수행할 수 있습니다.

통합 목록에서 비활성화하려는 특정 통합을 찾아 Edit settings를 클릭해야 합니다. 아래 예와 같이 통합의 현재 상태, 각 통합(인증 정보, API 키, 서비스 주체 또는 연결 세부 정보)에 대한 인증 정보를 업데이트할 수 있는 장소 및 연결을 끊을 수 있는 하단의 빨간색 상자를 보여주는 페이지로 이동합니다.

![](<../../../.gitbook/assets/image (26) (1).png>)

연결을 끊도록 선택하면 Snyk에서 인증 정보가 제거되고 모니터링하던 모든 통합 관련 프로젝가 Snyk에서 비활성화됩니다.

언제든지 이 통합을 다시 사용하도록 선택한 경우 인증 정보를 다시 입력하고 프로젝트를 활성화해야 합니다.

## Snyk에 Azure Functions 추가

Snyk을 Azure 계정에 성공적으로 연결했으면 Snyk이 모니터링할 Azure Functions를 선택할 수 있습니다. 통합 페이지의 **"Add projects"** 버튼을 사용하거나 Azure Functions 통합 설정 페이지에서 직접 이 작업을 수행할 수 있습니다.

두 경우 모두 연결한 Azure 계정에서 사용 가능한 Function 앱 목록을 볼 수 있습니다. 모니터링할 항목을 선택하고 **“Add to Snyk”** 버튼을 클릭합니다.

{% hint style="warning" %}
**NOTE:** 현재 **v2 functions** 가져오기에 대한 지원만 존재합니다. **모든 functions 무시됩니다.**&#x20;
{% endhint %}

![](<../../../.gitbook/assets/image (30).png>)

Snyk에 프로젝트를 추가하는 즉시 Snyk이 프로젝트를 테스트하고 [프로젝트 대시보드](https://app.snyk.io/projects)에 모니터링되는 모든 Azure functions 목록을 표시하기 시작합니다. 또한 현재 취약점의 스냅샷을 볼 수 있으며 수정 단계가 포함된 더 자세한 보고서를 클릭하여 볼 수 있습니다.

![](<../../../.gitbook/assets/image (32).png>)

이제 Snyk은 알려진 취약점에 대해 각 functions를 지속적으로 모니터링합니다. 언제든지 더 많은 functions를 추가할 수 있습니다.

**NOTE**\
Node.js 및 .Net의 경우 개발 디펜던시는 무시됩니다.
