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
중첩된 그룹의 경우 가장 낮은 level의 그룹 이름을 제공해야 합니다. 예를 들어 TopLevelGroup/MidLevelGroup/LowLevelGroup은 `--groups` flag가 있는 "LowLevelGroup"만 제공합니다.
{% endhint %}

* GitLab에서 특정 프로젝트에 대한 커밋을 가져오려면 GitLab 토큰과 **하나**의 그룹 이름 및 **하나**의 프로젝트 이름을 제공하십시오:

```
snyk-scm-contributors-count gitlab --token TOKEN --groups GROUP --project PROJECT
```

### 옵션

* 일부 기여자가 커밋에서 계산되지 않도록 하려면 무시할 이메일이 포함된 제외 파일(쉼표로 구분)을 추가하고 해당 파일의 경로와 함께 `--exclusionFilePath` 를 적용합니다.

```
snyk-scm-contributors-count gitlab --token TOKEN --projectKeys ID1,ID2,Path1/Namespace1 --exclusionFilePath PATH_TO_FILE
```

*   출력을 json 형식으로 설정하려면 `--json` flag를 추가하십시오:

    ```
    snyk-scm-contributors-count gitlab --token TOKEN --json
    ```
* 상세 출력에 대해 디버그 모드로 실행하려면 `DEBUG=synk*` 접두사를 사용합니다:

```
DEBUG=snyk* snyk-scm-contributors-count gitlab --token TOKEN --url URL --exclusionFilePath PATH_TO_FILE --json
```
