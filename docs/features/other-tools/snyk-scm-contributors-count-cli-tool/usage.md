---
description: SCM-Contributors-Count Modes 및 Levels
---

# 사용법

## 일반적인 command

```
snyk-scm-contributors-count <command> <command-options>
```

**`<command>`** 는 다음 중 하나 입니다:

* `azure-devops`
* `bitbucket-cloud`
* `bitbucket-server`
* `github`
* `github-enterprise`
* `gitlab`
* `consolidateResults`

**`<command-options>`**: [스크립트 섹션](the-scripts/)의 SCM 관련 페이지(예 페이지)를 참조하십시오.

## Modes

### Onboarding전 사용범위 지정

이 Mode는 Bitbucket 및 Azure에서만 작동합니다.

다음과 같이 `skipSnykMonitoredRepos` flag를 적용합니다:

```
snyk-scm-contributors-count bitbucket-cloud --user USERNAME --password PASSWORD --skipSnykMonitoredRepos
```

### Snyk license consumption

이 Mode는 Bitbucket 및 Azure에서만 작동합니다.

다음과 같이 `SNYK_TOKEN` 을 내보내야 합니다:

```
export SNYK_TOKEN=<YOUR-SNYK-TOKEN>
snyk-scm-contributors-count bitbucket-cloud --user USERNAME --password PASSWORD
```

## Levels

### Top Level

이 사용 Level에서 Tool은 SCM의 상단에서 시작하여 조직/그룹 가져온 다음 Repo Level로 내려가 모든 리포지토리를 가져온 다음 지난 90일 동안의 커밋을 카운트합니다.

이 Level을 사용하기위해 자격 증명(및 해당되는 경우 호스트/url)을 제공하면 Tool은 다음과 같이 모든 조직/그룹 및 해당 리포지토리에 대한 기여자 수를 가져옵니다:

```
snyk-scm-contributors-count github --token TOKEN
```

### Mid Level

이 사용 Level에서 Tool은 사용자가 제공하는 조직/그룹에서 시작하여 Repo Level로 내려가 모든 리포지토리를 가져온 다음 지난 90일 동안의 커밋을 계산합니다.

이 Level을 사용하려면 다음과 같이 자격 증명과 리포지토리와 해당 기여자 수를 가져올 그룹 또는 조직의 comma-separated 목록을 제공하십시오:

```
snyk-scm-contributors-count gitlab --token TOKEN --groups GROUP1,GROUP2
```

### Low Level

이 사용 Leve에서 Tool은 기여자 수를 얻기 위해 하나의 리포지토리에만 초점을 맞춥니다.

이 Level을 사용하려면 다음과 같이 자격 증명(해당되는 경우 호스트/url), 조직/그룹 및 리포지토리를 하나씩 제공하십시오:

```
snyk-scm-contributors-count github-enterprise --token TOKEN --url HOST_URL --orgs ORG --repo REPO
```

## Debug mode

다음과 같이 command 시작 부분에 `DEBUG=snyk*` 을 추가합니다:

```
DEBUG=snyk* snyk-scm-contributors-count bitbucket-server --token BITBUCKET-TOKEN --url BITBUCKET-URL --projectKeys Key1 --repo Repo1 --exclusionFilePath PATH_TO_FILE --skipSnykMonitoredRepos --json
```

## 추가 옵션 Flags

Command에 대해 추가 Flag를 설정할 수 있습니다:

* `snyk-api-import` tool과 함께 사용할 모니터링되지 않은 리포지토리 데이터로 **Import file**을 만들고 리포지토리를 `my Snyk account`로 가져옵니다. Bitbucket 및 Azure에서만 작동합니다. Import file을 저장할 유효한 쓰기 가능한 폴더에 경로를 지정하여 `importConfDir` flag를 적용합니다. 이 flag는 `importFileRepoType` flag와 관련이 있습니다.
* **Import file에 추가할 리포지토리 유형**을 선택합니다. Bitbucket 및 Azure에서만 작동합니다. `importFileRepoType` flag를 `all`, `private` 또는 `public` 옵션 중 하나와 함께 적용합니다.
* **Committer를 카운트 대상에서 제외합니다**. 카운트에서 제외할 커밋의 이메일이 포함된 텍스트 파일의 경로가 있는 명령에 `exclusionFilePath` flag를 적용합니다.
* 요약 및 결과를 json 형식으로 출력합니다. command에 `json` flag를 적용합니다.

## The consolidateResults command

Used for consolidating results from several commands across different SCMs, into a single file with unique contributors count. Refer to the [command page](consolidate-results.md).
