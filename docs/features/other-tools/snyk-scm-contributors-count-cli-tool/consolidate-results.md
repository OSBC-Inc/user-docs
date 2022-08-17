---
description: consolidateResults 명령을 사용하는 방법
---

# Consolidate Results

## consolidateResults command

SCM-Contributors-Count 도구로 작업할 때 둘 이상의 source control manager (SCM) 로 작업할 수 있습니다.각 SCM에 대해 별도의 명령을 실행하여 해당 저장소에 대한 기여자 수를 가져옵니다.

For example : GitHub 리포지토리와 Bitbucket 프로젝트 모두에 커밋하는 기여자가 있는 경우 두 SCM의 출력에서 해당 기여자의 세부 정보를 볼 수 있습니다.

모든 SCM에서 모든 기여자에 대한 전체적인 그림을 얻으려면 `consolidateResults` command를 사용하십시오.

이 command 사용하면 다양한 SCM에 대한 `snyk-scm-contributors-count` command의 여러(`json`) 출력을 가져와 고유한 기여자 수와 모든 SCM의 총 리포지토리를 하나의 파일로 통합할 수 있습니다.

`consolidateResults` command에 사용할 수 있는 옵션은 다음과 같습니다 :

```
  --version                 Show version number                        [boolean]
  --help                    Show help                                  [boolean]
  --folderPath              Path to a folder containing the json outputs        [required]
```

## command 실행

* `--json` flag를 사용하여 각 리포지토리에 대해 `snyk-scm-contributors-count` command를 실행하고 출력을 지정된 폴더로 보냅니다. 예를 들면 다음과 같습니다 :

```
snyk-scm-contributors-count github --token TOKEN --json > PathToFolder/FileName
snyk-scm-contributors-count github-enterprise --token TOKEN --json > PathToFolder/OtherFileName
```

* `consolidateResults` command를 실행하고 개별 SCM 결과와 함께 다른 출력 json 파일을 포함하는 지정된 읽기/쓰기 액세스 가능 폴더에 대한 경로와 함께 `--folderPath` flag를 적용합니다.

```
snyk-scm-contributors-count consolidateResults --folderPath PathToFolder
```

* 그런 다음 도구는 폴더에서 유효한 파일을 찾고, 파일의 내용을 읽고, 읽은 모든 파일에서 통합된 고유한 결과로 새 파일을 만듭니다. 새 파일의 이름은 `consolidated-results.json` 으로 지정합니다.
