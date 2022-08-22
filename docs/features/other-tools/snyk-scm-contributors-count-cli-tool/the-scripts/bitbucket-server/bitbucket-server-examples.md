---
description: Bitbucket Server에 대한 옵션 목록 및 몇 가지 예
---

# Bitbucket Server - 몇 가지 예

`snyk-scm-contributors-count bitbucket-server` command에는 다음 옵션을 사용할 수 있습니다:

```
  --version                 Show version number                        [boolean]
  --help                    Show help                                  [boolean]
  --token                   Bitbucket server token                     [required]
  --url                     Bitbucket server base url e.g. (https://bitbucket.mycompany.com)         [required]
  --projectKeys             [Optional] Bitbucket server project key to count contributors for
  --repo                    [Optional] Specific repo to count only for
  --exclusionFilePath       [Optional] Exclusion list filepath
  --json                    [Optional] JSON output, requiered when using the "consolidateResults" command
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
2. Bitbucket Server 토큰 및 URL 가져오기:
   *   토큰이 없는 경우 이 [가이드](https://www.jetbrains.com/help/youtrack/server/integration-with-bitbucket-server.html#enable-youtrack-integration-bbserver)를 참조하여 토큰을 만듭니다.

       **주의:** 토큰에 리포지토리에 대한 읽기 권한이 있는지 확인하십시오.
   * 이 URL은 Bitbucket Server 인스턴스의 실제 URL입니다\
     (예: http://bitbucket-server.mycompany.com).

## Command 실행

다음과 같은 level의 사용 및 옵션을 고려할 수 있습니다:

### 사용 Level:

*   Bitbucket Server에서 모든 프로젝트와 해당 리포지토리에 대한 커밋을 가져오려면 Bitbucket Server 토큰 및 URL을 제공하십시오:

    ```
    snyk-scm-contributors-count bitbucket-server --token BITBUCKET-TOKEN --url BITBUCKET-URL
    ```
*   Bitbucket Server에서 일부 프로젝트와 해당 리포지토리에 대한 커밋을 가져오려면 Bitbucket Server 토큰, Bitbucket Server URL 및 프로젝트를 쉼표로 구분하여 제공하십시오.

    ```
    snyk-scm-contributors-count bitbucket-server --token BITBUCKET-TOKEN --url BITBUCKET-URL --projectKeys Key1,Key2...
    ```
*   Bitbucket Server에서 특정 리포지토에 대한 커밋을 가져오려면 Bitbucket Server 토큰, Bitbucket Server URL, 프로젝트 및 리포지토리 이름을 입력하십시오.

    ```
    snyk-scm-contributors-count bitbucket-server --token BITBUCKET-TOKEN --url BITBUCKET-URL --projectKeys Key1 --repo Repo1
    ```

### 옵션

*   Snyk에서 이미 모니터링한 리포지토리에 관계없이 Bitbucket Server에서 모든 커밋을 가져오려면 `--skipSnykMonitoredRepos` flag를 추가하십시오.\
    Snyk에서 모니터링되지 않는 리포지토리가 Bitbucket Server에 있을 수 있습니다. 이 flag를 사용하여 Snyk에서  모니터링 하는 리포지토리 확인을 건너뛰고 Bitbucket Server로 직접 이동하여 커밋을 가져옵니다.

    ```
    snyk-scm-contributors-count bitbucket-server --token BITBUCKET-TOKEN --url BITBUCKET-URL --skipSnykMonitoredRepos
    ```
*   일부 기여자가 커밋에서 계산되지 않도록 하려면 무시할 이메일이 포함된 제외 파일(쉼표로 구분)을 추가하고 해당 파일의 경로와 함께 `--exclusionFilePath`를 적용합니다:

    ```
    snyk-scm-contributors-count bitbucket-server --token BITBUCKET-TOKEN --url BITBUCKET-URL --projectKeys Key1,Key2 --exclusionFilePath PATH_TO_FILE
    ```
*   출력을 json 형식으로 설정하려면 `--json` flag를 추가하십시오:

    ```
    snyk-scm-contributors-count bitbucket-server --token BITBUCKET-TOKEN --url BITBUCKET-URL --projectKeys Key1 --repo Repo1 --json
    ```
*   모니터링되지 않는 리포지토리로 import file을 생성하려면 import file이 저장될 폴더에 대한 유효한(쓰기 가능) 경로와 함께 `--importConfDir` flag를 추가하고 파일에 추가할 리포지토리 유형을 가진 `--importFileRepoType` flag(선택 사항)를 추가합니다(`all`/`private`/`public`, 기본값은 `all`). 이러한 flag는 `--repo` flag로 **설정할 수 없습니다**.

    ```
    snyk-scm-contributors-count bitbucket-server --token BITBUCKET-TOKEN --url BITBUCKET-URL --importConfDir ValidPathToFolder --importFileRepoType private/public/all
    ```

    이러한 flag에 대한 자세한 내용은 [import file 생성 및 사용](../../creating-and-using-the-import-files.md)을 참조하십시오.
*   상세 출력에 대해 디버그 모드로 실행하려면 `DEBUG=synk*` 을 command의 시작 부분에 추가하십시오.

    ```
    DEBUG=snyk* snyk-scm-contributors-count bitbucket-server --token BITBUCKET-TOKEN --url BITBUCKET-URL --projectKeys Key1 --repo Repo1 --exclusionFilePath PATH_TO_FILE --skipSnykMonitoredRepos --json
    ```
