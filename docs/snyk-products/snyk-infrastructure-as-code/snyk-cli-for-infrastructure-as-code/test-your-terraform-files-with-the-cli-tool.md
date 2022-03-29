# CLI를 사용하여 Terraform 파일 테스트

Snyk Infrastructure as Code를 사용하면 CLI에서 정적 구성 파일과 Terraform Plan output을 모두 스캔할 수 있습니다.

|                                   | **Terraform 설정 파일** | **Terraform Plan 파일**  |
| --------------------------------- | ------------------- | ---------------------- |
| **Identify configuration issues** | Yes                 | Yes                    |
| **Process Variables**             | No                  | Yes                    |
| **Scan Terraform Modules**        | No                  | Yes - public & private |

## Terraform 구성 파일

CLI를 사용하여 `main.tf`와 같은 구성 파일을 스캔할 수 있습니다.

외부 모듈은 현재 지원되지 않습니다.

변수 처리에 대한 자세한 내용은 [Terraform 변수 지원](https://docs.snyk.io/products/snyk-infrastructure-as-code/scan-terraform-files/terraform-variables-support)을 참조하십시오.

## 구성 파일 스캔

파일 이름 또는 전체 디렉토리를 지정할 수 있습니다.

```
snyk iac test main.tf
snyk iac test .
```

## Terraform Plan

Terraform Plan은 구성 파일을 작성하는 것과 변경 사항을 배포하는 사이에 실행되는 단계입니다.

`$ terraform plan`은 원하는 상태에 맞추기 위해 대상 환경에 적용해야 하는 변경 사항을 식별합니다.

이 Plan 단계에서는 대상 Terraform 배포에 사용되는 모든 변수와 Terraform 모듈이 고려됩니다.

사용자 정의 Terraform 모듈을 작성하고 배포에서 참조하는 경우 Terraform Plan 출력에 포함되고 그에 따라 스캔됩니다. 이는 Terraform Plan 출력이 보안 관점에서 스캔할 수 있는 완전한 아티팩트를 제공한다는 것을 의미합니다.

추가적으로 버전 **1.594.0**의 Snyk IaC CLI를 사용하여 이 아티팩트를 스캔할 수 있습니다.

이 파일은 처리하기 위해 Snyk으로 전송하지 않으며 CLI 내에서 로컬로 스캔하고 시스템을 떠나지 않습니다.

## Terraform Plan output 스캔 진행

유효한 JSON 파일로 저장해야 하는 Terraform Plan output 경로를 제공합니다.

```
snyk iac test tf-plan.json
```

기본적으로 인프라에 적용하는 변경 사항을 스캔합니다.

`--scan=` 옵션을 제공하여 해당 동작을 변경할 수 있습니다.

* `--scan=resource-changes`는 기본 동작입니다. `$ terraform apply`를 실행한 경우 인프라 변경 내용만 스캔합니다.
* `--scan=planed-values`는 전체 plan 상태를 스캔하여 기존 인프라의 결과와 변경 사항을 제공합니다.

아직 Terraform Plan output을 JSON 파일로 저장하지 않은 경우 다음 단계를 진행해야 할 수 있습니다.

```
terraform plan -out=tfplan.binary
terraform show -json tfplan.binary > tf-plan.json
```

필요에 따라 `tf-plan.json` 파일의 이름을 지정할 수 있습니다.

이러한 파일은 민감한 것으로 간주되며 commit하지 않는 것이 좋습니다.

## 문제 해결

#### 정적 파일 스캔과 Plan output 사이에는 차이가 있습니다.

다음과 같은 이유로 발생합니다.

* **변수** - Terraform Plan output에서 변수에 저장된 값을 고려합니다.
* **Terraform Modules** - Terraform Plan output에는 사용 중인 Terraform Modules에서 발견된 모든 구성 문제가 포함됩니다.
* **Delta** - 기본적으로 Terraform Plan output을 스캔하면 전체 배포가 아닌 변경 사항에 대한 구성 문제만 스캔합니다. 반면 정적 스캔은 모든 파일을 살펴봅니다. `--scan=planning-valules`를 추가하여 검색을 다시 실행해 보십시오.

```
Note: the flag --experimental is not required anymore when testing your Terraform projects.
```

위에서 발견하지 않은 항목이 발견되면 지원 요청을 제출하십시오.
