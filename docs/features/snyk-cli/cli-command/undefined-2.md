# 구성

## 사용법

`snyk config <SUBCOMMAND> [<OPTIONS>]`

## 설명

`snyk config` 명령은 로컬 Snyk CLI 구성 파일, `$XDG_CONFIG_HOME` 또는 `~/.config` 에 있는 JSON 파일, `configstore/snyk.json`을 관리합니다.

Example: `~/.config/configstore/snyk.json`

이 명령은 프로젝트의 일부인 `.synk` 파일을 관리하지 않습니다.  [`snyk policy`](undefined-5.md) 및 [`snyk ignore`](undefined-4.md) 명령을 참조하십시.

## 디버그

`-d` 옵션을 사용하여 디버그 로그를 출력합니다.

## 하위 명령

### `get <KEY>`

구성 값을 출력합니다.

### `set <KEY>=<VALUE>`

새로운 구성 값을 생성합니다.

### `unset <KEY>`

구성 값을 삭제합니다.

### `clear`

모든 구성 값을 삭제합니다.

## 지원되는 `<KEY>` 값

### `api`

Snyk API를 호출할 때 사용할 API 토큰입니다.

### `endpoint`

사용할 API 끝 지점을 정의합니다.

### `disable-analytics`

분석 보고 기능을 해제합니다.

### `oci-registry-url`

사용자 지정 규칙을 사용하여 IaC 검색에 사용되는 OCI 레지스트리를 구성합니다.

### `oci-registry-username`

사용자 지정 규칙을 사용하여 IaC 검색에 사용되는 OCI 레지스트리의 사용자 이름을 구성합니다.

### `oci-registry-password`

사용자 지정 규칙을 사용하여 IaC 검색에 사용되는 OCI 레지스트리의 암호를 구성합니다.
