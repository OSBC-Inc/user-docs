# Pivotal 통합 개요

Snyk의 Pivotal Web Services 통합을 사용하면 Java, Node.js 및 Ruby Pivotal Web Services 애플리케이션의 배포된 코드를 모니터링하여 애플리케이션의 디펜던시에서 발견된 알려진 취약점을 제어하고 설정한 빈도로 테스트할 수 있습니다.

각 테스트마다 Snyk은 Pivotal Web Services와 직접 통신하여 현재 배포된 코드와 사용 중인 디펜던시를 정확하게 확인합니다. 각 디펜던시는 Snyk의 취약점 데이터베이스에 대해 테스트되어 알려진 취약점이 있는지 확인합니다.

취약점이 발견되면 즉시 조치를 취할 수 있도록 이메일 또는 Slack을 통해 경고를 받게 됩니다.

Pivotal Web Services 통합을 설정하려면 다음 작업을 수행해야 합니다.

1. 통합 페이지에서 Pivotal Web Services에 연결
2. 모니터링할 프로젝트를 선택하고 “Add to Snyk”를 클릭

## **Snyk**을 **Pivotal Web Services**에 연결

Snyk이 배포된 Pivotal Web Services 애플리케이션을 모니터링할 수 있으려면 먼저 Snyk을 Pivotal Web Services 계정에 연결해야 합니다. [Integrations 페이지](https://app.snyk.io/integrations)로 이동한 후 “Connect to Pivotal Web Services”를 클릭하면 됩니다.

![](../../../.gitbook/assets/uuid-e7c43047-5065-ad28-db37-1c56e8796a8b-en-1-%20\(2\)%20\(2\)%20\(2\)%20\(2\)%20\(5\)%20\(7\)%20\(2\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(30\).png)

Pivotal Web Services의 Username과 Password를 입력하라는 메시지가 표시되는 페이지로 이동합니다. Snyk 조직에 대한 전용 사용자를 설정하는 것이 좋습니다.

![](../../../.gitbook/assets/uuid-f36c9d71-d472-085b-011b-0396dad112e5-en.png)

## **Pivotal Web Services:** 연결 상태 확인

Pivotal Web Services 인증 정보를 입력한 후 언제든지 두 곳 중 한 곳에서 연결 상태를 확인할 수 있습니다.

첫 번째는 통합 설정 페이지에서 현재 통합과 연결 상태를 볼 수 있습니다.

![](../../../.gitbook/assets/uuid-fb1cad51-f7f5-34ae-1142-f24fab0b0751-en%20\(3\)%20\(3\)%20\(3\)%20\(3\)%20\(3\)%20\(3\)%20\(3\)%20\(3\)%20\(3\)%20\(3\)%20\(2\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(15\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(20\).png)

연결 상태는 Pivotal Web Services 통합 설정 페이지에도 직접 표시됩니다.(위에 표시된 통합 설정 페이지에서 “Edit settings”를 클릭하면 확인할 수 있음.) 인증 정보를 입력한 경우 Snyk이 Pivotal Web Services에 올바르게 연결할 수 있는지 여부를 나타내는 상자가 표시됩니다.

![](../../../.gitbook/assets/uuid-442e2181-cac2-f74c-d50e-e4ebf0354b79-en.png)

연결할 수 없는 경우 계정 인증 정보를 다시 입력하여 올바른지 확인하십시오.

![](../../../.gitbook/assets/uuid-c7593b35-e315-e124-7a38-9c8c64ede382-en.png)

## Snyk에 Pivotal Web Services 앱 추가

Snyk을 Pivotal Web Services 계정에 성공적으로 연결했으면 Snyk이 모니터링할 Pivotal Web Services 앱을 선택할 수 있습니다. 통합 페이지의 “Add projects” 버튼을 사용하거나 Pivotal Web Services 통합 설정 페이지에서 직접 이 작업을 수행할 수 있습니다.

두 경우 모두 연결한 Pivotal Web Services 계정에서 사용 가능한 프로젝트 목록이 표시됩니다. 모니터링할 항목을 선택하고 “add to Snyk” 버튼을 클릭합니다.

![](../../../.gitbook/assets/uuid-3ab9deaa-2fca-d4b8-854e-64348b9b9cee-en%20\(1\)%20\(1\)%20\(3\)%20\(3\)%20\(3\)%20\(3\)%20\(3\)%20\(3\)%20\(3\)%20\(3\)%20\(3\)%20\(3\)%20\(2\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(11\).png)

Snyk에 프로젝트를 추가하는 즉시 Snyk이 프로젝트를 테스트하고 [프로젝트 대시보드](https://app.snyk.io/projects)에 모니터링되는 모든 Pivotal Web Services 애플리케이션 목록을 표시하기 시작합니다. 또한 현재 취약점의 스냅샷을 볼 수 있으며 수정 단계가 포함된 더 자세한 보고서를 클릭하여 볼 수 있습니다.

![](../../../.gitbook/assets/uuid-790ddca1-dfb1-2b98-952a-bd5eeff94a50-en.png)

이제 Snyk은 알려진 취약점에 대해 각 프로젝트를 지속적으로 모니터링합니다. 언제든지 프로젝트를 추가할 수 있습니다.

## **Pivotal Web Services** 통합 비활성화

어떤 이유로든 이 통합을 비활성화하기로 결정한 경우 Integrations 페이지에서 이 작업을 수행할 수 있습니다.

통합 목록에서 비활성화하려는 특정 통합을 찾아 Edit settings를 클릭해야 합니다. 아래 예와 같이 통합의 현재 상태, 각 통합(인증 정보, API 키, 서비스 주체 또는 연결 세부 정보)에 대한 인증 정보를 업데이트할 수 있는 장소 및 연결을 끊을 수 있는 하단의 빨간색 상자를 보여주는 페이지로 이동합니다.

![](../../../.gitbook/assets/uuid-b3a98f2c-4cc8-7753-8efa-396e9ec1e717-en-2-%20\(3\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(37\).png)

연결 해제를 선택하면 인증 정보가 Snyk에서 제거되고 우리가 모니터링하던 통합 관련 프로젝트가 Snyk에서 비활성화됩니다.

언제든지 이 통합을 다시 활성화하려면 인증 정보를 다시 입력하고 프로젝트를 활성화해야 합니다.

## **Pivotal Web Services**에 Snyk 관련 사용자 추가

Snyk 조직의 Pivotal Web Services에 전용 사용자를 추가하는 것이 좋습니다. 이렇게 하면 어떤 이유로든 액세스를 취소해야 하는 경우 조직 내의 다른 사용자에게 영향을 미치지 않고 액세스를 취소할 수 있습니다.

Snyk과 통합하기 위해 필요한 최소 권한은 SpaceAuditor의 space 역할입니다.

다음 명령을 사용하여 Cloud Foundry 명령줄에서 이러한 권한을 가진 새 사용자를 생성할 수 있습니다.

`cf create-user snyk pa55w0rd`

`cf set-space-role snyk my-example-org development SpaceAuditor`

[Cloud Foundry documentation](https://docs.cloudfoundry.org/adminguide/cli-user-management.html)의 명령줄을 통해 애플리케이션에 다른 사용자를 추가하는 방법에 대해 자세히 알아볼 수 있습니다.

또는 [Pivotal console](https://console.run.pivotal.io)을 통해 Snyk 관련 사용자를 추가할 수 있습니다.
