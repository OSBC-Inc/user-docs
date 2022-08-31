# IaC update-exclude-policy

## 사용법

`snyk iac update-exclude-policy [<OPTIONS>]`

## 설명

`snyk iac update-exclude-policy`는 snyk iac 설명에서 사용할 제외 정책 규칙을 생성합니다.

관련 명령 목록은 [snyk iac](iac.md) 도움말을 참조하십시오; `iac --help`

자세한 내용은 [Ignore resources](https://docs.snyk.io/products/snyk-infrastructure-as-code/detect-drift-and-manually-created-resources/ignore-resources)를 참조하세요.

## 종료 코드

사용 가능한 종료 코드 및 그 의미:

**0**: 성공, 성공적으로 생성된 규칙 제외\
**1**: 오류, 제외 규칙 생성 중에 문제가 발생

## Snyk CLI 구성

환경 변수를 사용하여 Snyk CLI를 구성하고 Snyk API와 연결하기 위한 변수를 설정할 수 있습니다. [Snyk CLI 구성](../snyk-cli-1.md)을 참조하십시오.

## Debug

`-d` 옵션을 사용하여 디버그 로그를 출력합니다.

## 옵션

### `--exclude-changed`

클라우드 공급자에서 변경된 리소스를 제외합니다.

### `--exclude-missing`

누락된 리소스를 제외합니다.

### `--exclude-unmanaged`

IaC에서 관리하지 않는 리소스를 제외합니다.

## 예시

```
$ snyk iac describe --json --all | snyk iac update-exclude-policy
```
