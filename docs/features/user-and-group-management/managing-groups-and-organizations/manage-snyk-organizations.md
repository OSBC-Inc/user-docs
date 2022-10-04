# Snyk 조직 관리

**Manage organization** 섹션에서 다음을 수행할 수 있습니다:

* 조직에 얼마나 많은 비공개, 공개 및 비활성 프로젝트가 있는지 확인
* 팀원을 확인하고 관리
* 조직 떠나기
* 조직 삭제하기(관리자 사용자만 해당).

### 새 Snyk 조직 만들기

Snyk에서 조직을 무제한으로 가질 수 있습니다. 각 조직은 다른 요금제를 사용할 수 있습니다.

새 조직을 만들려면 상단 탐색 메뉴의 드롭다운에서 '만들기' 링크를 선택합니다. 그런 다음 조직의 이름을 지정하고 평가판을 시작할 수 있습니다.

![](<../../../.gitbook/assets/Screen Shot 2021-10-28 at 9.57.47 AM.png>)

### 조직 삭제

조직 관리자는 관련된 그룹이 없는 한 조직을 삭제할 수 있습니다.

조직에서 그룹을 사용 중인 경우 그룹 관리자만 조직을 삭제할 수 있습니다.

**조직을 삭제하려면:**

1\. Snyk Web UI의 상단 메뉴에서 조직 드롭다운 목록을 열고 삭제할 조직을 선택합니다:

![](<../../../.gitbook/assets/Org Settings - Selecting an Org.png>)

2\. 선택한 조직이 표시되면 상단 메뉴에서 **Org Settings** 버튼<img src="../../../.gitbook/assets/image (11).png" alt="" data-size="line">을 클릭합니다:

![](<../../../.gitbook/assets/Org Settings - Button.png>)

3\. **Settings** 페이지의 왼쪽 메뉴에서 **Genera**l을 선택합니다:

![](<../../../.gitbook/assets/image (3) (1).png>)

4\. **Delete organization** 섹션까지 아래로 스크롤하고 **Delete organization** 버튼을 클릭합니다:

![](<../../../.gitbook/assets/Org Settings - Delete organization.png>)

5\. 확인 대화 상자에서 삭제할 조직의 이름을 입력하여 삭제를 확인합니다. 그런 다음 **OK**를 클릭합니다.

![](<../../../.gitbook/assets/Org Settings - Delete organization - Confirmation.png>)

선택한 조직이 Snyk 계정에서 삭제됩니다.

### 선호하는 조직 설정

여러 조직이 있는 경우 이러한 조직 중 하나가 기본적으로 Snyk 계정의 **Preferred Organization**으로 설정됩니다. 선호 조직은 다음을 결정합니다.

* Snyk Web UI - Snyk 계정에 로그인할 때 기본적으로 표시되는 조직입니다.
* Snyk CLI - CLI를 통해 테스트를 실행할 때 테스트 수에 기본적으로 사용되는 조직입니다.\
  **Note**: CLI를 통해 테스트 카운트에 사용할 조직을 변경하려면 다음을 사용하십시오. `--org=<ORG_ID>` 명령. 자세한 내용은 [code test 하위 명령에 대한 옵션](../../snyk-cli/cli-command/undefined-1.md)을 참조하십시오.

Web UI의 계정 설정을 통해 Snyk 계정의 기본 조직을 변경할 수 있습니다.

**선호하는 조직을 변경하려면:**

1\. Snyk Web UI에서 화면 오른쪽 상단 모서리에 있는 계정 아이콘을 클릭합니다. 그런 다음 **Account settings** 옵션을 선택합니다:

![](<../../../.gitbook/assets/Account Settings - Opening.png>)

2\. **Account Settings** 페이지 – **Preferred Organization** 섹션에서 조직 드롭다운 목록을 열고 선호하는 조직으로 설정할 조직을 선택합니다.

**Note**: 조직 드롭다운 목록에 기존 조직이 표시됩니다.

![](<../../../.gitbook/assets/spaces\_-MdwVZ6HOZriajCf5nXH\_uploads\_git-blob-4c4d5449f7627eeedbc1d0eb4e5d7142faff67a7\_image (244).png>)

3\. **Update Preferred Org** 버튼을 클릭하여 새 설정을 저장합니다.

**Preferred Organization**으로 선택한 조직은 Snyk 계정에 로그인할 때 표시되며 CLI를 통해 테스트를 실행할 때 기본적으로 테스트 수에 사용됩니다.
