# Snyk Infrastructure as Code

Snyk IaC(Infrastructure as Code)는 개발자가 안전한 애플리케이션 구성을 작성할 수 있도록 지원합니다. Snyk IaC는 애플리케이션이 운영 환경에 도달하기 전에 직접 코드를 변경할 수 있도록 수정 조언을 제공합니다.

Snyk IaC는 개발자가 [HashiCorp Terraform](scan-terraform-files/), [AWS CloudFormation](scan-cloudformation-files/), [Kubernetes](scan-kubernetes-configuration-files/), [ARM(Azure Resource Manager)](scan-arm-configuration-files.md)을 위한 보안 구성을 작성할 수 있도록 지원합니다.

### 잘못된 구성 탐지 및 수정

Kubernetes에 안전하게 배포하는 방법 또는 Terraform을 사용하여 인프라를 안전하게 프로비저닝하는 방법은 잘못되기 쉬워서 구성 오류(**misconfigurations**)가 발생할 수 있습니다. 이러한 잘못된 구성은 보안 문제를 일으킬 수 있습니다. 연구에 따르면 안전하지 않은 클라우드 스토리지와 같은 잘못된 구성은 금융 및 보험 분야에서 위반으로 이어지는 두 번째로 흔한 오류입니다.

#### Snyk IaC와 잘못된 구성

Snyk IaC는 잘못된 구성에 대한 보안 검사를 개발 라이프사이클에 통합합니다.

* [Snyk CLI for Infrastructure as Code](snyk-cli-for-infrastructure-as-code/)는 구성을 작성하는 즉시 로컬 피드백을 제공하므로 커밋하기 전에 문제를 해결할 수 있습니다.
* CI/CD 프로세스에 Snyk를 통합하여 보안 검사를 자동화합니다.
* 지속적인 모니터링 및 분석을 위해 소스 저장소를 Snyk으로 가져옵니다.
* Hashicorp Terraform Cloud와 통합하여 배포 파이프라인의 일부로 스캔이 가능합니다.

### Snyk IaC 보안 규칙

Snyk IaC는 업계 벤치마크, 클라우드 공급자 모범 사례 및 Snyk 보안 인텔리전스 팀의 위협 모델 연구를 기반으로 [사전 정의된 포괄적인 보안 규칙 세트](https://snyk.io/security-rules)가 있습니다.

OPA(Open Policy Agent)를 활용하여 [사용자 지정 규칙을 구축](custom-rules/)할 수 있습니다.
