# Snyk CLI로 Terraform 파일 테스트

Snyk Infrastructure as Code에서 CLI를 사용하여 정적 구성 파일과 Terraform Plan 출력을 모두 검색할 수 있습니다.

|                                   | **Terraform configuration files** | **Terraform Plan file** |
| --------------------------------- | --------------------------------- | ----------------------- |
| **Identify configuration issues** | Yes                               | Yes                     |
| **Process Variables**             | No                                | Yes                     |
| **Scan Terraform Modules**        | No                                | Yes - public & private  |

## Terraform 구성 파일

CLI를 사용하여 `main.tf`와 같은 구성 파일을 검색할 수 있습니다.

참조하는 선언된 변수 또는 외부 모듈은 고려하지 않습니다.

## 구성 파일 스캔

파일 이름 또는 전체 디렉토리를 지정할 수 있습니다.

```
snyk iac test main.tf
snyk iac test .
```

## Terraform Plan

Terraform Plan은 구성 파일을 작성하는 것과 변경 사항을 배포하는 사이에 실행되는 단계입니다.

`$ terraform plan`은 원하는 상태에 맞게 대상 환경을 변경해야 하는 사항을 식별합니다.

이 계획 단계에서는 대상 테라폼 배포에 사용되는 모든 변수와 테라폼 모듈을 고려합니다.

사용자 정의 테라폼 모듈을 작성한 후 배포에서 참조하는 경우 테라폼 계획 출력에 포함되고 그에 따라 스캔됩니다.

이는 Terraform Plan 출력이 보안 관점에서 스캔할 수 있는 완전한 아티팩트를 제공한다는 것을 의미합니다.

이제 버전 **1.594.0**의 Snyk IaC CLI를 사용하여 이 artefact를 스캔할 수 있습니다.

이 파일은 처리하기 위해 Snyk으로 전송하지 않으며 CLI 내에서 로컬로 검색하며 시스템을 떠나지 않습니다.

## To scan Terraform Plan output:

Provide the path to your Terraform Plan output which must be stored as a valid JSON file.

```
snyk iac test tf-plan.json
```

By default, we will scan the changes that will be made to your infrastructure, not the full infrastructure.

You can change this behaviour by providing the `--scan=` flag

* `--scan=resource-changes` is the default behaviour. This will scan only the changes that are going to be made to your infrastructure if you ran `$ terraform apply`
* `--scan=planned-values` will scan the full planned state, providing results of the existing infrastructure plus changes that will be made.

If you do not already have your terraform plan output saved as JSON file, you may need to follow these steps:

```
terraform plan -out=tfplan.binary
terraform show -json tfplan.binary > tf-plan.json
```

You can name the tf-plan.json file according to your needs.

These files are considered sensitive and is not recommended to commit them to source control.

## Troubleshooting

### There are differences between scanning the static files & plan output

This could be due to the following

* **Variables** - Terraform Plan output considers the values stored in variables
* **Terraform Modules** - Terraform Plan output will include any configuration issues found from Terraform Modules that you may be using
* **Delta** - By default, scanning the Terraform Plan output will only scan for configuration issues on the changes that will be made, not the whole deployment. Whereas the static scan looks at all of the files. Try re-running the scan with `--scan=planned-values` appended

```
Note: the flag --experimental is not required anymore when testing your Terraform projects.
```

If you have found a discrepancy that you cannot explain with the above, please raise a support ticket.
