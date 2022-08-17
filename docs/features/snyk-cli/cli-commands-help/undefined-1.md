# 코드

## 사용법

`snyk code [<SUBCOMMAND>] [<OPTIONS>] [<PATH>]`

## 설명

`snyk code` 명령은 정적 코드 분석을 사용하여 보안 문제를 찾습니다.

자세한 내용은 [CLI for Snyk Code](https://docs.snyk.io/snyk-code/cli-for-snyk-code) 참

## 하위 명령: `test`

알려진 문제가 있는지 테스트합니다.

## 종료 코드

가능한 종료 코드와 그 의미는 다음과 같습니다.&#x20;

**0**: 성공, 취약점 없음\
**1**: action\_neded, 취약성 발견\
**2**: 실패, 명령 재실행 시도\
**3**: 실패, 지원되는 프로젝트가 검색되지 않음

## Snyk CLI 구성

환경 변수를 사용하여 Snyk CLI를 구성하고 Snyk API로 연결하기 위한 변수를 설정할 수 있습니다. [Configure the Snyk CLI](https://docs.snyk.io/features/snyk-cli/configure-the-snyk-cli) 참

## 디버그

`-d` 옵션을 사용하여 디버그 로그를 출력합니다.

## 코드 테스트 하위 명령 옵션

### `--org=<ORG_ID>`

특정 조직에 연결된 Snyk 명령을 실행할`<ORG_ID>`를 지정합니다. `<ORG_ID>`는 개인 테스트 제한에 영향을 미칩니다.

조직이 여러 개인 경우 다음을 사용하여 CLI에서 기본 값을 설정할 수 있습니다.

`$ snyk config set org=<ORG_ID>`

새로 테스트한 모든 프로젝트가 기본 조직에서 테스트 되도록 기본 값을 설정합니다. 기본 값을 재 정의해야 하는 경우 `--org=<ORG_ID>`옵션을 사용합니다.

Default: `<ORG_ID>` that is the current preferred organization in your [Account settings](https://app.snyk.io/account)

Note that you can also use `--org=<orgslugname>`. The `ORG_ID` works in both the CLI and the API. The organization slug name works in the CLI, but not in the API.

For more information see the article [How to select the organization to use in the CLI](https://support.snyk.io/hc/en-us/articles/360000920738-How-to-select-the-organization-to-use-in-the-CLI)

### `--json`

Print results in JSON format.

Example: `$ snyk code test --json`

### `--json-file-output=<OUTPUT_FILE_PATH>`

Save test output in JSON format directly to the specified file, regardless of whether or not you use the `--json` option.

This is useful if you want to display the human-readable test output using stdout and at the same time save the JSON format output to a file.

Example: `$ snyk code test --json-file-output=vuln.json`

### `--sarif`

Return results in SARIF format.

Example: $snyk code

### `--sarif-file-output=<OUTPUT_FILE_PATH>`

Save test output in SARIF format directly to the \<OUTPUT\_FILE\_PATH> file, regardless of whether or not you use the `--sarif` option.

This is especially useful if you want to display the human-readable test output using stdout and at the same time save the SARIF format output to a file.

### `--severity-threshold=<low|medium|high|critical>`

Report only vulnerabilities at the specified level or higher. Note that the Snyk Code configuration issues do not currently use the `critical` severity level.
