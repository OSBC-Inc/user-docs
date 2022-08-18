# IaC

## 사용법

`snyk iac <COMMAND> [<OPTIONS>] [<PATH>]`

## 설명

`snyk iac` 명령은 인프라에서 보안 문제를 코드 파일로 찾아 보고하고, 인프라 드리프트 및 관리되지 않는 리소스에 대해 탐지, 추적 및 경고를 하며, .driftigore 파일을 생성합니다.

자세한 내용은 [Snyk CLI for Infrastructure as Code](https://docs.snyk.io/products/snyk-infrastructure-as-code/snyk-cli-for-infrastructure-as-code)를 참조하십시오.

## `snyk iac` 명령 및 도움말 문서

모든 `snyk iac` 명령은 도움말과 함께 여기에 나열됩니다.

* [iac test](broken-reference); `iac test --help`: 알려진 모든 보안 문제에 대한 테스트
* [iac update-exclude-policy](broken-reference); `iac update-exclude-policy --help`: 클라우드 리소스를 제외 `.synk` 제자동 생성\
  Example: `snyk iac describe --json --all | snyk iac update-exclude-policy`
* [iac describe](broken-reference); `iac describe --help`: detects infrastructure drift and unmanaged cloud resources\
  Example: `snyk iac describe --only-unmanaged`
