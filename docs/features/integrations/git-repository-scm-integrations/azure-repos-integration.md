# Azure Repos 통합

사용자는 특히 Snyk용으로 생성된 고유한 Azure DevOps PAT(개인 액세스 토큰)를 생성합니다. 사용자 이름과 비밀번호는 함께 Snyk이 사용하는 토큰을 구성합니다. 토큰은 Snyk이 생성할 때 사용자가 Azure Repos에 나타내는 특정 권한에 대해서만 사용자의 리포지토리에 액세스할 수 있는 권한을 부여합니다.

1. 사용자는 Snyk으로 가져올 프로젝트와 저장소를 선택합니다(테스트 및 모니터링용). 사용자는 저장소의 루트 폴더에 없는 매니페스트 파일에 대한 사용자 지정 파일 위치를 입력할 수도 있습니다.
2. Snyk은 사용자가 선택한 항목을 평가하고 루트 폴더와 모든 수준의 모든 하위 폴더에 관련 매니페스트 파일이 있는 항목을 가져옵니다.
3. Snyk는 실행되는 각 테스트에 대해 리포지토리와 직접 통신하여 현재 푸시된 코드와 사용 중인 종속성을 정확히 결정합니다. 각 종속성은 Snyk의 취약성 데이터베이스에 대해 테스트되어 알려진 취약성이 있는지 확인합니다.
4. 구성을 기반으로 취약점이 발견되면 Snyk는 이메일이나 Slack을 통해 알려 즉시 수정 조치를 취할 수 있습니다.

## Azure Repos용 Snyk에 프로젝트 추가

Snyk은 루트 폴더 및 사용자 지정 파일 위치를 평가하여 지원되는 언어로 된 Azure Repos를 테스트하고 모니터링합니다.

**Snyk에 프로젝트 추가**

1. **Projects**로 이동하여 **Add projects**를 클릭합니다. 프로젝트를 가져올 도구를 선택하십시오.
2. 선택한 통합에서 사용 가능한 모든 리포지토리가 포함된 팝업 화면이 열립니다.
3. 보안/라이센스 문제를 모니터링하기 위해 Snyk로 가져올 저장소를 선택하십시오. 특정 조직의 모든 저장소를 가져오려면 조직에 체크 표시를 합니다.
4. 선택한 리포지토리 추가를 클릭합니다. 이제 Snyk는 전체 파일 트리에서 종속성 파일을 검색하고 이를 프로젝트로 Snyk에 가져옵니다.

![](<../../../.gitbook/assets/uuid-cae3b5b8-6971-406c-3c00-91c9d1a570a2-en (1).png>)

## 사용자 지정 파일 위치 추가

1. 사용자 지정 파일 위치 추가 드롭다운 목록에서 사용자 지정 경로를 구성하려는 관련 리포지토리를 선택합니다. 리포지토리는 이전 단계에서 설명한 대로 프로젝트 추가 보기에서 먼저 선택해야 합니다.
2. 텍스트 필드에 위 이미지와 같이 매니페스트 파일이 있는 상대 경로를 입력합니다.

## 가져오기에서 폴더 제외

이 통합은 다른 통합과 유사하게 작동합니다. 프로젝트를 계속 모니터링, 수정 및 관리하려면 문서에서 관련 페이지를 참조하세요.

{% hint style="info" %}
**주의**\
이 필드는 대소문자를 구분하며 패턴은 모든 저장소에 적용됩니다.
{% endhint %}

**Next steps**

Once repositories are imported, a confirmation appears in green at the top of the screen. The selected files are indicated with a unique icon, they are named by organization/repo, and you can now also filter to view only those projects, as seen in the example below:

![](../../../.gitbook/assets/screen-shot-2021-09-16-at-9.12.12-am.png)

This integration works similar to our other integrations. To continue to monitor, fix and manage your projects, see the relevant pages in our Docs.

## Configure your integration for Azure Repos

{% hint style="info" %}
**Feature availability**\
Integration with Azure Repos Cloud is available for all of our pricing plans. Integration with Azure DevOps Server 2020 and above (also known as TFS) is available with Enterprise and Business plans. See [pricing plans](https://snyk.io/plans/) for more details.
{% endhint %}

Snyk integrates with Microsoft Azure Repos to enable you to import your projects and monitor the source code for your repositories. Snyk tests the projects you’ve imported for any known security vulnerabilities found in the application’s dependencies, testing at a frequency you control.

## How to configure your integration

Enable integration between Azure Repos and Snyk, and start managing your vulnerabilities.

**Prerequisites**

Ensure you have set up your Azure Repos account and your Snyk account.

{% hint style="info" %}
**Note**: it is important that a Snyk admin user configure the integration within the UI. Collaborator users cannot complete this task.
{% endhint %}

**Steps**

1. The account creating the Personal Access Token must be a member of the Project Administrators group to allow Git repositories to see the [Azure DevOps documentation](https://docs.microsoft.com/en-us/azure/devops/repos/git/set-git-repository-permissions).
2. Access your Azure Repos account and retrieve a unique Personal Access Token for use by Snyk. For help doing this, see the [Azure DevOps documentation](https://docs.microsoft.com/en-us/azure/devops/organizations/accounts/use-personal-access-tokens-to-authenticate?view=azure-devops).
3. When prompted in Azure, enable the following permissions for Snyk access as follows:
   * Expiry—We recommend choosing an expiration date for this token that is far in the future to avoid breaking integration.
   * Scopes—Custom defined
   * Code—Read and write (enable Project Administrators group permissions if user creating the Personal Access Token is not an admin of the Repositories)
4. [Log in](https://app.snyk.io) to your Snyk account.
5. Navigate to **Integrations** from the menu bar at the top.
6. From the **Integrations** page under the Azure Repos logo, click the **Connect to Azure Repos button.**
7. From the **Settings** page in the **Integrations** area, enter the Azure DevOps organization that you want to integrate with (i.e. [https://dev.azure.com/{org-name}\\](https://dev.azure.com/%7Borg-name%7D\)/) and the personal access token that you just generated. \* Enterprise customers can also provide a custom URL for Azure Repos Server private instance which is publicly reachable.
8. Click **Save**.
9. Snyk tests the connection values and the page reloads, now displaying Azure Repos integration information. A confirmation message that the details were saved also appears in green at the top of the screen. In addition, if the connection to Azure failed, a notification appears under the Connected to Azure Repos section.

![](../../../.gitbook/assets/screen\_shot\_2020-05-19\_at\_17.16.24.png)
