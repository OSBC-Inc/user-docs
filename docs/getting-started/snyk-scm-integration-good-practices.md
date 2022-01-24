# Snyk SCM 통합: 모범 사례

Snyk을 SCM(Source Control Manager)과 통합하여 모든 프로젝트를 쉽고 빠르게 파악할 수 있습니다.

Snyk SCM 통합을 통해 다음을 수행할 수 있습니다:

* 통합된 모든 저장에 대한 지속적인 보안 스캐닝 수행
* 오픈소스 컴포넌트의 취약성 탐지
* 자동 수정 기능 제공

## 권장하는 배포 순서

각 통합에 대한 원활한 배포를 위해 아래에 설명된 단계를 따르십시오.

모든 SCM 통합 기능을 동시에 구현하려고 하면 SDLC에 문제가 발생하여 개발 성능이 저하될 위험이 있습니다.

| **배포 단계**                                                                                                              | **구성**                                                                                                                                                                                                                    | 결과                                                                                                      |
| ---------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| <p><a href="snyk-scm-integration-good-practices.md">1단계 </a></p><p>SCM 통합을 설정합니다.</p>                                  | See configuration documentation for each [SCM integration](../features/integrations/git-repository-scm-integrations/)                                                                                                     | A configured integration, ready to import projects                                                      |
| <p><a href="snyk-scm-integration-good-practices.md">2단계</a></p><p>SCM에서 모든 프로젝트를 가져옵니다.</p>                            | <p>- Test both public and private repos</p><p>- Disable all user notifications</p><p>- Disable Snyk PR checks</p><p>- Disable Auto-fix PRs</p><p>- Disable Failing PR checks</p><p>- Disable Auto dependency upgrades</p> | A complete Software Bill of Materials that enables you to assess risk across your applications.         |
| <p><a href="snyk-scm-integration-good-practices.md">3단계</a></p><p>개발자 및 보안 팀은 Snyk의 우선순위 보고 기능을 사용하여 수정 계획을 수립합니다.</p> | Click [here](https://www.youtube.com/watch?v=\_kAY94JwQHY) to learn more about Snyk prioritization Reporting.                                                                                                             | Alignment between Developers and Security on what should be fixed and when streamlines the fix process. |
| <p><a href="snyk-scm-integration-good-practices.md">4단계</a></p><p>개발자에게 실시간으로 문제를 경고하고 수정 가능한 사항에 대해 알려줍니다.</p>        | <p>- Enable Snyk PR checks and fail PRs</p><p>if they contain High severity issues</p><p>with available fixes</p><p>- Enable Auto-fix PRs</p>                                                                             | Improve your organization’s mean-time-to-fix (MTTF).                                                    |
| <p><a href="snyk-scm-integration-good-practices.md">5단계</a></p><p>개발자가 새로운 취약점을 들어오지 못하도록 방지합니다.</p>                   | <p>- Enable Failing PR checks, for ANY</p><p>High severity issues (fix or no fix)</p>                                                                                                                                     | ‘Secure by Design’ methodology achieved.                                                                |
| <p><a href="snyk-scm-integration-good-practices.md">6단계</a></p><p>Reduce technical security debt</p>                   | - Enable Auto dependency upgrades                                                                                                                                                                                         | Reduce future design headaches, and hot fixes, which can be time-consuming to research & address.       |

&#x20;

## 1단계: SCM 통합 설정

Snyk은 GitHub, GitHub Enterprise, Bitbucket Cloud 등 SCM을 위한 사전 통합을 구축했습니다. 전체 목록은 [GIT 저장(SCM) 통합](https://support.snyk.io/hc/en-us/sections/360001138098-Git-repository-SCM-integrations)을 참조하십시오.

SCM이 이미 구성되어 있는지 확인하려면 **Integrations** 탭으로 이동합니다. 통합된 SCM은 **Configured**로 표시됩니다.

![](../.gitbook/assets/int1.png)

{% hint style="info" %}
SCM이 이미 통합되어 있다면 다음 단계로 이동합니다.
{% endhint %}

## 예: GitHub

다음은 **Github.com**에 통합을 설정하는 방법의 예입니다.

1. **Integrations** 탭으로 이동하여 **GitHub**를 클릭합니다.
2. Snyk에게 public 및 private 저장소 모두에 대한 액세스 권한을 부여할지 또는 public 저장소에만 액세스 권한을 부여할지 선택합니다:
3. Snyk에게 저장소에 대한 액세스 권한을 제공하려면 **Authorize snyk**을 클릭합니다:

![](<../.gitbook/assets/authorize (1) (2) (6) (1) (18).png>)

**저장소에 대한 SCM 권한 **~~**수정필요**~~** \*(**

Operations triggered using the Snyk UI (such as opening a Fix PR or retesting a project) are performed for the acting user. So to perform these operation, you must connect your own SCM user or service account. This gives Snyk the required permissions for the repositories for where you would like to perform these operations.

예를 들어 GitHub에서 Snyk으로 연결된 계정은 대상 저장에 대해 다음과 같은 액세스 권한이 필요합니다:

| **Action**                         | **Why?**                                                                             | **Required permissions on the repository** |
| ---------------------------------- | ------------------------------------------------------------------------------------ | ------------------------------------------ |
| 일별/주간별 테스트                         | private 저장에 파일 읽기용                                                                   | _**Write**_ 권한 이상                          |
| pull requests에서 Snyk 테스트           | 새로운 PR이 생성되거나 기존 PR이 업데이트될 때마다 pull request 상태 확인을 전송하기 위함                           |                                            |
| 수정 및 업그레이드 pull requests 열기        | 모니터링되는 저장소에 수정/업그레이드 PR 작성용                                                          |                                            |
| pull requests에 대한 Snyk 테스트 - 초기 구성 | 가져온 저장소에 Snyk의 웹훅을 추가하면 pull requests가 생성되거나 업데이트될 때마다 Snyk이 알림을 받고 검색을 트리거할 수 있습니다. | _**Admin**_                                |

### 알림 설정 변경

기본적으로 프로젝트 디펜던시의 새로운 문제 또는 수정 사항이 발견되면 Snyk은 조직 내 모든 사용자에게 메일을 통해 조직 전체의 보안 상태를 알립니다. 많은 프로젝트를 조직으로 가져오려는 경우 사용자에게 너무 많은 이메일 알림이 전송되지 않도록 해당 조직에 대한 모든 알림을 비활성화할 수 있습니다.

조직 내 사용자가 수신하는 이메일을 설정하려면 조직의 settings ![](../.gitbook/assets/cog\_icon.png) > **Notifications**로 이동합니다. 여기서 변경한 내용은 조직의 모든 구성원에게 영향을 미치지만, 조직 내 사용자는 사용자 수준 계정 설정에서 이러한 기본 설정을 재정의할 수 있습니다.

가져오기 전에 조직 내의 모든 사용자에 대한 알림을 비활성화하려면 해당 체크 박스들의 선택을 취소하십시오:

![](<../.gitbook/assets/image (58).png>)

자세한 내용은 [Notification management](https://support.snyk.io/hc/en-us/articles/360004037657-Notification-management)를 참조하십시오.

## 2단계: 프로젝트 가져오기

1. Snyk UI의 **Projects** 페이지로 이동하여 **Add projects**를 선택하고, Snyk로 가져올 저장소를 선택한 다음 **Add selected repositories**를 클릭합니다.
2. Snyk은 선택한 저장소에서 전체 디렉터리 트리의 디펜던시 파일(예: **package.json**)을 검사하기 시작하고 이러한 파일을 프로젝트로 가져옵니다.
3. Snyk은 루트 폴더와 정의된 사용자 정의 파일 위치를 평가합니다. 매니페스트 또는 구성 파일이 없으면 파일을 가져올 수 없다는 경고가 표시됩니다.
4. Snyk은 매니페스트 파일(프로젝트)을 탐지하여 테스트한 다음 결과를 표시합니다. 가져온 프로젝트는 저장소 이름 아래에 표시됩니다.

![](../.gitbook/assets/int3.png)

5\. 프로젝트를 가져왔는지 확인하려면 Add projects 페이지로 이동하십시오. 가져온 프로젝트에는 저장소 이름 옆에 ✔ 아이콘이 있습니다. (프로젝트를 가져온 후 지속적인 취약성 검사)

![](../.gitbook/assets/aws-sdk.png)

## 3단계: PR에서 Snyk 테스트 사용

**PR 테스트 설정 & 워크플로우**

기본적으로 Snyk은 모니터링되는 저장소에 제출된 모든 pull request를 검색하여 결과와 권장 사항을 단일 보안 검사와 단일 라이선스 검사로 그룹화하여 보여줍니다:

![](../.gitbook/assets/checks-passed.png)

**상태 세부 정보**

"Details" 링크를 클릭하면 Snyk 검사에서 다음과 같은 상태가 나타날 수 있습니다:

* **Success**: 식별된 문제가 없고 모든 점검이 통과됨
* **Processing**: Snyk 테스트가 끝날 때까지 표시됨
* **Failure**: 문제가 확인되었을 때, 검사를 통과하기 위한 수정 필요
* **Error**: 매니페스트 파일이 동기화되지 않았거나, Snyk이 매니페스트 파일을 읽을 수 없거나, Snyk가 매니페스트 파일을 찾을 수 없을 때 오류가 발생합니다.

![](../.gitbook/assets/security-check.png)

**PR 테스트 설정 관리**

관리자는 조직 수준에서 Snyk PR 테스트 설정을 관리하여 모든 프로젝트에 적용하거나 PR 테스트를 적용할 특정 프로젝트를 선택할 수 있습니다. 기능의 설정 여부(기본적으로 활성화됨)를 구성하고, 실패 조건을 설정하여 Snyk이 PR 검사를 통과하지 못할 시기를 정의할 수 있습니다.

조직의 PR 테스트 설정을 구성하려면 다음과 같이 하십시오:

1. **Org** > settings ![](../.gitbook/assets/cog\_icon.png) **>** Integrations > Edit Settings로 이동합니다.
2. **Enabled**로 설정하고 필요에 따라 **Fail conditions** 설정합니다.
3. **Update settings**를 클릭합니다.

![](../.gitbook/assets/image13.png)

특정 프로젝트에 대한 pull request를 설정하려면 **Projects Page**> **Projects Settings > Edit Settings**로 이동하여 조건을 비슷하게 설정하십시오:

![](../.gitbook/assets/main.png)

{% hint style="info" %}
라이선스 정책을 사용하여 라이선스 문제로 인해 Snyk이 PR에 실패하는 것을 방지할 수 있습니다. 자세한 내용은 [라이선스 정책](https://support.snyk.io/hc/en-us/sections/360002249578-License-Policies)을 참조하십시오.
{% endhint %}

**Initial step: visibility** 및 **fail conditions** 설정

At the start of rollout, 개발자가 Snyk Commit을 확인하는 것에 익숙해지도록, PR을 테스트하는 것부터 시작하는 것이 좋습니다.

1. 이를 조직 또는 특정 프로젝트에 적용하기로 결정합니다.
2. 조건을 설정합니다:
   * **예) Only fail when the PR is adding a dependency with issues** : PR이 문제가 있는 디펜던시를 추가하는 경우에만 실패
   * **예)** **Only Fail for high severity issues** : 심각도가 높은 문제에 대해서만 실패
   *   **예) Only fail when the issues found have a fix available** : 발견된 문제에 수정 가능한 사항이 있는 경우에만 실패

       &#x20;

## 4단계: **정책에 따른** PRs

SDLC에 Snyk을 내장하고 Snyk에 대한 개발자의 인지를 높인 후에는 보다 엄격한 정책을 적용하여 전반적인 보안 상태를 개선할 수 있습니다.

**예)**

* **낮은 우선 순위의 프로젝트**: 수정 가능한 새로운 높은 심각도에 대해서만 PR을 실패할 수 있습니다.
* **중간 우선 순위의 프로젝트**: 심각도가 높은 문제에 대해서만 PR에 실패합니다.
* **높은 우선 순위의 프로젝트(PCI/GDPR compliance)**: 모든 문제에 대해 PR에 실패합니다.

{% hint style="info" %}
취약점 심각도를 내부의 정책과 일치시키려면 보안 정책을 사용하여 문제의 심각도를 변경하고 관련 프로젝트 특성에 연결하십시오. 자세한 내용은 [보안 정책](https://support.snyk.io/hc/en-us/sections/360004225818-Security-Policies)을 참조하십시오.
{% endhint %}

## 5단계: 자동 수정 PRs

Snyk은 매일 또는 매주 프로젝트를 스캔합니다. 새 취약점이 발견되면 Snyk은 이메일을 통해 사용자에게 알리고 저장소에 대한 수정 사항이 포함된 PR을 자동으로 엽니다.

다음은 Snyk이 오픈한 수정 PR의 예입니다.

![](<../.gitbook/assets/mceclip0 (1).png>)

특정 프로젝트에 대한 PR 테스트 설정을 변경하려면 **Org** > **settings** ![](../.gitbook/assets/cog\_icon.png) > **Integrations > Edit Settings**로 이동하십시오.

![](../.gitbook/assets/automatic.png)

개발자가 패치 사용 및 실행 방법을 잘 모를 경우 자동 수정 PR에서 패치를 제외하는 것이 좋습니다.

개발자는 자동 수정 PR에 나타나는 merge advice를 고려해야 합니다:

![](<../.gitbook/assets/merge-advice-review-recommended (2) (2) (2) (22).png>)

![](<../.gitbook/assets/advice-green (1) (2) (2) (4) (3) (14).png>)

![](<../.gitbook/assets/merge-advice (2) (2) (4) (2) (1) (20).png>)

{% hint style="info" %}
Snyk 자동 수정 PR은 새로운 문제에 대해서만 생성됩니다.
{% endhint %}

~~**\*\*수정필요**~~ SCM이 Github이고 Snyk Broker를 사용하지 않는 경우 기본적으로 Snyk는 모든 Org 사용자의 자격 증명을 순환하여 자동 수정 PR을 엽니다. 필요한 경우 이 설정을 변경하고 사용자 자격 증명을 설정하여 자동 수정 PR을 열 수 있습니다. 자세한 내용은 [pening fix and upgrade pull requests from a fixed GitHub account](https://docs.snyk.io/integrations/git-repository-scm-integrations/opening-fix-and-upgrade-pull-requests-from-a-fixed-github-account)를 참조하십시오.

## 6단계: 디펜던시 업그레이드 PRs

그룹이 ~~**보안 기술 부채 문제**~~를 해결할 준비가 되면 종속성을 업그레이드하기 위해 사용자 대신 PR(Pull Request)을 자동으로 생성하도록 Snyk를 구성할 수 있습니다.

![](../.gitbook/assets/upgrade-node-uuid.png)

**How it works**

1. SCM과 통합을 한 후 사용자가 자동 업그레이드 PR을 사용 가능으로 설정합니다.
2. Snyk scans your projects as you import them and continues to monitor your projects, scanning on a regular basis.
3. For each scan, when Snyk identifies new versions for your dependencies:
   * Snyk creates automatic upgrade PRs (frequency based on Snyk project settings)
   * Snyk will not open a new upgrade PR for a dependency that is already changed (upgraded or patched) in another open Snyk PR.
   * Snyk opens separate PRs for each dependency.
   * Snyk will not create upgrade PRs for a repo that has 5 or more Snyk PRs open - if the limit of open PRs is reached, no new ones are created. This number can set to between 1-10 from the Settings. This limit only applies when creating upgrade PRs, but does count fix PRs. Fix PRs are not limited in this way.
   * By default, Snyk recommends only patch and minor upgrades, but major version upgrade can be enabled in the settings where the feature is enabled.
   * If the latest eligible version contains vulnerabilities not already found in your project, Snyk will not recommend an upgrade.
   * Snyk does not recommend upgrades to versions that are less than 21 days old. This is to avoid versions that introduce functional bugs and subsequently get unpublished, or versions that are released from a compromised account (where the account owner has lost control to someone with malicious intent).

**Supported languages and repos**

Snyk currently supports this feature for npm, Yarn and Maven-Central projects through GitHub, GitHub Enterprise Server and BitBucket Cloud, including use of the Snyk Broker. For use with the Broker, your admin should first upgrade to v4.55.0 or later.

**Enable automatic dependency upgrade PRs for a specific project**

To set PR Settings on the project level, overriding the PR settings on the organization level

1. Navigate to the organization for which you would like to enable automatic upgrade PRs
2. Click **Projects**.
3.  Navigate to the relevant project and click the **Settings** cog:

    ![](<../.gitbook/assets/image (56) (2) (3) (3) (3) (3) (4) (5) (5) (5) (5) (3) (1) (7).png>)
4. From the Settings area, click on the integration settings from the left panel menu to apply unique settings for that one project.
5. From settings that load, scroll to the **Automatic dependency upgrade pull requests** and click Disabled.
6. From the options that appear:
   1. Snyk creates PRs up to a maximum of 10 open simultaneously - per repo. To limit this number further, select the maximum number of PRs from the dropdown list. For more details, see [Upgrading dependencies with automatic PRs](https://docs.snyk.io/snyk-open-source/dependency-management/upgrading-dependencies-with-automatic-prs).
   2. In the Dependencies to ignore field, enter the exact name of any dependencies that should not be handled as part of the automatic functionality. This field accepts only lower case letters.
   3. Once you click ‘Upgrade dependency settings’ every time Snyk scans this project, it will automatically submit upgrade PRs based on results. If a newer version is released for an existing Snyk upgrade PR or for an existing fix PR, the existing PR must be closed or merged before Snyk can raise a new PR.

![](../.gitbook/assets/general-github\_integration.png)
