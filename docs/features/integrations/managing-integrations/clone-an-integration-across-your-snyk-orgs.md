# Snyk 조직 통합 복제

이미 구성한 조직을 복사 및 복제하기만 하면 Snyk의 여러 조직에서 동일한 브로커링된 Git 통합을 사용할 수 있습니다. 예를 들어 Snyk 조직 X, Y 및 Z를 단일 Git 저장소 X와 통합할 수 있습니다.

**전제 조건**: 조직 구성을 복제하려면 먼저 팀 및 그룹을 사용하도록 설정해야 합니다.

* **organization** 드롭다운에서 작업 중인 그룹 내의 조직으로 이동합니다.
* 이제 동일한 **organization** 드롭다운에서 **Create a new organization**을 클릭합니다.

![](../../../.gitbook/assets/create-new-org.png)

* 나타나는 페이지에서 작성 중인 새로운 조직의 이름을 입력합니다.
* **Copy across all settings and integrations?** 영역에서 브로커 토큰에 대해 이미 구성한 조직을 선택한 다음 **Create organization**을 클릭합니다.

![](../../../.gitbook/assets/create-new-org2.png)

* 브라우저가 방금 생성한 조직의 **대시보드**로 이동합니다. 브로커 통합이 복제되고 설정되며 브로커 토큰은 원래 조직의 토큰과 동일합니다.
* 복제된 구성을 다시 확인하려면 settings ![](../../../.gitbook/assets/cog\_icon.png) > **Integrations**를 클릭합니다.
* 설정할 통합 행에서 **Edit settings**를 클릭하여 복제된 브로커 통합을 확인합니다.
