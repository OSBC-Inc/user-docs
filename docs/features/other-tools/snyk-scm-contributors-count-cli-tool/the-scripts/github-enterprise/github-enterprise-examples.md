---
description: 옵션 목록 및 몇 가지 예
---

# Github Enterprise - 몇 가지 예

`snyk-scm-contributors-count github-enterprise` command에는 다음 옵션을 사용할 수 있습니다:

```
  --version                 Show version number                        [boolean]
  --help                    Show help                                  [boolean]
  --token                   Github Enterprise token                    [required]
  --url                     Your GitHub host custom URL, 
                            for example, https://ghe.prod.company.org/ [required]
  --orgs                    [Optional] A list of GitHub Enterprise organizations, separeted by comma, 
                            to fetch and count contributors for their repositories              
  --repo                    [Optional] Specific repo to count only for
  --fetchAllOrgs            [Optional] When enabled, will fetch all orgs that the token has access to
                            rather than fetching only the orgs your authorized to operate in.
  --exclusionFilePath       [Optional] Exclusion list filepath
  --json                    [Optional] JSON output, required when using the "consolidateResults" command
```

## **Command를 실행하기 전에**

이 [가이드](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)를 사용하여 GitHub Enterprise 토큰을 가져오거나 새 토큰을 만드십시오.

**주의:** 토큰에 리포지토리에 대한 읽기 권한이 있는지 확인하십시오.

## Command 실행

다음과 같은 level의 사용 및 옵션을 고려할 수 있습니다:

### 사용 Level

* GitHub Enterprise의 모든 조직에 있는 모든 리포지토리에 대한 커밋을 가져오려면 GitHub Enterprise 토큰을 제공하십시오:\
  `snyk-scm-contributors-count github-enterprise --token TOKEN --url HOST_URL`
*   GitHub Enterprise에서 일부 orgs 해당 리포지토리에 대한 커밋을 가져오려면 GitHub Enterprise 토큰과 org 이름을 쉼표로 구분하여 제공하십시오:

    ```
    snyk-scm-contributors-count github-enterprise --token TOKEN --url HOST_URL --orgs ORG_ONE,ORG_TWO,ORG_THREE
    ```
*   GitHub Enterprise에서 하나의 리포지토리만 커밋하려면 GitHub Enterprise 토큰, 하나의 org 이름 및 하나의 리포지토리 이름을 제공하십시오:

    ```
    snyk-scm-contributors-count github-enterprise --token TOKEN --url HOST_URL --orgs ORG --repo REPO
    ```

### 옵션

* To map all the orgs in GitHub Enterprise and not just the ones you have operate rights to, add the `--fetchAllOrgs` flag:

```
snyk-scm-contributors-count github-enterprise --token TOKEN --url HOST_URL --fetchAllOrgs
```

*   To exclude some contributors from being counted in the commits, add an exclusion file with the emails to ignore(separated by commas) and apply the `--exclusionFilePath` with the path to that file:

    ```
    snyk-scm-contributors-count github-enterprise --token TOKEN --url HOST_URL --orgs ORG_ONE,ORG_TWO --exclusionFilePath PATH_TO_FILE
    ```
*   To set the output to json format, dd the `--json` flag:

    ```
    snyk-scm-contributors-count github-enterprise --token TOKEN --url HOST_URL --json
    ```
* To run in debug mode for verbose output, prefix with `DEBUG=snyk*` :

```
DEBUG=snyk* snyk-scm-contributors-count github-enterprise --token TOKEN --url HOST_URL --orgs ORG --repo REPO --exclusionFilePath PATH_TO_FILE --json
```
