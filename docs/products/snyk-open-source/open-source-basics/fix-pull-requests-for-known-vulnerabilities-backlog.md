# 알려진 취약점(backlog)에 대한 자동화된 pull requests

**알려진 취약점**은 프로젝트의 백로그에서 취약점을 검색합니다. 이것은 이전에 선언된 취약점입니다.

취약점에 대한 자동 PR 생성에는 다음 규칙이 적용됩니다.

* Pull requests는 **Test & Automated Pull Request Frequency** (아래 스크린샷 참조) 설정을 기반으로 생성됩니다.
* 스캔이 수동으로 실행되는 경우(프로젝트에 대해 **Retest now**클릭)24시간 실행된 것으로 표시되고 다음 자동 스캔이 실행될 때까지 자동 PR이 생성되지 않습니다.
* 프로젝트당 하나의 pull request가 생성됩니다(우선순위 점수 700 이상에 해당).

![](../../../.gitbook/assets/os1.png)

마지막 24시간 실행이 시작된 시간을 확인하려면 프로젝트 페이지에서 **Snapshot taken by recurring test**를 확인하고, 특정 스캔 결과에 대한 **\[snyk] Vulnerability alert** 이메일도 확인하십시오.

![](../../../.gitbook/assets/os2.png)

## 통합을 위한 pull requests 활성화 또는 비활성화

전역 수준에서 활성화하려면 다음과 같은 과정을 진행합니다.

1. 설정 클릭 ![](../../../.gitbook/assets/cog\_icon.png) > **Integrations**
2. SCM(예:Github) 통합 선택
3. **Known vulnerabilities (backlog)** 활성화

**Apply changes to all overridden projects** 을 진행하면 "자동 pull request"에 대한 모든 개별 프로젝트 설정이 업데이트 됩니다. 프로젝트에 이에 대한 자체 설정이 존재하는 경우 전역 설정으로 재정의됩니다.

![](../../../.gitbook/assets/screen\_shot\_2021-05-24\_at\_12.23.38\_pm.png)

### 단일 프로젝트에 대한 pull requests 활성화 또는 비활성화

프로젝트 수준에서 활성화/비활성화를 진행하려면 해당 단일 프로젝트를 재정의합니다.

1. 프로젝트로 이동하여 **Settings**를 선택합니다.
2. **GitHub integration** 선택
3. **Automatic fix pull requests** 섹션에서 다음과 같이 진행합니다.
   * **Customize for only this project**를 선택합니다.
   * **Known vulnerabilities (backlog)** 활성화

![](../../../.gitbook/assets/os3.png)
