# Snyk SCM 통합: 모범 사례

Snyk을 SCM(Source Control Manager)과 통합하여 모든 프로젝트를 빠르고 쉽게 파악할 수 있습니다.

[Snyk SCM integrations](snyk-scm-integration-good-practices.md)를 통해 다음을 수행할 수 있습니다.

* 모든 통합 저장소에서 보안 검색 연속 수행
* 오픈 소스 구성 요소의 취약점 탐지
* 자동화된 수정 기능 제공

## 권장 배포 순서

팀이 원활하게 배포하려면 각 통합에 대해 아래에 설명된 단계를 따르십시오.

모든 SCM 통합 기능을 동시에 구현하려고 할 경우 [SDLC](https://snyk.io/learn/secure-sdlc/)에서 마찰을 일으킬 위험이 있으며, 이로 인해 개발자 환경이 저하될 수 있습니다.

| **Deployment Stages**                                                                                                  | **Configurations**                                                                                                                                             | **Outcome**                                     |
| ---------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------- |
| <p><a href="snyk-scm-integration-good-practices.md">Stage 1</a></p><p>SCM 통합 설정</p>                                    | [SCM integration](./)에 대한 구성 문서를 참조하십시오.                                                                                                                       | 구성된 통합, 프로젝트를 가져올 준비가 됨                         |
| <p><a href="snyk-scm-integration-good-practices.md">Stage 2</a></p><p>SCM에서 모든 프로젝트를 가져오기</p>                          | <p>- 공용 및 개인 리포지토리 모두 테스트</p><p>- 모든 사용자 알림 사용 안 함</p><p>- Snyk PR 검사 사용 안 함</p><p>- 자동 수정 PR 사용 안 함</p><p>- 실패한 PR 검사 사용 안 함</p><p>- 자동 디펜던시 업그레이드 사용 안 함</p> | 애플리케이션 전반에 걸쳐 위험을 평가할 수 있는 자료입니다.               |
| <p><a href="snyk-scm-integration-good-practices.md">Stage 3</a></p><p>개발자 및 보안 팀은 Snyk 우선 순위 보고 기능을 사용하여 수정 계획을 수립</p> | 자세한 내용을 확인하려면 [여기](https://www.youtube.com/watch?v=\_kAY94JwQHY)를 클릭하십시오.                                                                                      | 수정할 내용과 수정 프로세스를 간소화할 시기에 대한 개발자와 보안 간의 조정      |
| <p><a href="snyk-scm-integration-good-practices.md">Stage 4</a></p><p>개발자에게 실시간으로 문제를 알리고 사용 가능한 수정 사항을 교육</p>         | - Snyk PR 검사를 사용하도록 설정하고 사용 가능한 수정과 함께 심각도가 높은 문제가 포함된 경우 PR을 실패시킵니다.  - 자동 수정 PR을 사용합니다.                                                                      | 조직의 평균 수정 시간(MTTF)을 개선합니다.                      |
| <p><a href="snyk-scm-integration-good-practices.md">Stage 5</a></p><p>개발자가 새로운 취약점을 도입하지 못하도록 방지</p>                   | - 실패한 PR 검사를 사용하도록 설정합니다. 심각도가 높은 문제(수정 또는 수정 없음)입니다.                                                                                                          | ‘Secure by Design’ 방법론 달성                       |
| <p><a href="snyk-scm-integration-good-practices.md">Stage 6</a></p><p>기술 보안 부채 감소</p>                                  | - 자동 디펜던시 업그레이드를 사용하도록 설정합니다.                                                                                                                                  | 연구 및 해결에 많은 시간이 소요될 수 있는 미래의 설계 문제 및 핫픽스를 줄입니다. |

## 1단계 : SCM 통합 설정

Snyk은 GitHub, GitHub Enterprise, Bitbucket Cloud 등을 포함한 SCM을 위한 사전 구축된 통합 기능을 보유하고 있습니다. 전체 목록은 [GIT repository (SCM) integrations](https://support.snyk.io/hc/en-us/sections/360001138098-Git-repository-SCM-integrations)를 참조하십시오.

조직에 대해 SCM이 이미 구성되어 있는지 확인하려면 **Integrations** 탭으로 이동합니다. 구성된 SCM이 **Configured**으로 표시됩니다.

![](../../../.gitbook/assets/int1.png)

{% hint style="info" %}
SCM이 이미 구성된 경우 다음 단계로 이동합니다.
{% endhint %}

## 예시: GitHub

다음은 **Github.com**에 대한 통합을 설정하는 방법의 예시입니다.

1. **Integrations** 탭으로 이동하여 **GitHub**를 클릭합니다.
2. Snyk에게 공용 및 개인 저장소 모두에 대한 액세스 권한을 부여할지 또는 공용 저장소에만 대한 액세스 권한을 부여할지 선택하십시오.
3. **Authorize snyk**을 클릭하여 Snyk에게 저장소에 대한 액세스 권한을 제공합니다.

![](<../../../.gitbook/assets/spaces\_-MdwVZ6HOZriajCf5nXH\_uploads\_git-blob-efdd6cdac1096e497ea4265a39fc48655b3d3742\_authorize (1) (2) (6) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (21).png>)

**저장소에 대한 SCM 사용 권한**

Snyk UI를 사용하여 트리거된 작업(Fix PR 열기 또는 프로젝트 다시 테스트)은 acting user에 대해 수행됩니다. 따라서 이러한 작업을 수행하려면 자신의 SCM 사용자 또는 서비스 계정을 연결해야 합니다. 이렇게 하면 Snyk는 이러한 작업을 수행할 저장소에 대해 필요한 권한을 부여합니다.

예를 들어 GitHub에서 Snyk에 연결된 계정은 대상 저장소에 대해 다음과 같은 액세스 권한이 필요합니다.

| **Action**                                              | **Why?**                                                                                   | **Required permissions on the repository** |
| ------------------------------------------------------- | ------------------------------------------------------------------------------------------ | ------------------------------------------ |
| **Daily / weekly tests**                                | 개인 저장소에서 매니페스트 파일 읽기                                                                       | _**Write**_ or above                       |
| **Snyk tests on pull requests**                         | 새 PR이 생성되거나 기존 PR이 업데이트될 때마다 pull request status 전송                                        |                                            |
| **Opening fix and upgrade pull requests**               | 모니터링하는 저장소에 수정/업그레이드 PR 생성                                                                 |                                            |
| **Snyk tests on pull requests - initial configuration** | 가져온 저장소에 Snyk의 webhooks를 추가하면 pull requests가 생성되거나 업데이트될 때마다 Snyk이 알림을 받고 검색을 트리거할 수 있습니다. | _**Admin**_                                |

### 알림 설정 변경

기본적으로 Snyk은 프로젝트의 디펜던시에서 새로운 이슈 또는 수정 사항이 발견되면 모든 조직 사용자에게 이메일을 보내 조직 전체의 보안 상태에 대한 매주 업데이트를 제공합니다. 많은 프로젝트를 조직으로 가져오려는 경우 사용자에게 너무 많은 이메일 알림이 전송되지 않도록 해당 조직에 대한 모든 알림을 비활성화하십시오.

조직 사용자가 수신하는 이메일을 사용자 정의하려면 조직의 settings ![](../../../.gitbook/assets/cog\_icon.png) > **Notifications**으로 이동하십시오. 여기서 변경한 내용은 조직의 모든 구성원에 영향을 미치지만, 조직 사용자는 사용자 수준 계정 설정에서 이러한 기본 설정을 무시할 수 있습니다.

가져오기 전에 조직의 모든 사용자에 대한 notification을 실행 중지하려면 해당 notification box의 선택을 취소합니다.

![](<../../../.gitbook/assets/image (58).png>)

자세한 내용은 [Notification management](https://support.snyk.io/hc/en-us/articles/360004037657-Notification-management)를 참조하십시오.

## 2단계: 프로젝트 가져오기

1. Snyk UI에서 **Projects** 페이지로 이동하여 **Add projects**를 선택하고 Snyk으로 가져올 저장소를 선택한 다음 **Add selected repositories**를 클릭합니다.
2. Snyk은 전체 디렉토리 트리에서 선택한 저장소에서 디펜던시 파일(예: **package.json**)을 검색하고 이러한 파일을 프로젝트로 가져옵니다.
3. Snyk은 루트 폴더와 정의된 사용자 지정 파일 위치를 평가합니다. 매니페스트 또는 구성 파일을 찾을 수 없으면 파일을 가져올 수 없다는 알림 메시지가 표시됩니다.
4. Snyk은 매니페스트 파일(프로젝트)을 탐지하고 테스트한 다음 결과를 표시합니다. 가져온 프로젝트는 저장소 이름 아래에 나타납니다.

![](../../../.gitbook/assets/int3.png)

(프로젝트를 가져온 후 지속적으로 취약점 확인)

5\. 프로젝트를 가져왔는지 확인하려면 페이지로 이동합니다. 가져온 프로젝트에는 저장소 이름의 ✔ 아이콘이 있습니다.

![](../../../.gitbook/assets/aws-sdk.png)

## 3단계: PR에서 Snyk 테스트 활성화

**PR 테스트 설정 및 워크플로우**

기본적으로 Sny은 모니터링하는 저장소에 제출된 모든 pull request를 검사하여 단일 보안 검사와 단일 라이선스 검사로 그룹화된 결과 및 권장 사항을 표시합니다.

![](../../../.gitbook/assets/checks-passed.png)

**상태 세부 정보**

"Details" 링크를 클릭하면 Snyk checks에 다음과 같은 상태가 나타날 수 있습니다.

* **Success**: 문제가 식별되지 않고 모든 검사가 통과됨
* **Processing**: 이 상태는 Snyk test가 끝날 때까지 표시됩니다.
* **Failure**: 검사를 통과하기 위해 수정해야 하는 문제가 식별된 경우
* **Error**: 매니페스트 파일이 동기화되지 않았거나, Snyk이 매니페스트 파일을 읽을 수 없거나, Snyk이 매니페스트 파일을 찾을 수 없을 때 오류가 발생합니다.

![](../../../.gitbook/assets/security-check.png)

**PR 테스트 설정 관리**

관리자는 조직 수준에서 Snyk PR 테스트 설정을 관리하여 모든 프로젝트에 적용하거나 PR 테스트를 적용할 특정 프로젝트를 선택할 수 있습니다. 기능이 켜져 있는지 여부를 구성하고(기본적으로 활성화됨), 실패 조건을 설정하여 Snyk가 PR 검사를 통과하지 못할 시기를 정의할 수 있습니다.

조직의 PR 테스트 설정을 구성하려면 다음과 같이 진행합니다.

1. **Org** > settings ![](../../../.gitbook/assets/cog\_icon.png) **>** Integrations > Edit Settings로 이동합니다.
2. 토글을 **Enabled**로 설정하고 필요에 따라 **Fail conditions**을 설정합니다.
3. **Update settings**를 클릭합니다.

![](../../../.gitbook/assets/image13.png)

특정 프로젝트에 대한 pull request 테스트 설정을 구성하려면 **Projects Page**> **Projects Settings > Edit Settings**로 이동하고 다음과 유사하게 조건을 설정합니다.

![](../../../.gitbook/assets/main.png)

{% hint style="info" %}
라이선스 정책을 사용하면 Snyk이 라이선스 문제로 PR에 실패하는 것을 방지할 수 있습니다. 자세한 내용은 [License policies](https://support.snyk.io/hc/en-us/sections/360002249578-License-Policies)를 참조하십시오.
{% endhint %}

**초기 단계: 가시성 확보 및 실패 조건 설정**

롤아웃을 시작할 때는 Snyk이 PR을 테스트하는 것부터 시작하는 것이 좋습니다. 따라서 개발자는 Snyk 커밋 확인에 익숙해질 것입니다.

1. 조직 수준 또는 특정 프로젝트에 이 옵션을 적용하기로 결정합니다.
2. 위의 설명에 따라 조건을 설정합니다.
   * **PR이 이슈에 대한 디펜던시를 추가하는 경우**에만 **실패**합니다.
   * **심각도가 높은 문제에 대해서만 실패** 및 발견된 문제에 대해 **사용 가능한 수정 사항이 있는 경우에만 실패 확인**란을 선택합니다.

## 4단계: PR 차단 활성화

SDLC에 Snyk을 내장하고 좋은 개발자 인식을 구축한 후에는 보다 엄격한 정책을 적용하여 전반적인 보안 상태를 개선할 수 있습니다.

* **Low priority projects**: 수정 가능한 높은 새 심각도에 대해서만 PR을 실패할 수 있습니다.
* **Medium priority projects**: 심각도가 높은 문제에 대해서만 PR에 실패합니다.
* **High priority projects (PCI/GDPR compliance)**: 모든 문제에 대해 PR 실패

{% hint style="info" %}
취약점 심각도를 내부 정책과 일치시키려면 보안 정책을 사용하여 문제의 심각도를 변경하고 관련 프로젝트 특성에 연결합니다. 자세한 내용은 [Security policies](https://docs.snyk.io/features/fixing-and-prioritizing-issues/security-policies)를 참조하십시오.
{% endhint %}

## 5단계: 자동 수정 PR

Snyk은 매일 또는 매주 프로젝트를 스캔합니다. 새로운 취약점이 발견되면 Snyk은 이메일로 알려주고 저장소에 대한 수정 사항이 포함된 자동화된 PR을 엽니다.

다음은 Snyk에 의해 열린 수정 pull request의 예시입니다.

![](<../../../.gitbook/assets/mceclip0 (1).png>)

특정 프로젝트에 대한 PR 테스트 설정을 구성하려면 **Org** > settings ![](../../../.gitbook/assets/cog\_icon.png) > **Integrations > Edit Settings**로 이동합니다.

![](../../../.gitbook/assets/automatic.png)

개발자가 패치를 사용하고 실행하는 방법을 잘 모르는 경우 자동 수정 PR에서 패치를 제외하는 것이 좋습니다.

개발자에게 자동 수정 PR에 표시되는 merge advice label을 고려하도록 요청해야 합니다.

![](<../../../.gitbook/assets/spaces\_-MdwVZ6HOZriajCf5nXH\_uploads\_git-blob-0e0d25e7a674ee3035929bcf1be3a7073a1fc53c\_merge-advice-review-recommended (2) (2) (2) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (24).png>)

![](<../../../.gitbook/assets/spaces\_-MdwVZ6HOZriajCf5nXH\_uploads\_git-blob-75bc3b2514154caac478a306c5c64e803d39b40d\_advice-green (1) (2) (2) (4) (3) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (14).png>)

![](<../../../.gitbook/assets/spaces\_-MdwVZ6HOZriajCf5nXH\_uploads\_git-blob-0f8580a273102ad122374c855d6db17b7c33a7a3\_merge-advice (2) (2) (4) (2) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (20).png>)

{% hint style="info" %}
Snyk 자동 수정 PR은 새 이슈에 대해서만 생성됩니다.
{% endhint %}

SCM이 Github이고 Snyk Broker를 사용하지 않는 경우 기본적으로 Snyk은 모든 조직 사용자의 인증 정보를 교체하여 자동 수정 PR을 엽니다. 필요한 경우 이를 변경할 수 있으며 사용자 인증 정보를 설정하여 자동 수정 PR을 열 수 있습니다. 자세한 내용은 [Opening fix and upgrade pull requests from a fixed GitHub account](https://docs.snyk.io/integrations/git-repository-scm-integrations/opening-fix-and-upgrade-pull-requests-from-a-fixed-github-account)를 참조하십시오.

## 6단계: 디펜던시 업그레이드 PR

그룹이 보안 기술 채무 해결을 시작할 준비가 되면 디펜던시를 업그레이드하기 위해 사용자 대신 PR(Pull Request)을 자동으로 생성하도록 Snyk을 구성할 수 있습니다.

![](../../../.gitbook/assets/upgrade-node-uuid.png)

**How it works**

1. 통합이 구성되고 사용자가 자동 업그레이드 PR을 활성화합니다.
2. Snyk은 프로젝트를 가져올 때 프로젝트를 검사하고 정기적으로 검사하면서 프로젝트를 계속 모니터링합니다.
3. 각 스캔에 대해 Snyk이 디펜던시에 대한 새 버전을 식별할 때 다음을 수행합니다.
   * Snyk은 자동 업그레이드 PR을 생성합니다(Snyk 프로젝트 설정에 따른 빈도).
   * 다른 열린 Snyk PR에서 이미 변경(업그레이드 또는 패치 적용)된 디펜던시에 대해 Snyk은 새 업그레이드 PR을 열지 않습니다.
   * Snyk은 각 디펜던시에 대해 별도의 PR을 엽니다.
   * Snyk은 5개 이상의 Snyk PR이 열려 있는 저장소에 대해 업그레이드 PR을 만들지 않습니다. 열린 PR의 제한에 도달하면 새 PR이 생성되지 않습니다. 이 숫자는 설정에서 1-10 사이로 설정할 수 있습니다. 이 제한은 업그레이드 PR을 생성할 때만 적용되지만 수정 PR은 카운트됩니다. 수정 PR은 이러한 방식으로 제한되지 않습니다.
   * 기본적으로 Snyk은 패치 및 minor 업그레이드만 권장하지만 major 버전 업그레이드는 이 기능이 활성화된 설정에서 활성화할 수 있습니다.
   * 해당 최신 버전에 프로젝트에 아직 발견되지 않은 취약점이 있는 경우 Snyk는 업그레이드를 권장하지 않습니다.
   * 출시한지 21일 미만의 버전에는 업그레이드를 권장하지 않습니다. 이는 기능적 버그가 발생하여 나중에 게시되지 않는 버전이나 손상된 계정에서 릴리스된 버전(계정 소유자가 악의적인 의도를 가진 사람에게 제어 권한을 빼앗긴 버전)을 방지하기 위한 것입니다.

**지원하는 개발 언어 및 저장소**

Snyk은 현재 GitHub, GitHub Enterprise Server 및 BitBucket Cloud를 통해 npm, Yarn 및 Maven-Central 프로젝트에 해당 기능을 지원합니다. 브로커와 함께 사용하려면 관리자가 먼저 v4.55.0 이상으로 업그레이드해야 합니다.

**특정 프로젝트에 대한 자동 디펜던시 업그레이드 PR 실행**

프로젝트 수준에서 PR을 설정하려면 조직 수준에서 PR 설정을 재정의합니다.

1. 자동 업그레이드 PR을 사용할 조직으로 이동합니다.
2. **Projects**를 클릭합니다.
3.  관련 프로젝트로 이동하여 **Settings**를 클릭합니다.

    <img src="../../../.gitbook/assets/spaces_-MdwVZ6HOZriajCf5nXH_uploads_git-blob-82e957b854af6179585ebbbf4b503c1a9863a054_image (56) (2) (3) (3) (3) (3) (4) (5) (5) (5) (5) (3) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt="" data-size="original">
4. Settings 영역의 왼쪽 패널 메뉴에서 integration settings를 클릭하여 해당 프로젝트에 고유한 설정을 적용합니다.
5. 나타나는 설정에서 **Automatic dependency upgrade pull requests**로 이동하고 Disabled를 클릭합니다.
6. 표시되는 옵션에서 다음 작업을 수행합니다.
   1. Snyk은 저장소당 최대 10개의 PR을 동시에 생성합니다. PR을 추가로 제한하려면 드롭다운 목록에서 최대 PR 수를 선택합니다. 자세한 내용은 [Upgrading dependencies with automatic PRs](https://docs.snyk.io/snyk-open-source/dependency-management/upgrading-dependencies-with-automatic-prs)를 참조하십시오.
   2. 무시할 디펜던시 필드에 자동 기능으로 처리해서는 안 되는 디펜던시의 정확한 이름을 입력합니다. 이 필드에는 소문자만 사용할 수 있습니다.
   3. Snyk에서 이 프로젝트를 검색할 때마다 ‘Upgrade dependency settings’를 클릭하면 결과에 따라 업그레이드 PR이 자동으로 제출됩니다. 기존 Snyk 업그레이드 PR 또는 기존 수정 PR에 대해 최신 버전이 릴리스된 경우 기존 PR을 닫거나 병합해야 Snyk가 새 PR을 올릴 수 있습니다.

![](../../../.gitbook/assets/general-github\_integration.png)
