# 코드

## 사용법

`snyk code [<SUBCOMMAND>] [<OPTIONS>] [<PATH>]`

## 설명

`snyk code` 명령은 정적 코드 분석을 사용하여 보안 문제를 찾습니다.

자세한 내용은 [CLI for Snyk Code](../../../snyk-products/snyk-code/cli-for-snyk-code/) 참조.

## 하위 명령: `test`

알려진 문제가 있는지 테스트합니다.

## 종료 코드

가능한 종료 코드와 그 의미는 다음과 같습니다.&#x20;

**0**: 성공, 취약점 없음\
**1**: action\_neded, 취약성 발견\
**2**: 실패, 명령 재실행 시도\
**3**: 실패, 지원되는 프로젝트가 검색되지 않음

## Snyk CLI 구성

환경 변수를 사용하여 Snyk CLI를 구성하고 Snyk API로 연결하기 위한 변수를 설정할 수 있습니다. [Snyk CLI 구성](../snyk-cli.md) 참조.

## 디버그

`-d` 옵션을 사용하여 디버그 로그를 출력합니다.

## 코드 테스트 하위 명령 옵션

### `--org=<ORG_ID>`

특정 조직에 연결된 Snyk 명령을 실행할`<ORG_ID>`를 지정합니다. `<ORG_ID>`는 개인 테스트 제한에 영향을 미칩니다.

조직이 여러 개인 경우 다음을 사용하여 CLI에서 기본 값을 설정할 수 있습니다.

`$ snyk config set org=<ORG_ID>`

새로 테스트한 모든 프로젝트가 기본 조직에서 테스트 되도록 기본 값을 설정합니다. 기본 값을 재 정의해야 하는 경우 `--org=<ORG_ID>`옵션을 사용합니다.

기본값: [Account settings](https://app.snyk.io/account)에서 현재 선호하는 조직인 \<ORG\_ID>

`--org=<orgslugname>`을 사용할 수도 있습니다. `ORG_ID`는 CLI와 API 모두에서 작동합니다. 조직 슬러그 이름은 CLI에서 작동하지만 API에서는 작동하지 않습니다.

자세한 내용은 [How to select the organization to use in the CLI](https://support.snyk.io/hc/en-us/articles/360000920738-How-to-select-the-organization-to-use-in-the-CLI) 문서를 참조하십시오.

### `--json`

결과를 JSON 형식으로 인쇄합니다.

예: `$ snyk code test --json`

### `--json-file-output=<OUTPUT_FILE_PATH>`

`--json` 옵션 사용 여부에 관계없이 테스트 출력을 JSON 형식으로 지정된 파일에 직접 저장합니다.

이것은 stdout을 사용하여 human-readable 테스트 출력을 표시하고 동시에 JSON 형식 출력을 파일에 저장하려는 경우에 유용합니다.

예: `$ snyk code test --json-file-output=vuln.json`

### `--sarif`

결과를 SARIF 형식으로 반환합니다.

예:  `$snyk code`

### `--sarif-file-output=<OUTPUT_FILE_PATH>`

`--sarif` 옵션을 사용하는지 여부에 관계없이 테스트 출력을 SARIF 형식으로 \<OUTPUT\_FILE\_PATH> 파일에 직접 저장합니다.

이것은 stdout을 사용하여 human-readable 테스트 출력을 표시하는 동시에 SARIF 형식 출력을 파일에 저장하려는 경우에 특히 유용합니다.

### `--severity-threshold=<low|medium|high|critical>`

지정된 수준 이상의 취약점만 보고합니다. Snyk 코드 구성 문제는 현재 `critical` 심각도 수준을 사용하지 않습니다.
