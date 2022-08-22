---
description: 옵션 목록 및 몇 가지 예
---

# GitHub - 몇 가지 예

사용 가능한 옵션:

```
  --version                 Show version number                        [boolean]
  --help                    Show help                                  [boolean]
  --token                   Github token                               [required]
  --orgs                    [Optional] A list of Github organizations, separeted by comma, 
                            to fetch and count contributors for their repositories              
  --repo                    [Optional] Specific repo to count only for
  --exclusionFilePath       [Optional] Exclusion list filepath
  --json                    [Optional] JSON output, requiered when using the "consolidateResults" command
```

## **Command를 실행하기 전에**:

이 [가이드](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)를 사용하여 GitHub Enterprise 토큰을 가져오거나 새 토큰을 만드십시오.

**주의:** 토큰에 리포지토리에 대한 읽기 권한이 있는지 확인하십시오.

## Command 실행

다음과 같은 level의 사용 및 옵션을 고려할 수 있습니다:

### 사용 Level:

*   To get commits for all repos in all my orgs in Github: provide the Github token:

    ```
    snyk-scm-contributors-count github --token TOKEN
    ```
*   To get commits for some Orgs and their repos in Github: Provide the Github token and the org names, separated by a comma:

    ```
    snyk-scm-contributors-count github --token TOKEN --orgs ORG_ONE,ORG_TWO,ORG_THREE
    ```
*   To get commits for only one repo in Github: Provide the Github token, one org name and one repo name:

    ```
    snyk-scm-contributors-count github --token TOKEN --orgs ORG --repo REPO
    ```

### 옵션:

* To exclude some contributors from being counted in the commits => add an exclusion file with the emails to ignore(separated by commas) and apply the `--exclusionFilePath` with the path to that file:

```
snyk-scm-contributors-count github --token TOKEN --orgs ORG_ONE,ORG_TWO --exclusionFilePath PATH_TO_FILE
```

*   To set the output to json format: add the `--json` flag:

    ```
    snyk-scm-contributors-count github --token TOKEN --json
    ```
* To run in debug mode for verbose output: prefix with `DEBUG=snyk*`:

```
DEBUG=snyk* snyk-scm-contributors-count github --token TOKEN --orgs ORG --repo REPO --exclusionFilePath PATH_TO_FILE --json
```
