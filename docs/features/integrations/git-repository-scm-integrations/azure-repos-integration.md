# Azure Repos 통합

사용자는 특히 Snyk용으로 생성된 고유한 Azure DevOps PAT(개인 액세스 토큰)를 생성합니다. 사용자 이름과 비밀번호는 함께 Snyk이 사용하는 토큰을 구성합니다. 토큰은 Snyk이 생성할 때 사용자가 Azure Repos에 나타내는 특정 권한에 대해서만 사용자의 리포지토리에 액세스할 수 있는 권한을 부여합니다.

1. 사용자는 Snyk으로 가져올 프로젝트와 저장소를 선택합니다(테스트 및 모니터링용). 사용자는 저장소의 루트 폴더에 없는 매니페스트 파일에 대한 사용자 지정 파일 위치를 입력할 수도 있습니다.
2. Snyk은 사용자가 선택한 항목을 평가하고 루트 폴더와 모든 수준의 모든 하위 폴더에 관련 매니페스트 파일이 있는 항목을 가져옵니다.
3. Snyk는 실행되는 각 테스트에 대해 리포지토리와 직접 통신하여 현재 푸시된 코드와 사용 중인 종속성을 정확히 결정합니다. 각 종속성은 Snyk의 취약성 데이터베이스에 대해 테스트되어 알려진 취약성이 있는지 확인합니다.
4. 구성을 기반으로 취약점이 발견되면 Snyk는 이메일이나 Slack을 통해 알려 즉시 수정 조치를 취할 수 있습니다.

## Azure Repos용 Snyk에 프로젝트 추가

Snyk은 루트 폴더 및 사용자 지정 파일 위치를 평가하여 지원되는 언어로 된 Azure Repos를 테스트하고 모니터링합니다.

**Snyk에 프로젝트 추가**

1. **Projects**로 이동하여 **Add projects**를 클릭합니다. 프로젝트를 가져올 도구를 선택하십시오.
2. 선택한 통합에서 사용 가능한 모든 리포지토리가 포함된 팝업 화면이 열립니다.
3. 보안/라이센스 문제를 모니터링하기 위해 Snyk로 가져올 저장소를 선택하십시오. 특정 조직의 모든 저장소를 가져오려면 조직에 체크 표시를 합니다.
4. 선택한 리포지토리 추가를 클릭합니다. 이제 Snyk는 전체 파일 트리에서 종속성 파일을 검색하고 이를 프로젝트로 Snyk에 가져옵니다.

![](<../../../.gitbook/assets/uuid-cae3b5b8-6971-406c-3c00-91c9d1a570a2-en (1).png>)

## 사용자 지정 파일 위치 추가

1. 사용자 지정 파일 위치 추가 드롭다운 목록에서 사용자 지정 경로를 구성하려는 관련 리포지토리를 선택합니다. 리포지토리는 이전 단계에서 설명한 대로 프로젝트 추가 보기에서 먼저 선택해야 합니다.
2. 텍스트 필드에 위 이미지와 같이 매니페스트 파일이 있는 상대 경로를 입력합니다.

## 가져오기에서 폴더 제외

이 통합은 다른 통합과 유사하게 작동합니다. 프로젝트를 계속 모니터링, 수정 및 관리하려면 문서에서 관련 페이지를 참조하세요.

{% hint style="info" %}
**주의**\
이 필드는 대소문자를 구분하며 패턴은 모든 저장소에 적용됩니다.
{% endhint %}

**다음 단계**

리포지토리를 가져오면 화면 상단에 확인 메시지가 녹색으로 나타납니다. 선택한 파일은 고유한 아이콘으로 표시되며 조직/리포지토리별로 이름이 지정되며 이제 아래 예와 같이 해당 프로젝트만 보도록 필터링할 수도 있습니다.

![](../../../.gitbook/assets/screen-shot-2021-09-16-at-9.12.12-am.png)

이 통합은 다른 통합과 유사하게 작동합니다. 프로젝트를 계속 모니터링, 수정 및 관리하려면 문서에서 관련 페이지를 참조하세요.

## Azure Repos에 대한 통합 구성 기능 가용성

{% hint style="info" %}
**기능 가용성**\
Azure Repos Cloud와의 통합은 모든 요금제에 사용할 수 있습니다. Azure DevOps Server 2020 이상(TFS라고도 함)과의 통합은 엔터프라이즈 및 비즈니스 플랜에서 사용할 수 있습니다. 자세한 내용은 [요금제](https://snyk.io/plans/)를 참조하세요.
{% endhint %}

Snyk는 Microsoft Azure Repos와 통합되어 프로젝트를 가져오고 리포지토리의 소스 코드를 모니터링할 수 있습니다. Snyk는 가져온 프로젝트에서 애플리케이션의 종속성에서 발견된 알려진 보안 취약성을 테스트하고 사용자가 제어하는 빈도로 테스트합니다.

## 통합을 구성하는 방법

Azure Repos와 Snyk 간의 통합을 활성화하고 취약성 관리를 시작하세요.

전제 조건

Azure Repos 계정과 Snyk 계정을 설정했는지 확인합니다.

{% hint style="info" %}
**주의**: it is important that a Snyk admin user configure the integration within the UI. Collaborator users cannot complete this task.
{% endhint %}

**단계**

1. Git 리포지토리가 [Azure DevOps documentation](https://docs.microsoft.com/en-us/azure/devops/repos/git/set-git-repository-permissions)를 볼 수 있도록 하려면 개인 액세스 토큰을 만드는 계정이 Project Administrators 그룹의 구성원이어야 합니다. .
2. Azure Repos 계정에 액세스하고 Snyk에서 사용자 한 개인 액세스를 검색합니다. 이 작업에 대한 도움말은 [Azure DevOps documentation](https://docs.microsoft.com/en-us/azure/devops/repos/git/set-git-repository-permissions)를  참조하세요.
3. Azure에서 메시지가 표시되면 다음과 같이 Snyk 액세스 권한을 활성화합니다.
   * 만료 - 통합 중단을 방지하기 위해 이 토큰의 만료 날짜를 훨씬 먼 미래로 선택하는 것이 좋습니다.
   * 범위 - 사용자 정의
   * 코드 - 읽기 및 쓰기(개인 액세스 토큰을 생성하는 사용자가 리포지토리의 관리자가 아닌 경우 프로젝트 관리자 그룹 권한 활성화)
4. Snyk 계정에 [로그인](https://app.snyk.io/login)합니다.
5. 상단의 메뉴 모음에서 **Integrations**로 이동합니다.
6. Azure Repos 로고 아래의 **Integrations** 페이지에서 **Connect to Azure Repos** 버튼을 클릭합니다.
7. 통합 영역의 **설정** 페이지에서 **통합**하려는 Azure DevOps 조직(예: [https://dev.azure.com/{org-name}\\](https://dev.azure.com/%7Borg-name%7D\)/) 및 방금 생성한 개인 액세스 토큰)을 입력합니다. \* Enterprise 고객은 공개적으로 연결할 수 있는 Azure Repos Server 프라이빗 인스턴스에 대한 사용자 지정 URL을 제공할 수도 있습니다.
8. **Save**를 클릭합니다.
9. Snyk은 연결 값을 테스트하고 페이지를 다시 로드하여 이제 Azure Repos 통합 정보를 표시합니다. 세부 정보가 저장되었다는 확인 메시지도 화면 상단에 녹색으로 나타납니다. 또한 Azure에 대한 연결이 실패한 경우 Azure Repos에 연결됨 섹션 아래에 알림이 나타납니다.

![](../../../.gitbook/assets/screen\_shot\_2020-05-19\_at\_17.16.24.png)
