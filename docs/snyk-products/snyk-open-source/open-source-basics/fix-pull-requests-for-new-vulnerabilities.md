# 새로운 수정 사항에 대한 자동 pull request 생성

취약점에 대한 자동 PR 생성에는 다음 규칙이 적용됩니다.

* Pull requests는 **Test & Automated Pull Request Frequency**(아래 스크린샷 참조) 설정을 기반으로 생성됩니다.
* 스캔이 수동으로 실행되는 경우(프로젝트에 대해 **Retest now**를 클릭) 24시간 내에 실행되었다고 표시되며 다음 자동 스캔이 실행될 때까지 자동 PR이 생성되지 않습니다.
* 프로젝트당 하나의 pull request가 생성됩니다(우선순위 점수 700 이상만 해당).
* 수정 가능한 사항이 있거나 무시되지 않는 새로운 취약점에 대해 적용됩니다.
* 알려진 취약점에 대해서는 다음을 참조하십시오.[fix-pull-requests-for-known-vulnerabilities-backlog.md](fix-pull-requests-for-known-vulnerabilities-backlog.md "mention")

![](../../../.gitbook/assets/os1.png)

마지막 스캔이 언제 시작되었는지 확인하려면 프로젝트 페이지에서 **Snapshot taken by recurring test**을 확인하고, 특정 스캔 결과에 대한 **\[snyk] Vulnerability alert** 이메일을 확인하십시오.

![](../../../.gitbook/assets/os2.png)

새로운 취약점에 대한 pull request는 새로운 통합에 대해 기본적으로 활성화되어 있습니다.

지원되는 통합에 대한 자세한 내용은 [Git 저장소(SCM) 통합](../../../features/integrations/git-repository-scm-integrations/)을 참조하십시오.

## 모든 프로젝트에 대한 pull requests 활성화 또는 비활성화

전역 통합 설정을 진행하는 방법은 다음과 같습니다.

1. 설정으로 이동하여 ![](../../../.gitbook/assets/cog\_icon.png) > **Integrations** 클릭
2. SCM 통합(예: Github)을 클릭
3. **New vulnerabilities** 활성화

**Apply changes to all overridden projects**를 진행하면 "Automatic fix pull requests"에 대한 모든 개별 프로젝트 설정이 업데이트됩니다. 이전에 프로젝트에 대한 개별 설정이 진행된 경우 이 버튼을 클릭하면 전역 설정으로 재정의됩니다.

![](../../../.gitbook/assets/global-pr-setting.png)

## 단일 프로젝트에 대한 pull requests 활성화 또는 비활성화

프로젝트 수준에서 활성화/비활성화를 설정하면 전역 통합 설정과 별개로 해당 프로젝트를 재정의합니다.

1. **Projects**에서 프로젝트를 선택하고 **Settings**(오른쪽 상단)를 클릭합니다.
2. **GitHub integration** 클릭
3. **Automatic fix pull requests** 섹션에서 설정을 진행합니다.
   * **Customize for only this project**를 클릭합니다.
   * **New vulnerabilities**를 활성화합니다.
   * **Save changes**를 클릭합니다.

![](../../../.gitbook/assets/os3.png)
