# GitHub 통합

Snyk의 GitHub 통합을 통해 모든 통합 저장소에서 보안 스캔을 지속적으로 수행하고, 오픈 소스 구성 요소의 취약점을 탐지하고, 자동화된 수정 프로그램을 제공할 수 있습니다.

**GitHub은 조직이 아닌 사용자별로 통합됩니다**. 이 통합을 설정하면 계정과 연결된 모든 조직에서 통합이 사용됩니다.

{% hint style="warning" %}
GitHub 통합에서 **Personal Access Token**을 사용하면 PR을 열 수 있지만 프로젝트를 가져올 수는 없습니다. [Personal Access Token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)을 사용하여 프로젝트 가져오기를 설정하려면 [GitHub Enterprise 통합](github-enterprise-integration.md)을 사용하십시오.
{% endhint %}

## GitHub 통합 설정

1. Integrations 페이지로 이동하여 “GitHub”를 클릭합니다.
2. Snyk에게 공용 및 개인 저장소 모두에 대한 액세스 권한을 부여할지 아니면 공용 저장소에만 액세스할 수 있도록 할지 선택하십시오.
3. GitHub 인증 화면이 열리면 "Authorize snyk"을 클릭하여 저장소에 대한 액세스를 제공합니다.
4. Snyk으로 가져올 저장소를 선택하십시오. 완료되면 페이지 상단에 있는 **Add selected repositories** 버튼을 클릭합니다. 클릭하면 Snyk이 선택한 저장소에서 전체 디렉터리 트리의 의존성 파일(package.json, pom.xml 등)을 검색하고 프로젝트로 가져옵니다.
5. 가져온 프로젝트가 Projects 페이지에 나타나고 취약점을 지속적으로 검사합니다.

![](<../../../.gitbook/assets/spaces\_-MdwVZ6HOZriajCf5nXH\_uploads\_git-blob-8b3be1cd3d5f4117327c067a1b1c17761b08c9b0\_which\_repos (3) (5) (9) (7) (18) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (27) (1) (1) (27).jpg>)

## GitHub 통합 기능

통합이 완료되면 다음과 같은 기능을 이용할 수 있습니다.

### **1.** Project level 보안 보고서

Snyk은 고급 보안 보고서를 생성하여 저장소에서 발견된 취약점을 탐색하고 필요한 업그레이드 또는 패치를 사용하여 저장소로 직접 pull request을 열어 즉시 수정할 수 있습니다.

다음은 project-level 보안 보고서의 예시입니다.

![](<../../../.gitbook/assets/mceclip0-22- (2) (5) (6) (1) (1) (1) (2).png>)

### **2.** 프로젝트 모니터링 및 자동 수정 **pull requests**

Snyk은 매일 또는 매주 프로젝트를 자주 검색합니다. 새 취약점이 발견되면 e메일을 통해 저장소에 대한 수정 사항이 포함된 pull requests를 열어 사용자에게 알립니다. 다음은 Snyk이 연 수정 pull request의 예시입니다.

![image7.png](../../../.gitbook/assets/uuid-6cfdaf0b-c349-468d-fe65-4f80bad110ea-en.png)

Snyk (Settings --> Integration --> GitHub)의 GitHub Integration Settings로 이동하여 자동 수정 pull request 설정을 검토하고 조정할 수 있습니다.

![](<../../../.gitbook/assets/mceclip4 (1) (2) (6) (7) (3) (1) (1) (2).png>)

#### 서명 커밋

Snyk의 PR에 있는 모든 커밋은 GitHub에서 확인된 사용자인 [snyk-bot@snyk.io](mailto:snyk-bot@snyk.io)에 의해 수행되며 PGP 키로 서명됩니다. 따라서 모든 Snyk PR은 GitHub에 검증된 것으로 나타나므로 개발자는 수정/업그레이드 PR이 신뢰할 수 있는 소스에 의해 생성된다는 확신을 가질 수 있습니다.

{% hint style="info" %}
이 기능은 브로커된 GitHub 통합에서 지원되지 않습니다.
{% endhint %}

### **3. Pull request** 테스트

Snyk은 저장소에 새로 생성된 pull request에서 보안 취약점을 테스트하고 GitHub에 상태 점검을 보내 pull request가 GitHub에서 직접 새로운 보안 Issue를 발생시키는지 확인합니다.

다음은 GitHub의 Pull Request 페이지에 Snyk pull request가 나타나는 방법입니다.

![](<../../../.gitbook/assets/spaces\_-MdwVZ6HOZriajCf5nXH\_uploads\_git-blob-d169f3f27aefe4eb86d28051fcdeeb9f9d4d0f84\_uuid-87113833-be79-dbe2-8860-a3f224d654c4-en (2) (2) (6) (5) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (23) (1).png>)

Snyk (Settings --> Integration --> GitHub)의 GitHub Integration **Settings**로 이동하여 pull request 테스트 설정을 검토하고 조정할 수 있습니다.

![](<../../../.gitbook/assets/mceclip5 (1) (1).png>)

## GitHub 통합에 필요한 권한 범위

### 브로커되지 않은 GitHub 통합

1. Snyk UI를 통해 트리거되는 작업(예: PR 수정 열기 또는 프로젝트 재 테스트)은 대행 사용자 대신 수행됩니다. 따라서 Snyk UI를 통해 GitHub에서 이 작업을 수행하려는 사용자는 GitHub 계정을 Snyk에 연결하고 이러한 작업을 수행하려는 저장소에 대해 필요한 권한 범위를 가지고 있어야 합니다. 자세한 내용은 **저장소에 필요한 사용 권한 범위** 섹션을 참조하십시오.
2. GitHub 계정을 Snyk에 연결하고 저장소에 필요한 사용 권한 범위를 가진 임의 Snyk 조직 구성원을 대신하여 일일/주간 테스트 및 자동 PR(수정 및 업그레이드)과 같이 UI를 통해 트리거되지 않는 작업이 수행됩니다.
3. 일부 작업(예: PR 생성)은 브로커되지 않은 공용 저장소에 대해 [snyk-bot@snyk.io](mailto:snyk-bot@snyk.io)에 의해 가끔 수행될 수 있습니다.

{% hint style="info" %}
**Note**\
Snyk 조직 관리자는 [PR을 대신해서 열 특정 GitHub 계정](opening-fix-and-upgrade-pull-requests-from-a-fixed-github-account.md)을 구성할 수 있습니다. 이 경우 Snyk는 임의의 Snyk 조직 구성원의 GitHub 계정을 사용하여 다른 모든 작업을 계속 수행합니다. 따라서 이 기능을 사용해도 사용자의 GitHub 계정을 Snyk에 연결할 필요가 없습니다.
{% endhint %}

## 중개된 GitHub 통합

UI를 통해 트리거되는 작업과 자동 작업을 모두 포함하여 모든 작업은 토큰이 브로커로 구성된 GitHub 서비스 계정을 대신하여 수행됩니다. 다음은 구성된 토큰에 필요한 액세스 범위에 대한 분류입니다.

| **동작**                            | **목**                                                                                                   | **GitHub에서 필요한 권한**                |
| --------------------------------- | ------------------------------------------------------------------------------------------------------- | ---------------------------------- |
| 일일/주간 테스트                         | 개인 저장소에서 매니페스트 파일을 읽습니다.                                                                                | _repo (all)_                       |
| 수동 수정 pull request(사용자에 의해 트리거됨)  | 모니터링하는 저장소에 수정 PR을 생성합니다.                                                                               | _repo (all)_                       |
| 자동 수정 및 업그레이드 pull request        | 모니터링하는 저장소에 수정/업그레이드 PR을 생성합니다.                                                                         | _repo (all)_                       |
| pull request에 대한 Snyk 테스트         | 새 PR이 생성되거나 기존 PR이 업데이트될 때마다 pull request 상태 확인을 보냅니다.                                                  | _repo (all)_                       |
| Snyk로 새 프로젝트 가져오기                 | 또는 "Add Projects" 화면(가져오기 팝업)에 GitHub 조직에서 사용 가능한 모든 리포지토리 목록을 표시합니다.                                   | _admin:read:org, repo (all)_       |
| pull request에 대한 Snyk 테스트 - 초기 구성 | 가져온 저장소에 Snyk의 가져온 저장소에 Snyk의 webhook을 추가하면 pull request가 생성되거나 업데이트될 때마다 Snyk이 알림을 받고 검색을 트리거할 수 있습니다. | _admin:repo\_hooks (read & write)_ |

## 저장소에 필요한 사용 권한 범위 <a href="#h_01eefvj14p8b3depeffvyvdwzj" id="h_01eefvj14p8b3depeffvyvdwzj"></a>

Snyk이 모니터링 중인 저장소에서 필요한 작업을 수행할 수 있도록 하려면 매니페스트 파일을 자주 읽고 PR을 열어야 합니다. Snyk에 직접 또는 Broker를 통해 연결된 계정은 저장소에 대해 다음과 같은 액세스 권한이 있어야 합니다.

| **동**                             | **목**                                                                                                   | **저장소에 대한 필수 권한** |
| --------------------------------- | ------------------------------------------------------------------------------------------------------- | ----------------- |
| 일일/주간 테스트                         | 개인 저장소에서 매니페스트 파일을 읽습니다.                                                                                | _Write_ or above  |
| pull request에 대한 Snyk 테스트         | 새 PR이 생성되거나 기존 PR이 업데이트될 때마다 pull request 상태 확인을 보냅니다.                                                  | _Write_ or above  |
| 수정 및 업그레이드 pull request 열기        | 모니터링하는 저장소에 수정/업그레이드 PR을 생성합니다.                                                                         | _Write_ or above  |
| pull request에 대한 Snyk 테스트 - 초기 구성 | 가져온 저장소에 Snyk의 가져온 저장소에 Snyk의 webhook을 추가하면 pull request가 생성되거나 업데이트될 때마다 Snyk이 알림을 받고 검색을 트리거할 수 있습니다. | _Admin_           |

### **1.** 고정된 GitHub 계정에서 수정 및 업그레이드 pull request 열기

Snyk을 사용하면 수정 및 업그레이드 PR을 열 특정 GitHub 계정을 구성할 수 있습니다. 구성된 계정은 PR을 여는 데만 사용됩니다. 다른 모든 작업은 여전히 GitHub 계정을 Snyk에 연결한 임의의 Snyk 조직 구성원을 대신하여 수행됩니다.

해당 기능을 사용하려면 다음 작업을 수행해야 합니다.

1. _Settings_ → _Integrations_ → _GitHub_을 클릭하여 Snyk Web UI에서 GitHub의 통합 설정 페이지를 엽니다.
2. 고정된 GitHub 계정에서 _Open fix and upgrade pull requests from a fixed GitHub_ _account_ 설정에서 toggle 버튼을 활성화합니다.
3. GitHub 2에서 개인 액세스 토큰을 만드는 방법에 대한 지침을 따르십시오. 새로 생성된 토큰을 Snyk에 제공하여 GitHub에서 작업을 수행할 수 있도록 합니다(PR 열기 등).

![](../../../.gitbook/assets/screen-shot-2020-09-29-at-21.27.30.png)

**참고 사항**

토큰을 제공하는 GitHub 계정이 Snyk로 모니터링할 저장소에 대한 _**write**_ 수준 이상의 권한을 가지고 있는지 확인하십시오.

[GitHub 통합에 필요한 권한 범위](github-integration.md#github-2)에 대해 자세히 알아보십시오.

### **2. Pull request** 지정 <a href="#pr-assignment" id="pr-assignment"></a>

Snyk은 작성한 Pull request를 자동으로 할당하여 올바른 사용자에 의해 수행되도록 할 수 있습니다.

이 기능은 GitHub 통합(GitHub을 통해 가져온 모든 프로젝트) 또는 프로젝트별로 사용할 수 있습니다. 이 기능은 개인 저장소에 대해서만 지원합니다.

사용자를 수동으로 지정하거나(그리고 모두 할당됨) 마지막 commit 사용자 계정에 따라 자동으로 선택할 수 있습니다.

**Github 통합 내의 모든 프로젝트를 활성화**

Snyk의 GitHub Integration _**Settings**_ 페이지로 이동합니다(설정 --> 통합 --> GitHub)

![](../../../.gitbook/assets/code-assignees-contribs.png)

**하나의 프로젝트에 대해 사용**

프로젝트 설정으로 이동하고 프로젝트 설정 내의 **Integration settings** 탭에서 다음을 수행합니다.

![](../../../.gitbook/assets/code-assigness-project.png)

## GitHub 통합 연결 해제

Snyk의 GitHub SCM 통합은 oAuth 앱 통합을 활용합니다. 브로커를 사용하지 않고 GitHub에 통합한 경우 다음 단계에 따라 연결을 끊으면 됩니다.

1. 처음에 통합을 생성한 GitHub 계정에 로그인합니다.
2. account settings으로 이동하고 오른쪽 사이드바에서 **Applications** 탭을 선택합니다.
3. **Authorized OAuth Apps** 탭을 선택합니다. 또한 [Authorized OAuth Apps tab ](https://github.com/settings/applications)탭에도 직접 액세스할 수 있습니다.
4. **Snyk** 항목을 찾아 오른쪽의 점 3개를 클릭하고 **Revoke**를 선택합니다.

이 액세스를 취소하면 해당 GitHub 계정에 대한 Snyk의 액세스가 효과적으로 차단됩니다. 가져온 기존 스냅샷은 Snyk에 유지되며 삭제될 때까지 기존 스냅샷을 기반으로 다시 검색됩니다. Snyk은 더 이상 GitHub 통합에서 새 프로젝트를 가져올 수 없으며 더 이상 새 코드 병합을 다시 검색하지 않습니다.

또한 GitHub - Repository -> Settings -> Branches -> Branch protection rules -> Status checks의 기존 "Branch protection rules"에서 Snyk이 활성화되어 있지 않은지 확인해야 합니다.

## GitHub badges

취약점이 해제되면 README에 패키지에 알려진 보안 구멍이 없음을 나타내는 badge를 부착할 수 있습니다. 이렇게 하면 보안에 관심이 있다는 것을 사용자에게 보여주고 사용자도 관심을 가져야 한다는 것을 알려줍니다.

취약성이 없는 경우 green badge로 표시됩니다.

![](../../../.gitbook/assets/uuid-cb438aa4-226e-2109-f901-c59ca233732e-en.png)

취약성이 발견되면 red badge에 취약성 수가 표시됩니다.

![](../../../.gitbook/assets/uuid-96d6b4d1-afb7-a2bd-093d-eaa96e2ac2c1-en.png)

지정된 Node.js, Ruby 또는 Java GitHub 저장소에 대한 badge를 표시하려면 아래 관련 스니펫을 복사하고 “{username}/{repo}”를 테스트할 GitHub 사용자 이름 및 저장소로 바꿉니다.

**HTML:**

`<*a href="https://snyk.io/test/github/{username}/{repo}">`![image2.png](../../../.gitbook/assets/uuid-2678b218-659f-61c6-8e14-57964dfb2bc6-en.png)

**Markdown:**

`[![Known Vulnerabilities](https://snyk.io/test/github/{username}/{repo}/badge.svg)](https://snyk.io/test/github/{username}/{repo})`

Badge는 master branch에 있는 최신 커밋의 취약점 상태를 반영합니다. 특정 분기, 릴리스 또는 태그의 취약점 상태를 표시하려면 URL의 저장소 이름 뒤에 해당 이름을 추가하십시오.

예를 들어 express 저장소의 4.x 분기에 대한 badge를 표시하려면 다음 URL을 사용합니다. [https://snyk.io/test/github/expressjs/express/4.x/badge.svg](https://snyk.io/test/github/expressjs/express/4.x/badge.svg).

**Styles**

badge의 스타일을 변경하려면 badge.svg뒤에 다음 쿼리 파라미터를 추가합니다.

![](../../../.gitbook/assets/uuid-cb438aa4-226e-2109-f901-c59ca233732e-en.png)

`?style=flat-square`

![](../../../.gitbook/assets/uuid-cb438aa4-226e-2109-f901-c59ca233732e-en.png)

`style=plastic`

**npm badges**

지정된 npm 패키지에 대한 badge를 표시하려면 아래 관련 스니펫을 복사하고 “{name}”을 패키지 이름으로 바꿉니다.

**HTML**

`<*img src="https://snyk.io/test/npm/{name}/badge.svg" alt="Known Vulnerabilities" data-canonical-src="https://snyk.io/test/npm/{name}" style="max-width:100%;"/>`

**Markdown**

`[![Known Vulnerabilities](https://snyk.io/test/npm/{name}/badge.svg)](https://snyk.io/test/npm/{name})`

Badge는 이 패키지의 최신 버전의 취약점 상태를 반영합니다. 특정 패키지의 취약점 상태를 표시하기 위해 URL에서 특정 버전을 지정할 수 있습니다.

예를 들어 패키지 이름의 버전 1.2.3을 테스트하려면 URL을 사용하십시오. [https://snyk.io/test/npm/name/1.2.3/badge.svg](https://snyk.io/test/npm/name/1.2.3/badge.svg).

**개인 패키지 및 저장소**

Badge는 현재 공용 npm 패키지 및 GitHub 저장소에 대해서만 작동하며 개인 저장소를 가리킬 경우 실패합니다. 공개 및 비공개 GitHub 저장소의 취약점을 지속적으로 확인하려면 GitHub 저장소를 Snyk와 통합하는 것을 고려하십시오.

**사용자 지정 매니페스트 파일 위치**

기본적으로 badge는 프로젝트의 루트에서 탐지된 첫 번째 유효한 [manifest file](../../../products/snyk-open-source/language-and-package-manager-support/)에 대해 테스트합니다.

매니페스트 파일이 저장소의 루트가 아닌 다른 위치에 있거나 badge를 표시할 매니페스트 파일이 여러 개 있는 경우 targetFile 쿼리 문자열 파라미터를 전달하여 지원하는 다른 매니페스트 파일에 대해 badge를 테스트하도록 지정할 수 있습니다.

**HTML:**

`<*a href="https://snyk.io/test/github/{username}/{repo}">`

**Markdown:**

`[![Known Vulnerabilities](https://snyk.io/test/github/{username}/{repo}/badge.svg?targetFile={path-to-target-file})](https://snyk.io/test/github/{username}/{repo})`
