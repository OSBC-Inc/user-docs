# 구축 시 Snyk을 사용하여 TeamCity 통합

모든 프로젝트의 경우 구성에 따라 빌드 중에 코드를 검색하고 빌드에 취약점이 있는지 확인하기 위해 빌드에 Snyk을 추가할 수 있습니다.

Snyk은 배포 전에 Snyk Security 단계를 사용하여 빌드를 실행하는 것이 좋습니다.

TeamCity 및 기능에 대한 자세한 내용은 [TeamCity documentation](https://www.jetbrains.com/help/teamcity/teamcity-documentation.html)을 참조하십시오.

다음은 **Snyk 단계로 빌드를 구성하는 방법**을 설명합니다.

* 새 프로젝트 또는 기존 프로젝트에 Snyk 단계를 추가합니다.
  * 새 프로젝트의 경우 빌드를 생성할 Git 저장소를 구성한 후 자동 탐지 기능을 활성화하여 프로젝트 빌드와 관련된 단계를 자동으로 식별합니다.
  * 기존 프로젝트의 경우 **프로젝트 빌드 단계를 편집**하기 위해 이동합니다.\
    \
    Snyk 단계가 추가되면 제안된 단계 목록에 **Snyk Security** 가 나타나고 **Parameters Description** 열에 현재 테스트 정책이 나타납니다.

![Snyk Security in the list of suggested build steps](../../../../../.gitbook/assets/uuid-97395df2-f141-6f77-4551-f19397ac0781-en.png)

* 다음과 같이 Snyk Security 단계를 구성합니다.
  * **Snyk Security** 행의 아무 곳이나 클릭하여 구성 화면에 액세스합니다.
  * 기존 프로젝트의 경우 **Add build step**을 클릭하여 구성 화면에 액세스합니다.

![Configure Snyk security for TeamCity](../../../../../.gitbook/assets/uuid-88e38280-121e-a17b-cfd3-9fde89305b5c-en.png)

* TeamCity 필드(Runner type, Step name 및 Execute Step)를 구성합니다.
* 선택적으로 **Show advanced options**를 클릭하여 추가 Snyk 파라미터가 표시됩니다.

![Additional Snyk parameters](../../../../../.gitbook/assets/uuid-8f294e8d-ca5e-123b-2992-a98c1e62fd6f-en.png)

* **Snyk Settings** 및 **Snyk Tool Settings**를 구성합니다. 자세한 내용은 TeamCity configuration parameters를 참조하십시오.
* 구성이 완료되면 빌드를 실행합니다. Snyk Security 단계가 성공적으로 완료되면 **Snyk Security Report** 탭으로 이동하여 TeamCity 내의 결과를 보고 추가 작업을 위해 Snyk UI로 이동할 수 있습니다.

![Snyk test report](../../../../../.gitbook/assets/uuid-e8b1fd6f-3b49-069c-c9fe-c0948931b141-en.png)

* F보고서 맨 위에서 **View on Snyk.io**를 클릭하여 Snyk 앱에서 스냅샷 및 취약성 정보를 직접 확인합니다.
