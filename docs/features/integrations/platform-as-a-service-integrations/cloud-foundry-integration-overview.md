# Cloud Foundry 통합 개요

## Cloud Foundry 통합 개요

Snyk의 Cloud Foundry 통합을 사용하면 Java, Node.js, PHP 및 Ruby Cloud Foundry 애플리케이션의 배포된 코드를 모니터링하여 애플리케이션 디펜던시에서 발견되는 알려진 취약점을 제어하고 설정한 빈도로 테스트할 수 있습니다.

각 테스트마다 Snyk은 Cloud Foundry와 직접 통신하여 현재 어떤 코드가 구축되어 있으며 어떤 디펜던시가 사용되고 있는지 정확히 파악합니다. 각 디펜던시는 Snyk의 취약점 데이터베이스에 대해 차례로 테스트되며 알려진 취약점이 있는지 확인합니다.

취약점이 발견되면 즉시 조치를 취할 수 있도록 이메일 또는 Slack을 통해 경고를 받게 됩니다.

Cloud Foundry 통합 기능을 사용하려면 다음 작업을 수행해야 합니다.

1. 통합 페이지에서 Cloud Foundry로 연결
2. 모니터링할 프로젝트를 선택하고 “Add to Snyk”를 클릭

### Snyk을 Cloud Foundry에 연결하기

Snyk이 배포된 Cloud Foundry 애플리케이션을 모니터링할 수 있으려면 먼저 Snyk을 Cloud Foundry 계정에 연결해야 합니다. [Integrations 페이지](https://app.snyk.io/integrations)로 이동한 후 “Connect to Cloud Foundry”을 클릭하면 됩니다.

![](../../../.gitbook/assets/uuid-e7c43047-5065-ad28-db37-1c56e8796a8b-en-1-%20\(2\)%20\(2\)%20\(2\)%20\(2\)%20\(5\)%20\(7\)%20\(2\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(32\).png)

다음으로 Cloud Foundry API URL, Username 및 Password를 입력하라는 메시지가 나타나는 페이지로 이동합니다. Snyk 조직에 전용 사용자를 설정하는 것이 좋습니다.

![](<../../../.gitbook/assets/uuid-9710041e-427e-d577-ec40-5d3d1c818b5d-en (1).png>)

Cloud Foundry API URL을 찾는 방법은 다음과 같습니다.

### Cloud Foundry: API URL 찾기

[cf CLI](https://docs.cloudfoundry.org/cf-cli/install-go-cli.html) 도구에서 Cloud Foundry API URL을 찾을 수 있습니다.

`$ cf api API` endpoint: [https://api.example.com](https://api.example.com) (API version: 2.2.0)

여기에서 Snyk 계정에 로그인하고 Cloud Foundry 인증 정보를 입력할 수 있습니다.

### Cloud Foundry: 연결 상태 확인

Cloud Foundry 인증 정보를 입력한 후에는 언제든지 두 곳 중 한 곳에서 연결 상태를 확인할 수 있습니다.

첫 번째는 통합 설정 페이지에서 현재 통합 목록과 연결 상태를 볼 수 있습니다.

![](../../../.gitbook/assets/uuid-fb1cad51-f7f5-34ae-1142-f24fab0b0751-en%20\(3\)%20\(3\)%20\(3\)%20\(3\)%20\(3\)%20\(3\)%20\(3\)%20\(3\)%20\(3\)%20\(3\)%20\(2\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(15\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(15\).png)

연결 상태는 Cloud Foundry 통합 설정 페이지에도 직접 표시됩니다.(위에 표시된 통합 설정 페이지에서 “Edit settings”를 클릭하면 확인할 수 있음.) 인증 정보를 입력한 경우 Snyk이 Cloud Foundry에 올바르게 연결할 수 있는지 여부를 나타내는 상자가 표시됩니다.

![](../../../.gitbook/assets/uuid-f1a60a5d-1aa6-4983-956f-1e4fcecb9892-en.png)

연결할 수 없는 경우 계정 인증 정보를 다시 입력하여 올바른지 확인하십시오.

![](../../../.gitbook/assets/uuid-d78f594d-75a9-3cf3-2685-c96c63596ea0-en.png)

### Cloud Foundry 통합 비활성화

어떤 이유로든 이 통합을 비활성화하기로 결정한 경우 Settings의 Integrations 페이지에서 이 작업을 수행할 수 있습니다.

통합 목록에서 비활성화하려는 특정 통합을 찾아 Edit settings를 클릭해야 합니다. 아래 예와 같이 통합의 현재 상태, 각 통합(인증 정보, API 키, 서비스 주체 또는 연결 세부 정보)에 대한 인증 정보를 업데이트할 수 있는 장소 및 연결을 끊을 수 있는 하단의 빨간색 상자를 보여주는 페이지로 이동합니다.

![](../../../.gitbook/assets/uuid-b3a98f2c-4cc8-7753-8efa-396e9ec1e717-en-2-%20\(3\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(29\).png)

연결 해제를 선택하면 인증 정보가 Snyk에서 제거되고 우리가 모니터링하던 통합 관련 프로젝트가 Snyk에서 비활성화됩니다.

언제든지 이 통합을 다시 활성화하려면 인증 정보를 다시 입력하고 프로젝트를 활성화해야 합니다.

### Cloud Foundry에 Snyk 관련 사용자 추가

Snyk 조직의 Cloud Foundry에 전용 사용자를 추가할 것을 권장합니다. 이렇게 하면 어떤 이유로든 액세스를 취소해야 하는 경우 조직 내의 다른 사용자에게 영향을 미치지 않고 액세스를 취소할 수 있습니다.

Snyk과 통합하기 위해 필요한 최소 권한은 SpaceAuditor의 space 역할입니다.

다음 명령을 사용하여 명령줄에서 이러한 사용 권한을 가진 새 사용자를 생성할 수 있습니다.

`cf create-user snyk pa55w0rd`

`cf set-space-role snyk my-example-org development SpaceAuditor`

[Cloud Foundry documentation](https://docs.cloudfoundry.org/adminguide/cli-user-management.html)에서 다른 사용자를 애플리케이션에 추가하는 방법에 대해 자세히 알아볼 수 있습니다.

### Snyk에 Cloud Foundry 앱 추가

Snyk을 Cloud Foundry 계정에 성공적으로 연결했으면 Snyk이 모니터링할 Cloud Foundry 앱을 선택할 수 있습니다. 이 작업은 통합 페이지의 “Add projects” 버튼을 사용하거나 Cloud Foundry 통합 설정 페이지에서 직접 수행할 수 있습니다.

두 경우 모두 연결한 Cloud Foundry 계정에서 사용 가능한 프로젝트 목록을 볼 수 있습니다. 모니터링할 항목을 선택하고 “add to Snyk” 버튼을 클릭합니다.

![](../../../.gitbook/assets/uuid-d7a81cd8-f968-97d1-dcf8-d77a3b7df2fb-en.png)

Snyk에 프로젝트를 추가하는 즉시 Snyk이 프로젝트를 테스트하고 [프로젝트 대시보드](https://app.snyk.io/projects)에 모니터링되는 모든 Cloud Foundry 애플리케이션 목록을 표시하기 시작합니다. 또한 현재 취약점의 스냅샷을 볼 수 있으며 수정 단계가 포함된 더 자세한 보고서를 클릭하여 볼 수 있습니다.

![](../../../.gitbook/assets/uuid-de93d111-acb5-8792-2c6d-27bfece48315-en.png)

이제 Snyk은 알려진 취약점에 대해 각 프로젝트를 지속적으로 모니터링합니다. 언제든지 프로젝트를 추가할 수 있습니다.
