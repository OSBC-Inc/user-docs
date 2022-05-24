# Bitbucket Cloud 통합

Snyk의 Bitbucket Cloud 통합을 통해 모든 통합 저장소에서 보안 스캔을 지속적으로 수행하고, 오픈 소스 구성 요소의 취약점을 탐지하고, 자동화된 수정 프로그램을 사용할 수 있습니다.

> **기능 사용 여부**\
> 이 기능은 모든 plan에서 사용할 수 있습니다. 자세한 내용은 [pricing plans](https://snyk.io/plans/)를 참고하십시오.

### Bitbucket Cloud 통합 설정

> 새로 생성된 사용자는 Snyk을 사용하여 모니터링해야 하는 모든 저장소에 대한 **Admin** 권한이 있어야 합니다.
>
> 관리자 권한이 필요하지만, Snyk의 액세스는 궁극적으로 [App Password에 할당된 권한](https://support.atlassian.com/bitbucket-cloud/docs/app-passwords/)에 의해 제한됩니다.

1. Snyk에게 Bitbucket 계정에 대한 액세스 권한을 부여하려면 다음과 같이 하십시오.
   1. 관리자 권한이 있는 Bitbucket에서 전용 서비스 계정을 설정합니다.
   2. 사용자 작성에 대한 자세한 내용은 [Bitbucket documentation](https://support.atlassian.com/bitbucket-cloud/docs/grant-access-to-a-workspace/)을 참조하십시오.
2. Snyk에서 **Integrations**페이지로 이동하여 **Bitbucket Cloud** 카드를 클릭합니다.
3. Bitbucket Cloud 계정에 액세스하여 다음 권한으로 고유한 Snyk용 App Password를 생성하십시오.
   1. **Account: Email & Read**
   2. **Workspace membership: Read**
   3. **Projects: Read**
   4. **Repositories: Read & Write**
   5. **Pull requests: Read & Write**
   6. **Webhooks: Read & Write**
      1. 자세한 방법은 [Bitbucket documentation](https://confluence.atlassian.com/bitbucket/app-passwords-828781300.html)을 참조하십시오.
4. BitBucket의 개인 설정에서 찾을 수 있는 사용자 이름과 사용자가 만든 [서비스 계정의 App Password](https://support.atlassian.com/bitbucket-cloud/docs/app-passwords/)를 입력하십시오.
5.  **Save**를 클릭합니다.\
    Snyk은 Bitbucket Cloud 계정에 연결합니다. 연결에 성공하면 다음 표시가 나타납니다.

    ![](<../../../.gitbook/assets/settings (1).png>)\
    Snyk이 모니터링할 저장소를 선택할 수 있습니다.
6. Import repositories to Snyk을 시작하려면 **Add your Bitbucket Cloud repositories to Snyk**을 클릭합니다.
7. 메시지가 나타나면 Snyk으로 가져올 저장소를 선택한 다음 **Add selected repositories**를 클릭합니다.
8. Snyk은 전체 디렉토리 트리에서 선택한 저장소에서 디펜던시 파일(package.json 및 pom.xml)을 스캔하고 프로젝트로 가져옵니다.
9. 가져온 프로젝트가 **Projects** 페이지에 나타나고 취약점을 지속적으로 검사합니다.

![](<../../../.gitbook/assets/spaces\_-MdwVZ6HOZriajCf5nXH\_uploads\_git-blob-41b0e6025361da5ff79cfe594401899bf4377de3\_444 (2) (4) (4) (4) (5) (4) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (10).png>)

After the integration is done, you can use capabilities as described below.

### Project level security reports

Snyk produces advanced security reports, allowing you to explore the vulnerabilities found in your repositories, and fix them immediately by opening a fix pull request directly to your repository, with the required upgrades or patches.

This is an example of a project level security report:

![](../../../.gitbook/assets/mceclip0-22-%20\(2\)%20\(5\)%20\(6\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(33\).png)

### Projects monitoring and automatic fix pull requests

Snyk frequently scans your projects on either a daily or a weekly basis. When new vulnerabilities are found, it notifies you by email and by opening an automated pull requests with fixes to repositories.

Here is an example of a fix pull request opened by Snyk:

![](../../../.gitbook/assets/666.png)

To review and adjust the automatic fix pull request settings:

1. Click on settings![cog\_icon.png](../../../.gitbook/assets/cog\_icon.png) > **Integrations**.
2. Select **Edit Settings** for Bitbucket Cloud.
3. Navigate to **Automatic fix pull requests**:

![](../../../.gitbook/assets/mceclip4%20\(1\)%20\(2\)%20\(6\)%20\(7\)%20\(3\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(1\)%20\(31\).png)

### Pull request tests

Snyk tests any newly created pull request in your repositories for security vulnerabilities, and sends a build check to Bitbucket Cloud. You can to see whether the pull request introduces new security issues, directly from Bitbucket Cloud.

This is how Snyk pull request build check appears in the **Pull Request** page in Bitbucket Cloud:

![](../../../.gitbook/assets/888.png)

To review and adjust the pull request tests settings,

1. Click on settings ![cog\_icon.png](../../../.gitbook/assets/cog\_icon.png) > **Integrations**.
2. Select **Edit Settings** for Bitbucket Cloud.
3. Navigate to **Default Snyk test for pull requests > Open Source Security & Licenses**, and edit settings: \*\*\*\*

![](../../../.gitbook/assets/Screenshot%202022-03-16%20at%2010.07.50.png)

### Required permissions scope for the Bitbucket Cloud integration

All the operations, triggered manually or automatically, are performed for a Bitbucket Cloud service account that has its token (App Password) configured in the integrations settings.

This shows the required access scopes for the configured token:

| **Action**                                          | **Why?**                                                                                                                                               | **Required permissions in Bitbucket**                            |
| --------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------- |
| Daily / weekly tests                                | For reading manifest files in private repos                                                                                                            | _Repositories read_                                              |
| Manual fix pull requests (triggered by the user)    | For creating fix PRs in the monitored repos                                                                                                            | _Repositories (read & write)_ _pull requests (read & write)_     |
| Automatic fix and upgrade pull requests             | For creating fix / upgrade PRs in the monitored repos                                                                                                  | _Repositories (read & write)_ _pull requests (read & write)_     |
| Snyk tests on pull requests                         | For sending pull request status checks whenever a new PR is created / an existing PR is updated                                                        | _Repositories (read & write)_ _pull requests (read & write)_     |
| Importing new projects to Snyk                      | For presenting a list of all the available repos in the Bitbucket in the "Add Projects" screen (import popup)                                          | _Account (read)_ _Workspace membership (read)_ _Projects (read)_ |
| Snyk tests on pull requests - initial configuration | For adding Snyk's webhooks to the imported repos, so Snyk will be informed whenever pull requests are created or updated and be able to trigger scans. | _webhooks (read & write)_                                        |

### Required permissions scope for repositories <a href="#h_01eefvj14p8b3depeffvyvdwzj" id="h_01eefvj14p8b3depeffvyvdwzj"></a>

For Snyk to perform the required operations on monitored repositories (such as reading manifest files on a frequent basis and opening fix or upgrade PRs), the integrated Bitbucket Cloud service account needs **Admin** permissions on the imported repositories:

| **Action**                                          | **Why?**                                                                                                                            | **Required permissions on the repository** |
| --------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------ |
| Daily / weekly tests                                | To read manifest files in private repositories.                                                                                     | **Write** or above                         |
| Snyk tests on pull requests                         | To send pull request status checks when a new PR is created, or an existing PR is updated.                                          |                                            |
| Opening fix and upgrade pull requests               | To create fix PRs in monitored repositories.                                                                                        |                                            |
| Snyk tests on pull requests - initial configuration | To add Snyk's webhooks to the imported repos, so Snyk is informed when pull requests are created or updated, and can trigger scans. | **Admin**                                  |

## 1st Party Integration (Connect App)

The Connect App integration is a layer on top of the regular App Password integration, which allows your developers to consume Snyk from the Bitbucket interface.

> The Connect App currently supports [Snyk Open Source](../../../products/snyk-open-source/) and [Snyk Container](../../../products/snyk-container/) products only.

By adding the Connect App to your Bitbucket workspaces, your workspaces members can import repos and see the security data in a dedicated Snyk tab in Bitbucket Cloud:

![](../../../.gitbook/assets/mceclip1-13-.png)

### Installing the Connect App

To install the app, navigate to the **Security** tab in one of your workspace's repos in Bitbucket Cloud, then click **Try now**:

![](../../../.gitbook/assets/mceclip2-3-.png)

### Uninstalling the Connect App

To remove the Connect App from your workspace in Bitbucket Cloud:

1. Navigate to the **workspace settings** page > **Installed apps**.
2. Find **Snyk Security for Bitbucket Cloud** in the installed applications list.
3. Click **remove**.

### Associating the Connect App to a different Snyk account / organization

The Connect App is associated to a specific Snyk account and organization, as defined during the app onboarding process.

To change these settings later, navigate to the workspace settings and select **Security for Bitbucket Cloud Integration Settings**:

![](../../../.gitbook/assets/mceclip0-23-.png)

### Disabling the Bitbucket Cloud integration

To disable this integration:

1. Click on settings![cog\_icon.png](../../../.gitbook/assets/cog\_icon.png) > **Integrations** in Snyk.
2. Find the specific integration to deactivate in your list of integrations, and click Edit settings.
3. A page appears showing the current status of your integration and a place to update your credentials, specific to each integration (credentials, API key, Service Principal, or connection details):
4. Click **Disconnect**.

![](../../../.gitbook/assets/mceclip2-4-.png)

> Your credentials are removed from Snyk and any integration-specific projects Snyk is monitoring are deactivated on Snyk.\
> If you then choose to re-enable this integration at any time, you will need to re-enter your credentials and activate your projects.
