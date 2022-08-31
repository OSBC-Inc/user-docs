# IaC 테스트

## 사용법

`snyk iac test [<OPTIONS>] [<PATH>]`

## 설명

`snyk iac test` command는 알려진 보안 문제에 대해 테스트합니다.

관련 명령 목록은 [snyk iac](iac.md) 도움말을 참조하십시오; `iac --help`

자세한 내용은 [Infrastructure as Code용 Snyk CLI](../../../snyk-products/snyk-infrastructure-as-code/snyk-cli-for-infrastructure-as-code/)를 참조하십시오.

## 종료 코드

사용 가능한 종료 코드 및 그 의미:

**0**: 성공, 발견된 취약점 없음\
**1**: action\_needed, 취약점 발견\
**2**: 실패, command 다시 실행하십시오.\
**3**: 실패, 지원되는 프로젝트가 감지되지 않음

## Snyk CLI 구성

환경 변수를 사용하여 Snyk CLI를 구성하고 Snyk API와 연결하기 위한 변수를 설정할 수 있습니다. [Snyk CLI 구성](../snyk-cli-1.md)을 참조하십시오.

## Debug

`-d` 옵션을 사용하여 디버그 로그를 출력합니다.

## 옵션

### `--detection-depth=<DEPTH>`

검색할 하위 디렉터리 수를 나타내는 데 사용합니다. `DEPTH`는 1 이상의 숫자여야 합니다. 영(0)은 현재 디렉토리입니다.

기본값: 제한 없음.

예: `--detection-depth=3`은 검색을 지정된 디렉터리(또는 `<PATH>` 가 지정되지 않은 경우 현재 디렉터리)와 세 가지 수준의 하위 디렉터리로 제한합니다. 영(0)은 현재 디렉토리입니다.

### `--org=<ORG_ID>`

특정 조직에 연결된 Snyk 명령을 실행하려면 `<ORG_ID>`를 지정하십시오. `<ORG_ID>`는 비공개 테스트 제한에 영향을 줍니다.

여러 조직이 있는 경우 다음을 사용하여 CLI에서 기본값을 설정할 수 있습니다:

`$ snyk config set org=<ORG_ID>`

새로 테스트된 모든 프로젝트가 기본 조직에서 테스트 되도록 기본값을 설정합니다. 기본값을 재정의해야 하는 경우 `--org=<ORG_ID>` 옵션을 사용합니다.

기본값: [계정 설정](https://app.snyk.io/login?redirectUri=L2FjY291bnQ%3D\&from=snyk\_auth\_link)에서 현재 선호하는 조직인 \<ORG\_ID>

주의: --org=을 사용할 수도 있습니다. ORG\_ID는 CLI와 API 모두에서 작동합니다. 조직 슬러그 이름은 CLI에서 작동하지만 API에서는 작동하지 않습니다.

자세한 내용은 [How to select the organization to use in the CLI](https://support.snyk.io/hc/en-us/articles/360000920738-How-to-select-the-organization-to-use-in-the-CLI) 문서를 참조하십시오.

### `--ignore-policy`

설정된 모든 정책, `.snyk` 파일의 현재 정책, 조직 수준 무시 및 snyk.io의 프로젝트 정책을 무시합니다.

### `--policy-path=<PATH_TO_POLICY_FILE>`

`.snyk` 정책 파일에 대한 경로를 수동으로 전달합니다.

### `--json`

결과를 JSON 형식으로 인쇄합니다.

Example: `$ snyk iac test --json`

### `--json-file-output=<OUTPUT_FILE_PATH>`

`--json` 옵션 사용 여부에 관계없이 테스트 출력을 JSON 형식으로 지정된 파일에 직접 저장합니다.

이것은 표준 출을 사용하여 사람이 읽을 수 있는 테스트 출력을 표시하고 동시에 JSON 형식 출력을 파일에 저장하려는 경우에 특히 유용합니다.

Example: `$ snyk iac test --json-file-output=vuln.json`

### `--sarif`

결과를 SARIF 형식으로 반환합니다.

### `--sarif-file-output=<OUTPUT_FILE_PATH>`

`--sarif` 옵션을 사용하는지 여부에 관계없이 테스트 출력을 SARIF 형식으로 \<OUTPUT\_FILE\_PATH> 파일에 직접 저장합니다.

이것은 stdout을 사용하여 사람이 읽을 수 있는 테스트 출력을 표시하는 동시에 SARIF 형식 출력을 파일에 저장하려는 경우에 특히 유용합니다.

### `--project-business-criticality=<BUSINESS_CRITICALITY>[,<BUSINESS_CRITICALITY>]...>`

`--report` 옵션과 함께 사용할 수 있습니다.

프로젝트 비즈니스의 중요도는 프로젝트 속성을 하나 이상의 값(쉼표로 구분)으로 설정하십시오. 프로젝트 비즈니스 중요도 설정을 지우려면`--project-business-criticality=`를 설정합니다.

허용되는 값: `critical, high, medium, low`

자세한 내용은 [Project attributes](https://docs.snyk.io/getting-started/introduction-to-snyk-projects/view-project-information/project-attributes) 참조하세요.

### `--project-environment=<ENVIRONMENT>[,<ENVIRONMENT>]...>`

`--report` 옵션과 함께 사용할 수 있습니다.

프로젝트 환경 프로젝트 속성을 하나 이상의 값(쉼표로 구분)으로 설정하십시오. 프로젝트 환경을 지우려면 `--project-environment=`

허용되는 값: `frontend`, `backend`, `internal`, `external`, `mobile`, `saas`, `onprem`, `hosted`, `distributed`를 설정합니다.

자세한 내용은 [Project attributes](https://docs.snyk.io/getting-started/introduction-to-snyk-projects/view-project-information/project-attributes) 참조하세요.

### `--project-lifecycle=<LIFECYCLE>[,<LIFECYCLE>]...>`

`--report` 옵션과 함께 사용할 수 있습니다.

프로젝트 수명 주기의 프로젝트 속성을 하나 이상의 값(쉼표로 구분)으로 설정합니다. 프로젝트 수명 주기를 지우려면 `--project-lifecycle=` 를 설정합니다.

허용되는 값: `production`, `development`, `sandbox`

자세한 내용은 [Project attributes](https://docs.snyk.io/getting-started/introduction-to-snyk-projects/view-project-information/project-attributes) 참조하세요.

### `--project-tags=<TAG>[,<TAG>]...>`

`--report` 옵션과 함께 사용할 수 있습니다.

프로젝트 태그를 하나 이상의 값("=" 구분 기호가 있는 쉼표로 구분된 키 값 쌍)으로 설정합니다.

예: `--project-tags=department=finance,team=alpha`

프로젝트 태그 세트를 지우려면 `--project-tags=`를 설정합니다.

### `--remote-repo-url=<URL>`

`--report` 옵션과 함께 사용할 수 있습니다.

리포지토리에 대한 원격 URL을 설정하거나 재정의합니다.

### `--report`

**새로운** 옵션: Snyk Web UI와 결과를 공유합니다.

이렇게 하면 현재 구성 문제의 스냅샷이 있는 Snyk 계정에 프로젝트가 생성됩니다. 이 옵션을 사용한 후 Snyk 웹사이트에 로그인하고 프로젝트를 보고 모니터를 봅니다.

Example: `$ snyk iac test --report`

주의: 이 옵션은 `--rules` 옵션과 함께 사용할 수 없습니다.

### `--rules=<PATH_TO_CUSTOM_RULES_BUNDLE>`

IaC 스캔이 `snyk-iac-rules` SDK로 생성된 사용자 정의 규칙 번들을 사용하도록 하려면 사용자 정의 규칙 스캔에 이 전용 옵션을 사용하십시오. [snyk-iac-rules](https://github.com/snyk/snyk-iac-rules#readme) SDK 참조

사용자 정의 규칙 설정이 Snyk UI로 구성된 경우 이 옵션을 사용할 수 없습니다.\
기본값: --rules 플래그가 지정되지 않은 경우 내부 Snyk 규칙만 사용하여 구성 파일을 스캔합니다.

예: 사용자 정의 규칙 및 내부 Snyk 규칙을 사용하여 구성 파일을 스캔합니다.

`--rules=bundle.tar.gz`

주의: 이 옵션은 `--report` 옵션과 함께 사용할 수 없습니다.

### `--severity-threshold=<low|medium|high|critical>`

지정된 수준 이상의 취약점만 보고합니다.

### `--scan=<TERRAFORM_PLAN_SCAN_MODE>`

Terraform plan scanning modes에 대해 이 전용 옵션을 사용하여 스캔이 전체 최종 상태(예: `planned-values`)를 분석할지 아니면 제안된 변경만(예: `resource-changes`) 분석할지 여부를 제어합니다.

기본값: `--scan` 옵션이 지정되지 않은 경우 기본적으로 제안된 변경 사항만 검색합니다.\
예 1: `--scan=planned-values` (전체 상태 스캔)\
예 2: `--scan=resource-changes` (제안된 변경 사항 스캔)

### `--target-name=<TARGET_NAME>`

`--report` 옵션과 함께 사용할 수 있습니다.

리포지토리의 프로젝트 이름을 설정하거나 재정의합니다.

주의: 이 플래그는 함께 사용되는 경우 --remote-repo-url을 대체합니다.

### `--target-reference=<TARGET_REFERENCE>`

`--report` 옵션과 함께 사용할 수 있습니다.

이 프로젝트를 구별하는 참조를 지정하십시오(예: 분기 이름 또는 버전). 참조가 동일한 프로젝트는 해당 참조를 기반으로 그룹화할 수 있습니다.

예, 현재 Git branch분기로 설정:

`snyk iac test myproject/ --report --target-reference="$(git branch --show-current)"`

\
예, 최신 Git 태그로 설정:

`snyk iac test myproject/ --report --target-reference="$(git describe --tags --abbrev=0)"`

### `--var-file=<PATH_TO_VARIABLE_FILE>`

스캔한 디렉토리와 다른 디렉토리에 있는 terraform 변수 정의 파일을 로드하려면 이 옵션을 사용하십시오.

예:

`$ snyk iac test myproject/staging/networking --var-file=myproject/vars.tf`

## snyk iac 테스트 명령의 예

자세한 내용은 [Infrastructure as Code용 Snyk CLI](../../../snyk-products/snyk-infrastructure-as-code/snyk-cli-for-infrastructure-as-code/)를 참조하십시오.

### CloudFormation 파일 테스트

```
$ snyk iac test /path/to/cloudformation_file.yaml
```

### Kubernetes 파일 테스트

```
$ snyk iac test /path/to/kubernetes_file.yaml
```

### Terraform 파일 테스트

```
$ snyk iac test /path/to/terraform_file.tf
```

### Terraform plan 파일 테스트

```
$ terraform plan -out=tfplan.binary
$ terraform show -json tfplan.binary > tf-plan.json
$ snyk iac test tf-plan.json
```

### ARM 파일 테스트

```
$ snyk iac test /path/to/arm_file.json
```

### 디렉토리에서 일치하는 파일 테스트

```
$ snyk iac test /path/to/directory
```

### 로컬 사용자 정의 규칙 번들을 사용하여 디렉토리에서 일치하는 파일 테스트

```
$ snyk iac test /path/to/directory --rules=bundle.tar.gz
```
