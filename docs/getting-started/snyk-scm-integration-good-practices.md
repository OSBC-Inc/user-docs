# Snyk SCM 통합: 모범 사례

Snyk을 SCM(Source Control Manager)과 통합하여 모든 프로젝트를 쉽고 빠르게 파악할 수 있습니다.

Snyk SCM 통합을 통해 다음을 수행할 수 있습니다:

* 통합된 모든 저장에 대한 지속적인 보안 스캐닝 수행
* 오픈소스 컴포넌트의 취약성 탐지
* 자동 수정 기능 제공

## 권장하는 배포 순서

각 통합에 대한 원활한 배포를 위해 아래에 설명된 단계를 따르십시오.

모든 SCM 통합 기능을 동시에 구현하려고 하면 SDLC에 문제가 발생하여 개발 성능이 저하될 위험이 있습니다.

| **배포 단계**                                                                                                              | **구성**                                                                                                                                              | 결과                                                        |
| ---------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------- |
| <p><a href="snyk-scm-integration-good-practices.md">1단계</a></p><p>SCM 통합을 설정합니다.</p>                                   | 각 [SCM integration](../features/integrations/git-repository-scm-integrations/)에 대한 구성 설명서 참조                                                        | 프로젝트를 가져올 준비가 된 구성된 통합                                    |
| <p><a href="snyk-scm-integration-good-practices.md">2단계</a></p><p>SCM에서 모든 프로젝트를 가져옵니다.</p>                            | <p>- 공용 및 개인 리포지토리 모두 테스트</p><p>- 모든 사용자 알림 비활성화</p><p>- Snyk PR 검사 비활성화</p><p>- 자동 수정 PR 비활성화</p><p>- 실패한 PR 검사 비활성화</p><p>- 자동 종속성 업그레이드 비활성화</p> | 애플리케이션 전체의 위험을 평가할 수 있는 완전한 소프트웨어 BOM(Bill of Materials)  |
| <p><a href="snyk-scm-integration-good-practices.md">3단계</a></p><p>개발자 및 보안 팀은 Snyk의 우선순위 보고 기능을 사용하여 수정 계획을 수립합니다.</p> | Snyk 우선순위 보고에 대해 자세히 알아보려면 [여기](https://www.youtube.com/watch?v=\_kAY94JwQHY)를 클릭하십시오.                                                              | 수정해야 할 사항과 수정 프로세스를 합리화하는 시기를 개발자 및 보안 팀간에 조정합니다.         |
| <p><a href="snyk-scm-integration-good-practices.md">4단계</a></p><p>개발자에게 실시간으로 문제를 경고하고 수정 가능한 사항에 대해 알려줍니다.</p>        | <p>- Enable Snyk PR checks and fail PRs</p><p>if they contain High severity issues</p><p>with available fixes</p><p>- Enable Auto-fix PRs</p>       | 조직이 취약점을 더 빠르게 수정할 수 있습니다.                                |
| <p><a href="snyk-scm-integration-good-practices.md">5단계</a></p><p>개발자가 새로운 취약점을 들어오지 못하도록 방지합니다.</p>                   | <p>- Enable Failing PR checks, for ANY</p><p>High severity issues (fix or no fix)</p>                                                               | ‘Secure by Design’ 방법론을 달성했습니다.                           |
| <p><a href="snyk-scm-integration-good-practices.md">6단계</a></p><p>기술 보안 부채 구축</p>                                      | - 자동 디펜던시 업그레이드 사용                                                                                                                                  | 연구 및 해결에 시간이 많이 소요될 수 있는 향후 설계 문제 및 긴급한 수정 사항을 줄일 수 있습니다. |

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

**저장소에 대한 SCM 사용 권한**

Snyk과 작업을 수행할 저장소에 대한 권한을 갖게하여 작업 중인 사용자에 대해 Snyk UI를 사용하여 트리거된 작업(예: 수정 PR 열기 또는 프로젝트 다시 테스트)이 수행됩니다. 이러한 작업을 수행하려면 자신의 SCM 사용자 또는 서비스 계정을 연결해야 합니다.

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

기본적으로 Snyk은 모니터링하는 저장소에 제출된 모든 pull request를 검색하여 결과와 권장 사항을 단일 보안 검사와 단일 라이선스 검사로 그룹화하여 제공합니다.

![](../.gitbook/assets/checks-passed.png)

**상태 세부 정보**

"Details" 링크를 클릭하면 Snyk 검사에서 다음과 같은 상태가 나타날 수 있습니다:

* **Success**: 식별된 문제가 없고 모든 점검이 통과됨
* **Processing**: Snyk 테스트가 끝날 때까지 표시됨
* **Failure**: 문제가 확인되었을 때, 검사를 통과하기 위한 수정 필요
* **Error**: 매니페스트 파일이 동기화되지 않았거나, Snyk이 매니페스트 파일을 읽을 수 없거나, Snyk과 매니페스트 파일을 찾을 수 없을 때 오류가 발생합니다.

![](../.gitbook/assets/security-check.png)

**PR 테스트 설정 관리**

관리자는 조직 수준에서 Snyk PR 테스트 설정을 관리하여 모든 프로젝트에 적용하거나 PR 테스트를 적용할 특정 프로젝트를 선택할 수 있습니다. 기능의 설정 여부(기본적으로 활성화됨)를 구성하고, 실패 조건을 설정하여 Snyk이 PR 검사를 통과하지 못할 시기를 정의할 수 있습니다.

조직의 PR 테스트 설정을 구성하려면 다음과 같이 하십시오.

1. **Org** > settings ![](../.gitbook/assets/cog\_icon.png) **>** Integrations > Edit Settings 이동
2. **Enabled**로 설정하고 필요에 따라 **Fail conditions** 설정합니다.
3. **Update settings**를 클릭합니다.

![](../.gitbook/assets/image13.png)

특정 프로젝트에 대한 pull request를 설정하려면 **Projects Page**> **Projects Settings > Edit Settings**로 이동하여 조건을 비슷하게 설정하십시오.

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
   * **예) Only fail when the issues found have a fix available** : 발견된 문제에 수정 가능한 사항이 있는 경우에만 실패

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

개발자는 자동 수정 PR에 나타나는 merge advice를 고려해야 합니다.

![](<../.gitbook/assets/merge-advice-review-recommended (2) (2) (2) (22).png>)

![](<../.gitbook/assets/advice-green (1) (2) (2) (4) (3) (14).png>)

![](<../.gitbook/assets/merge-advice (2) (2) (4) (2) (1) (20).png>)

{% hint style="info" %}
Snyk 자동 수정 PR은 새로운 문제에 대해서만 생성됩니다.
{% endhint %}

당신의 SCM이 Github이고 Snyk Broker를 사용하지 않는 경우 기본적으로 Snyk는 모든 Org 사용자의 인증 정보을 확인하여 자동 수정 PR을 엽니다. 필요한 경우 이 설정을 변경하고 사용자 인증 정보를 설정하여 자동 수정 PR을 열 수 있습니다. 자세한 내용은 [Opening fix and upgrade pull requests from a fixed GitHub account](../features/integrations/git-repository-scm-integrations/opening-fix-and-upgrade-pull-requests-from-a-fixed-github-account.md)를 참조하십시오.

## 6단계: 디펜던시 업그레이드 PRs

그룹이 \~\~**보안 기술 부채 문제**\~\~를 해결할 준비가 되면 디펜던시를 업그레이드하기 위해 사용자 대신 PR(Pull Request)을 자동으로 생성하도록 Snyk을 구성할 수 있습니다.

![](../.gitbook/assets/upgrade-node-uuid.png)

**작동 방식**

1. SCM과 통합을 한 후 사용자가 자동 업그레이드 PR을 사용 가능으로 설정합니다.
2. Snyk은 프로젝트를 가져오면서 스캔을 하고 정기적으로 프로젝트를 계속 모니터링합니다.
3. 각각을 모니터링할 때, Snyk이 디펜던시에 대한 새 버전을 식별하면 다음과 같이 수행합니다:
   * Snyk은 자동 업그레이드 PR을 생성합니다.(Snyk 프로젝트 설정의 테스트 빈도 기반)
   * Snyk은 열려 있는 다른 Snyk PR에서 이미 변경(업그레이드 또는 패치 적용)된 디펜던시에 대해 새 업그레이드 PR을 열지 않습니다.
   * Snyk은 각 디펜던시에 대해 별도의 PR을 생성합니다.
   * Snyk은 5개 이상의 Snyk PR이 열려 있는 저장소에 대해 업그레이드 PR을 생성하지 않습니다. 이 숫자는 설정에서 1\~10 사이로 설정할 수 있습니다. 이 제한은 업그레이드 PR을 생성할 때만 적용되지만 수정 PR 수는 계산되지 않습니다. 따라서 수정 PR은 이러한 방식으로 제한되지 않습니다.
   * 기본적으로 Snyk은 패치 및 부분 업그레이드만 권장하지만 기능이 활성화된 설정에서 major 버전 업그레이드를 활성화할 수 있습니다.
   * 적용 가능한 최신 버전의 프로젝트에서 아직 발견되지 않은 취약점이 포함되어 있는 경우 Snyk은 업그레이드를 권장하지 않습니다.
   * Snyk은 21일 미만의 버전에는 업그레이드를 권장하지 않습니다. 이는 기능적인 버그를 도입했다가 나중에 게시되지 않은 버전이나 손상된 계정(계정 소유자가 악의적인 의도를 가진 사람에게 제어권을 빼앗긴 경우)에서 릴리즈되는 버전을 피하기 위함입니다.

**지원되는 언어 및 저장소**

npm, Yarn and Maven-Central projects through GitHub, GitHub Enterprise Server and BitBucket Cloud, including use of the Snyk Broker. Broker와 함께 사용하려면 관리자가 먼저 v4.55.0 이상으로 업그레이드를 해야 합니다.

**특정 프로젝트에 대해 자동 디펜던시 업그레이드 PR 사용**

프로젝트 수준에서 PR 설정을 설정하려면 조직 수준에서 PR 설정을 재지정하십시오.

1. 자동 업그레이드 PR을 사용할 조직으로 이동합니다.
2. **Projects**를 클릭하세요.
3.  관련 프로젝트로 이동하고 **Settings** 톱니바퀴 아이콘을 클릭합니다.

    ![](<../.gitbook/assets/image (56) (2) (3) (3) (3) (3) (4) (5) (5) (5) (5) (3) (1) (7).png>)
4. 설정 영역의 왼쪽 패널 메뉴에서 통합 설정을 클릭하여 해당 프로젝트에 고유한 설정을 적용합니다.
5. **Automatic dependency upgrade pull requests**로 스크롤하고 Disabled를 클릭합니다.
6. 표시되는 옵션:
   1. Snyk은 저장소마다 최대 10개의 PR을 동시에 생성할 수 있습니다. 이 수를 추가로 제한하려면 드롭다운 목록에서 최대 PR 수를 선택합니다. 자세한 내용은 [Upgrading dependencies with automatic PRs](https://docs.snyk.io/snyk-open-source/dependency-management/upgrading-dependencies-with-automatic-prs)를 참조하십시오.
   2. Dependencies to ignore 필드에 자동 기능의 일부로 처리되지 않는 디펜던시의 정확한 이름을 입력합니다. 이 필드에는 소문자만 사용할 수 있습니다.
   3. 프로젝트를 모니터링할 때마다 ‘Upgrade dependency settings’를 클릭하면 결과에 따라 업그레이드 PR이 자동으로 제출됩니다. 기존 Snyk 업그레이드 PR 또는 기존 수정 PR에 대해 최신 버전이 릴리즈된 경우 기존 PR을 closed 하거나 merge해야 Snyk이 새 PR을 생성할 수 있습니다.

![](../.gitbook/assets/general-github\_integration.png)
