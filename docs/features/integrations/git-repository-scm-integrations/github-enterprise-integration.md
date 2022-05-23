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

Click on settings![cog\_icon.png](../../../.gitbook/assets/cog\_icon.png) > **Integrations**. 2. Select **Edit Settings** for GitHub Enterprise. 3. Navigate to **Automatic fix pull requests**:

![](../../../.gitbook/assets/mceclip4%20\(1\)%20\(2\)%20\(6\)%20\(7\)%20\(3\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(38\).png)

**Pull request testing**

Snyk tests any newly created pull requests in your repositories for security vulnerabilities and sends a status check to GitHub Enterprise. This allows you to see whether the pull request introduces new security issues, directly from GitHub Enterprise.

This is how Snyk pull request checks appear in the Pull Request page in GitHub Enterprise:

![](../../../.gitbook/assets/uuid-87113833-be79-dbe2-8860-a3f224d654c4-en%20\(2\)%20\(2\)%20\(6\)%20\(5\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(23\).png)

To review and adjust the pull request tests settings:

1. Click on settings![cog\_icon.png](../../../.gitbook/assets/cog\_icon.png) > **Integrations**.
2. Select **Edit Settings** for GitHub Enterprise.
3. Navigate to **Default Snyk test for pull requests**:

![](<../../../.gitbook/assets/mceclip5 (1) (1).png>)

## Required permissions scope for the GitHub integration

All the operations, triggered manually or automatically, are performed for a GitHub service account that has its token is configured in the integrations settings. This shows the required access scopes for the configured token:

| **Action**                                          | **Why?**                                                                                                                                              | **Required permissions in GitHub** |
| --------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------- |
| Daily / weekly tests                                | For reading manifest files in private repos                                                                                                           | _repo (all)_                       |
| Manual fix pull requests (triggered by the user)    | For creating fix PRs in the monitored repos                                                                                                           | _repo (all)_                       |
| Automatic fix and upgrade pull requests             | For creating fix/upgrade PRs in the monitored repos                                                                                                   | _repo (all)_                       |
| Snyk tests on pull requests                         | For sending pull request status checks whenever a new PR is created / an existing PR is updated                                                       | _repo (all)_                       |
| Importing new projects to Snyk                      | For presenting a list of all the available repos in the GitHub org in the "Add Projects" screen (import popup)                                        | _admin:read:org, repo (all)_       |
| Snyk tests on pull requests - initial configuration | For adding Snyk's webhooks to the imported repos, so Snyk will be informed whenever pull requests are created or updated and be able to trigger scans | _admin:repo\_hooks (read & write)_ |

**Required permissions scope for repositories**

For Snyk to perform the required operation on monitor repositories, such as reading manifest files on a frequent basis, the accounts connected to Snyk (either directly or using Snyk Broker) need the following access on the repositories:

| **Action**                                          | **Why?**                                                                                                                                              | **Required permissions on the repository** |
| --------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------ |
| Daily / weekly tests                                | For reading manifest files in private repos                                                                                                           | _Write_ or above                           |
| Snyk tests on pull requests                         | For sending pull request status checks whenever a new PR is created / an existing PR is updated                                                       | _Write_ or above                           |
| Opening fix and upgrade pull requests               | For creating fix/upgrade PRs in the monitored repos                                                                                                   | _Write_ or above                           |
| Snyk tests on pull requests - initial configuration | For adding Snyk's webhooks to the imported repos, so Snyk will be informed whenever pull requests are created or updated and be able to trigger scans | _Admin_                                    |
