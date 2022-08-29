# IaC

## 사용법

`snyk iac <COMMAND> [<OPTIONS>] [<PATH>]`

## 설명

`snyk iac` 명령은 인프라에서 보안 문제를 코드 파일로 찾아 보고하고, 인프라 드리프트 및 관리되지 않는 리소스에 대해 탐지, 추적 및 경고를 하며, .driftigore 파일을 생성합니다.

자세한 내용은 [Infrastructure as Code용 Snyk CLI](../../../snyk-products/snyk-infrastructure-as-code/snyk-cli-for-infrastructure-as-code/)를 참조하십시오.

## `snyk iac` 명령 및 도움말 문서

모든 `snyk iac` 명령은 도움말과 함께 여기에 나열됩니다.

* [iac 테스트](iac-2.md); `iac test --help`: 알려진 모든 보안 문제에 대한 테스트
* [iac update-exclude-policy](iac-update-exclude-policy.md); `iac update-exclude-policy --help`: 클라우드 리소스를 제외한 `.synk` 자동 생성\
  예: `snyk iac describe --json --all | snyk iac update-exclude-policy`
* [iac 설명](iac-1.md); `iac describe --help`: 인프라 이동 및 관리되지 않는 클라우드 리소스 감지\
  예: `snyk iac describe --only-unmanaged`
