---
description: GitHub에 대한 옵션 목록 및 몇 가지 예
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

*   Github에서 내 모든 Org의 모든 레포지토리에 대한 커밋을 가져오려면, Github 토큰을 제공하십시오:

    ```
    snyk-scm-contributors-count github --token TOKEN
    ```
*   Github에 있는 일부 Org와 해당 리포지토리에 대한 커밋을 가져오려면, Github 토큰과 조직 이름을 쉼표로 구분하여 제공하십시오:

    ```
    snyk-scm-contributors-count github --token TOKEN --orgs ORG_ONE,ORG_TWO,ORG_THREE
    ```
*   Github에서 하나의 리포지토리에 대한 커밋만 가져오려면: Github 토큰, 하나의 Org 이름 및 하나의 리포지토리 이름을 제공합니다:

    ```
    snyk-scm-contributors-count github --token TOKEN --orgs ORG --repo REPO
    ```

### 옵션:

* 일부 기여자를 커밋에서 제외하려면 => 무시할 이메일이 포함된 제외 파일(쉼표로 구분)을 추가하고 해당 파일에 대한 경로와 함께 `--exclusionFilePath` 를 적용합니다:

```
snyk-scm-contributors-count github --token TOKEN --orgs ORG_ONE,ORG_TWO --exclusionFilePath PATH_TO_FILE
```

*   출력을 json 형식으로 설정하려면 `--json` flag를 추가하십시오:

    ```
    snyk-scm-contributors-count github --token TOKEN --json
    ```
* 상세 출력에 대해 디버그 모드로 실행하려면 `DEBUG=synk*` 을 command의 시작 부분에 추가하십시오:

```
DEBUG=snyk* snyk-scm-contributors-count github --token TOKEN --orgs ORG --repo REPO --exclusionFilePath PATH_TO_FILE --json
```
