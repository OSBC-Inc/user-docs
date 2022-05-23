# GitHub Enterprise 통합

{% hint style="info" %}
GitHub Enterprise와 같은 자체 관리 소스 코드는 엔터프라이즈 계획, [계획 및 가격 페이지](https://snyk.io/plans/)에서 자세한 내용을 확인할 수 있습니다.
{% endhint %}

Snyk의 GitHub Enterprise 통합을 통해 다음과 같은 이점을 얻을 수 있습니다.

* 모든 통합 저장소에서 보안 스캔을 지속적으로 수행합니다.
* 오픈 소스 구성 요소의 취약점을 탐지합니다.
* 자동화된 수정 및 업그레이드를 제공합니다.

## GitHub Enterprise 통합 설정

1. GitHub Enterprise에서 Snyk 권한으로 모니터링할 저장소에 _**write**_ level 이상의 권한을 가진 전용 서비스 계정을 만듭니다. 자세한 내용은 [Required permissions scope for the GitHub integration](github-enterprise-integration.md#required-permissions-scope-for-the-github-integration)을 참조하십시오.
2. **repo (all)**, **admin:read:org**, 및 **admin:repo\_hooks (read & write)** 한 범위를 사용하여 해당 계정에 대한 개인 액세스 토큰을 생성합니다. 자세한 내용은 [GitHub Enterprise documentation](https://docs.github.com/en/enterprise-server@2.22/github/authenticating-to-github/creating-a-personal-access-token)을 참조하십시오.
3. 개인 액세스 토큰을 **인증**하고 SSO를 활성화합니다.
4. Snyk의 **Integrations** 페이지로 이동하여 **GitHub Enterprise**를 클릭합니다.
5. Github Enterprise URL과 작성한 서비스 계정의 개인 액세스 토큰을 입력하십시오. **Note**: 다음 URL을 제공하여 이 통합을 사용하여 GitHub Enterprise Cloud에 통합할 수 있습니다. [https://api.github.com](https://api.github.com)
6. **Save**을 클릭합니다. Snyk는 GitHub Enterprise 인스턴스에 연결합니다. 연결에 성공하면 다음 표시가 나타납니다.
7. Snyk으로 가져올 저장소를 선택한 다음 **Add selected repositories**를 클릭합니다.
8. Snyk은 전체 디렉토리 트리에서 선택한 저장소에서 디펜던시 파일(예: package.json)을 검색하고 프로젝트로 가져옵니다.
9. 가져온 프로젝트는 **Projects** 페이지에 나타나고 취약점을 지속적으로 검사합니다.

![](<../../../.gitbook/assets/spaces\_-MdwVZ6HOZriajCf5nXH\_uploads\_git-blob-8b3be1cd3d5f4117327c067a1b1c17761b08c9b0\_which\_repos (3) (5) (9) (7) (18) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (27) (1) (1) (26).jpg>)

## GitHub Enterprise Broker startup script

```
docker run --restart=always \
           -p 8000:8000 \
           -e BROKER_TOKEN=secret-broker-token \
           -e GITHUB_TOKEN=secret-github-token \
           -e GITHUB=your.ghe.domain.com \
           -e GITHUB_API=your.ghe.domain.com/api/v3 \
           -e GITHUB_GRAPHQL=your.ghe.domain.com/api \
           -e PORT=8000 \
           -e BROKER_CLIENT_URL=http://my.broker.client:8000 \
       snyk/broker:github-enterprise
```

## GitHub Enterprise 통합 기능

통합을 설정한 후에는 다음 기능을 사용할 수 있습니다.

**Project-level 보안 보고서**

Snyk은 고급 보안 보고서를 생성하여 저장소에서 발견된 취약점을 탐색하고 필요한 업그레이드 또는 패치를 사용하여 저장소로 직접 수정 pull request를 열어 수정할 수 있습니다.

다음은 project-level 보안 보고서의 예시입니다.

![](<../../../.gitbook/assets/spaces\_-MdwVZ6HOZriajCf5nXH\_uploads\_git-blob-fc8f10812029577f2ec93a2b199e8159105438a4\_mceclip0-22- (2) (5) (6) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (34).png>)

**프로젝트 모니터링 및 자동 수정 pull requests**

Snyk은 매일 또는 매주 프로젝트를 자주 스캔합니다. 새 취약점이 발견되면 e메일을 통해 저장소에 대한 수정 사항이 포함된 자동 pull request를 열어 사용자에게 알립니다.

다음은 Snyk이 연 수정 pull request의 예입니다.

![](../../../.gitbook/assets/uuid-6cfdaf0b-c349-468d-fe65-4f80bad110ea-en.png)

자동 수정 pull request 설정을 검토하고 조정하려면 다음과 같이 진행하십시오.

1. settings ![cog\_icon.png](../../../.gitbook/assets/spaces\_-MdwVZ6HOZriajCf5nXH\_uploads\_git-blob-6ec48d5a9af2aa5be97d1691317737ef059c75bd\_cog\_icon.png) > **Integrations**를 클릭합니다.&#x20;
2. GitHub Enterprise에서 **Edit Settings**를 선택합니다.&#x20;
3. **Automatic fix pull requests**로 이동합니다.

![](<../../../.gitbook/assets/spaces\_-MdwVZ6HOZriajCf5nXH\_uploads\_git-blob-416e8bc0d0657eb9fc7c38c2c869f0577e7b3334\_mceclip4 (1) (2) (6) (7) (3) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (30).png>)

**Pull request 테스트**

Snyk은 저장소에 새로 생성된 pull request에서 보안 취약점을 검사하고 GitHub Enterprise로 status check를 보냅니다. 이를 통해 pull request가 GitHub Enterprise에서 직접 새로운 보안 문제를 발생시키는지 여부를 확인할 수 있습니다.

다음은 GitHub Enterprise의 Pull Request 페이지에 Snyk pull request checks가 나타나는 방법입니다.

![](<../../../.gitbook/assets/spaces\_-MdwVZ6HOZriajCf5nXH\_uploads\_git-blob-d169f3f27aefe4eb86d28051fcdeeb9f9d4d0f84\_uuid-87113833-be79-dbe2-8860-a3f224d654c4-en (2) (2) (6) (5) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (20).png>)

pull request 테스트 설정을 검토하고 조정하려면 다음과 같이 진행하십시오.

1. settings ![cog\_icon.png](../../../.gitbook/assets/spaces\_-MdwVZ6HOZriajCf5nXH\_uploads\_git-blob-6ec48d5a9af2aa5be97d1691317737ef059c75bd\_cog\_icon.png) > **Integrations**를 클릭합니다.&#x20;
2. GitHub Enterprise에서 **Edit Settings**를 선택합니다.&#x20;
3. **pull requests**에 대한 **Default Snyk test**로 이동합니다.

![](<../../../.gitbook/assets/mceclip5 (1) (1).png>)

## GitHub 통합에 필요한 권한 범위

수동으로 또는 자동으로 트리거되는 모든 작업은 통합 설정에서 토큰이 구성된 GitHub 서비스 계정에 대해 수행됩니다. 구성된 토큰에 필요한 액세스 범위가 표시됩니다.

| **Action**                                          | **Why?**                                                                                       | **Required permissions in GitHub** |
| --------------------------------------------------- | ---------------------------------------------------------------------------------------------- | ---------------------------------- |
| Daily / weekly tests                                | 개인 저장소에서 매니페스트 파일을 읽습니다.                                                                       | _repo (all)_                       |
| Manual fix pull requests (triggered by the user)    | 모니터링하는 저장소에 수정 PR을 생성합니다.                                                                      | _repo (all)_                       |
| Automatic fix and upgrade pull requests             | 모니터링하는 저장소에 수정/업그레이드 PR을 생성합니다.                                                                | _repo (all)_                       |
| Snyk tests on pull requests                         | 새로운 PR을 생성하거나 기존 PR이 업데이트될 때마다 pull request status check를 보냅니다.                                | _repo (all)_                       |
| Importing new projects to Snyk                      | For presenting a list of all Github 조직에서 사용 가능한 모든 저장소의 목록을 "Add Projects" 화면(가져오기 팝업)에 표시합니다. | _admin:read:org, repo (all)_       |
| Snyk tests on pull requests - initial configuration | 가져온 저장소에 Snyk의 webhook을 추가하면 pull request를 생성하거나 업데이트될 때마다 Snyk이 알림을 받고 스캔을 진행할 수 있습니다.        | _admin:repo\_hooks (read & write)_ |

**저장소에 필요한 사용 권한 범위**

Snyk이 매니페스트 파일을 자주 읽는 것과 같은 모니터링하는 저장소에서 필요한 작업을 수행하려면 Snyk에 연결된 계정(직접 또는 Snyk Broker 사용)이 저장소에 대해 다음과 같은 액세스 권한이 필요합니다.

| **Action**                                          | **Why?**                                                                                | **Required permissions on the repository** |
| --------------------------------------------------- | --------------------------------------------------------------------------------------- | ------------------------------------------ |
| Daily / weekly tests                                | 개인 저장소에서 매니페스트 파일을 읽습니다.                                                                | _Write_ or above                           |
| Snyk tests on pull requests                         | 새로운 PR을 생성하거나 기존 PR이 업데이트될 때마다 pull request status check을 보냅니다.                         | _Write_ or above                           |
| Opening fix and upgrade pull requests               | 모니터링하는 저장소에 수정/업그레이드 PR을 생성합니다.                                                         | _Write_ or above                           |
| Snyk tests on pull requests - initial configuration | 가져온 저장소에 Snyk의 webhook을 추가하면 pull request를 생성하거나 업데이트될 대마다 Snyk이 알림을 받고 스캔을 진행할 수 있습니다. | _Admin_                                    |
