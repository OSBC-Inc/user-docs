---
description: consolidateResults 명령을 사용하는 방법
---

# Consolidate Results

## consolidateResults command

SCM-Contributors-Count 도구로 작업할 때 둘 이상의 source control manager (SCM) 로 작업할 수 있습니다.각 SCM에 대해 별도의 명령을 실행하여 해당 저장소에 대한 기여자 를 가져옵니다.

For example : GitHub 리포지토리와 Bitbucket 프로젝트 모두에 커밋하는 기여자가 있는 경우 두 SCM의 출력에서 해당 기여자의 세부 정보를 볼 수 있습니다.

모든 SCM에서 모든 기여자에 대한 전체적인 그림을 얻으려면 `consolidateResults` command를 사용하십시오.

이 command 사용하면 다양한 SCM에 대한 `snyk-scm-contributors-count` command의 여러(`json`) 출력을 가져와 고유한 기여자 수와 모든 SCM의 총 리포지토리를 하나의 파일로 통합할 수 있습니다.

`consolidateResults` command에 사용할 수 있는 옵션은 다음과 같습니다 :

```
  --version                 Show version number                        [boolean]
  --help                    Show help                                  [boolean]
  --folderPath              Path to a folder containing the json outputs        [required]
```

## Running the commands

* Run the `snyk-scm-contributors-count` command for each repo with the `--json` flag and send the output to a designated folder, for example:

```
snyk-scm-contributors-count github --token TOKEN --json > PathToFolder/FileName
snyk-scm-contributors-count github-enterprise --token TOKEN --json > PathToFolder/OtherFileName
```

* Run the `consolidateResults` command and apply the `--folderPath` flag with the path to the designated, read/write accessible folder that contains the different output json files with the individual SCM results.

```
snyk-scm-contributors-count consolidateResults --folderPath PathToFolder
```

* The tool will then look for valid files in the folder, read the content of the files, create a new file with consolidated, unique results from all the files that have been read, and name the new file`consolidated-results.json`.
