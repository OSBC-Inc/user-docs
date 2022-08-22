---
description: Azure에 대한 옵션 목록 및 몇 가지 예
---

# Azure - 몇 가지 예

`snyk-scm-contributors-count azure devops` command에는 다음 옵션을 사용할 수 있습니다:

```
  --version                 Show version number                        [boolean]
  --help                    Show help                                  [boolean]
  --token                   Azure DevOps token                         [required]
  --org                     Your Org name in Azure DevOps, for example, https://dev.azure.com/{OrgName}           [required]
  --projectKeys             [Optional] Azure DevOps project key/name to count
                            contributors for
  --repo                    [Optional] Specific repo to count only for
  --exclusionFilePath       [Optional] Exclusion list filepath
  --json                    [Optional] JSON output, required when using the "consolidateResults" command
  --skipSnykMonitoredRepos  [Optional] Skip Snyk monitored repos and count contributors for all repos
  --importConfDir           [Optional] Generate an import file with the unmonitored repos: A path to a valid folder for the generated import files
  --importFileRepoType      [Optional] To be used with the importConfDir flag: Specify the type of repos to be added to the import file. Options: all/private/public. Default: all
```

## **Command를 실행하기 전에**

1. SNYK\_TOKEN 내보내기(Snyk에서 이미 모니터링한 리포지토에 대한 기여자만 가져오려는 경우):
   * 토큰에 그룹 level 액세스 권한이 있는지 확인하거나 그룹 level 액세스 권한이 있는 서비스 계정의 토큰을 사용하십시오. 서비스 계정을 만드는 방법에 대한 자세한 내용은 [서비스 계정 설정 방법](https://docs.snyk.io/features/user-and-group-management/structure-account-for-high-application-performance/service-accounts#how-to-set-up-a-service-account)을 참조하십시오.
   * 토큰 값을 복사합니다.
   *   사용자 환경에서 토큰 내보내기:

       ```
       export SNYK_TOKEN=<YOUR-SNYK-TOKEN>
       ```
2. Azure Devops 토큰 및 Org를 얻으십시오.
   *   토큰이 없는 경우 이 [가이드](https://docs.microsoft.com/en-us/azure/devops/organizations/accounts/use-personal-access-tokens-to-authenticate?view=azure-devops\&tabs=Windows)를 참조하여 토큰을 만듭니다.

       **주의:** 토큰에 리포지토리에 대한 읽기 권한이 있는지 확인하십시오.
   * Azure DevOps 사이트의 왼쪽 창에 나열된 Azure에서 Org 이름을 찾습니다.

## Command 실행

Consider the following levels of usage and options:

### 사용 Level:

*   To get commits for all projects and their repos under my Org in Azure , only provide the Azure token and Azure Org:

    ```
    snyk-scm-contributors-count azure-devops --token AZURE-TOKEN --org AZURE-ORG
    ```
*   To get commits for some projects and their repos under my Org in Azure , provide the Azure token, Azure Org and the project key/s separated by a comma:

    ```
    snyk-scm-contributors-count azure-devops --token AZURE-TOKEN --org AZURE-ORG --projectKeys Key1,Key2...
    ```
*   To get commits for a specific repo under my Org in Azure , provide the Azure token, Azure Org, a project key and a repo name:

    ```
    snyk-scm-contributors-count azure-devops --token AZURE-TOKEN --org AZURE-ORG --projectKeys Key1 --repo Repo1
    ```

### 옵션

*   To get all the commits from Azure regardless of the repos that are already monitored by Snyk, add the `--skipSnykMonitoredRepos` flag.

    You might have repos in Azure that are not monitored in Snyk; use this flag to skip checking for Snyk monitored repos and go directly to Azure to fetch the commits.

    ```
    snyk-scm-contributors-count azure-devops --token AZURE-TOKEN --org AZURE-ORG --skipSnykMonitoredRepos
    ```
*   To exclude some contributors from being counted in the commits, add an exclusion file with the emails to ignore (separated by commas) and apply the `--exclusionFilePath` with the path to that file:

    ```
    snyk-scm-contributors-count azure-devops --token AZURE-TOKEN --org AZURE-ORG --projectKeys Key1,Key2 --exclusionFilePath PATH_TO_FILE
    ```
*   To set the output to json format: add the `--json` flag:

    ```
    snyk-scm-contributors-count azure-devops --token AZURE-TOKEN --org AZURE-ORG --projectKeys Key1 --repo Repo1 --json
    ```
*   To create an import file for your unmonitored repos: add the `--importConfDir` flag with a valid (writable) path to a folder in which the import files will be stored and add the `--importFileRepoType` flag (optional) with the repo types to add to the file (`all`/`private`/`public`, defaults to `all`). Note that these flags **can not** be set with the `--repo flag.`

    ```
    snyk-scm-contributors-count azure-devops --token AZURE-TOKEN --org AZURE-ORG --importConfDir ValidPathToWritableFolder --importFileRepoType private/public/all
    ```

    For more details about these flags, refer to the [Creating and using the import page](../../creating-and-using-the-import-files.md).
*   To run in debug mode for verbose output, prefix the command with`DEBUG=snyk*`:

    ```
    DEBUG=snyk* snyk-scm-contributors-count azure-devops --token AZURE-TOKEN --org AZURE-ORG --projectKeys Key1 --repo Repo1 --exclusionFilePath PATH_TO_FILE --skipSnykMonitoredRepos --json
    ```
