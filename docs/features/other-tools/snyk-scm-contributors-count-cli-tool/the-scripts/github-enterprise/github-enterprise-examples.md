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

* GitHub Enterprise의 모든 org를 매핑하고 운영 권한을 가진 org만 매핑하려면 `--fetchAllOrgs` flag를 추가하십시오:

```
snyk-scm-contributors-count github-enterprise --token TOKEN --url HOST_URL --fetchAllOrgs
```

*   일부 기여자가 커밋에서 계산되지 않도록 하려면 무시할 이메일이 포함된 제외 파일(쉼표로 구분)을 추가하고 해당 파일에 대한 경로와 함께 `--exclusionFilePath`를 적용합니다:

    ```
    snyk-scm-contributors-count github-enterprise --token TOKEN --url HOST_URL --orgs ORG_ONE,ORG_TWO --exclusionFilePath PATH_TO_FILE
    ```
*   출력을 json 형식으로 설정하려면 `--json` flag를 추가하십시오:

    ```
    snyk-scm-contributors-count github-enterprise --token TOKEN --url HOST_URL --json
    ```
* 상세 출력에 대해 디버그 모드로 실행하려면 `DEBUG=synk*` 접두사를 사용합니다:

```
DEBUG=snyk* snyk-scm-contributors-count github-enterprise --token TOKEN --url HOST_URL --orgs ORG --repo REPO --exclusionFilePath PATH_TO_FILE --json
```
