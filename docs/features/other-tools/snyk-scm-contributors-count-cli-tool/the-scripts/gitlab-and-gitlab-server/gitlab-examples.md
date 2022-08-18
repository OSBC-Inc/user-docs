---
description: GitLab에 대한 옵션 목록 및 몇 가지 예
---

# GitLab - 몇 가지 예

`snyk-scm-contributors-count gitlab` command에는 다음 옵션을 사용할 수 있습니다:

```
  --version                 Show version number                        [boolean]
  --help                    Show help                                  [boolean]
  --token                   GitLab token                               [required]
  --url                     [Optional] Your GitLab host custom URL. If no host was provided
                            it will default to https://gitlab.com/
  --groups                  [Optional] Your Gitlab groups names to count contributors for 
                            *note* for sub-level groups, provide the lowest level group name                                             
  --project                 [Optional] Your GitLab project path with namespaces to count contributors for
  --exclusionFilePath       [Optional] Exclusion list filepath
  --json                    [Optional] JSON output, required when using the "consolidateResults" command
```

## **Command를 실행하기 전에**

이 [가이드](https://docs.gitlab.com/ee/user/profile/personal\_access\_tokens.html)를 사용하여 GitLab 토큰을 가져오거나 새 토큰을 만드십시오.

**주의:** 토큰에 리포지토리에 대한 읽기 권한이 있는지 확인하십시오.

## Command 실행

다음과 같은 level의 사용 및 옵션을 고려할 수 있습니다:

### 사용 Level

*   GitLab에서 모든 그룹 및 해당 프로젝트에 대한 커밋을 가져오려면 GitLab 토큰(및 GitLab Enterprise의 서버 URL)을 제공하십시오:

    ```
    snyk-scm-contributors-count gitlab --token TOKEN --url URL
    ```
*   GitLab에서 일부 그룹 및 해당 프로젝트에 대한 커밋을 가져오려면 GitLab 토큰과 그룹 이름을 쉼표로 구분하여 제공하십시오:

    ```
    snyk-scm-contributors-count gitlab --token TOKEN --groups GROUP1,GROUP2
    ```

{% hint style="info" %}
Note that for nested groups, you need to provide the lowest level group name, for example, for `TopLevelGroup/MidLevelGroup/LowLevelGroup` provide only "LowLevelGroup" with the `--groups` flag
{% endhint %}

*   To get commits for a specific project in GitLab, provide the GitLab token and **one** group name and **one** project name:

    ```
    snyk-scm-contributors-count gitlab --token TOKEN --groups GROUP --project PROJECT
    ```

### 옵션

* To exclude some contributors from being counted in the commits, add an exclusion file with the emails to ignore(separated by commas) and apply the `--exclusionFilePath` with the path to that file:

```
snyk-scm-contributors-count gitlab --token TOKEN --projectKeys ID1,ID2,Path1/Namespace1 --exclusionFilePath PATH_TO_FILE
```

*   To set the output to json format, add the `--json` flag:

    ```
    snyk-scm-contributors-count gitlab --token TOKEN --json
    ```
* To run in debug mode for verbose output, prefix with`DEBUG=snyk*`:

```
DEBUG=snyk* snyk-scm-contributors-count gitlab --token TOKEN --url URL --exclusionFilePath PATH_TO_FILE --json
```
