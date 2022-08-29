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

환경 변수를 사용하여 Snyk CLI를 구성하고 Snyk API와 연결하기 위한 변수를 설정할 수 있습니다. [Snyk CLI 구성](../snyk-cli.md)을 참조하십시오.

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

Save test output in SARIF format directly to the \<OUTPUT\_FILE\_PATH> file, regardless of whether or not you use the `--sarif` option.

This is especially useful if you want to display the human-readable test output using stdout and at the same time save the SARIF format output to a file.

### `--project-business-criticality=<BUSINESS_CRITICALITY>[,<BUSINESS_CRITICALITY>]...>`

This can be used in combination with the `--report` option.

Set the project business criticality project attribute to one or more values (comma-separated). To clear the project business criticality set `--project-business-criticality=`

Allowed values: `critical, high, medium, low`

For more information see [Project attributes](https://docs.snyk.io/getting-started/introduction-to-snyk-projects/view-project-information/project-attributes)

### `--project-environment=<ENVIRONMENT>[,<ENVIRONMENT>]...>`

This can be used in combination with the `--report` option.

Set the project environment project attribute to one or more values (comma-separated). To clear the project environment set `--project-environment=`

Allowed values: `frontend`, `backend`, `internal`, `external`, `mobile`, `saas`, `onprem`, `hosted`, `distributed`

For more information see [Project attributes](https://docs.snyk.io/getting-started/introduction-to-snyk-projects/view-project-information/project-attributes)

### `--project-lifecycle=<LIFECYCLE>[,<LIFECYCLE>]...>`

This can be used in combination with the `--report` option.

Set the project lifecycle project attribute to one or more values (comma-separated). To clear the project lifecycle set `--project-lifecycle=`

Allowed values: `production`, `development`, `sandbox`

For more information see [Project attributes](https://docs.snyk.io/getting-started/introduction-to-snyk-projects/view-project-information/project-attributes)

### `--project-tags=<TAG>[,<TAG>]...>`

This can be used in combination with the `--report` option.

Set the project tags to one or more values (comma-separated key value pairs with an "=" separator).

Example: `--project-tags=department=finance,team=alpha`

To clear the project tags set `--project-tags=`

### `--remote-repo-url=<URL>`

This can be used in combination with the `--report` option.

Set or override the remote URL for the repository.&#x20;

### `--report`

**NEW** option: Share results with the Snyk Web UI.

This creates a project in your Snyk account with a snapshot of the current configuration issues. After using this option, log in to the Snyk website and view your projects to see the monitor.

Example: `$ snyk iac test --report`

Note: This option cannot be used in combination with the `--rules` option.

### `--rules=<PATH_TO_CUSTOM_RULES_BUNDLE>`

Use this dedicated option for Custom Rules scanning to enable the IaC scans to use a custom rules bundle generated with the `snyk-iac-rules` SDK. See [`snyk-iac-rules` SDK](https://github.com/snyk/snyk-iac-rules#readme)

This option cannot be used if the custom rules settings were configured with the Snyk UI. Default: If the `--rules` flag is not specified, scan the configuration files using the internal Snyk rules only.

Example: Scan the configuration files using custom rules and internal Snyk rules.

`--rules=bundle.tar.gz`

Note: This option can not be used in combination with the `--report` option.

### `--severity-threshold=<low|medium|high|critical>`

Report only vulnerabilities at the specified level or higher.

### `--scan=<TERRAFORM_PLAN_SCAN_MODE>`

Use this dedicated option for Terraform plan scanning modes to control whether the scan analyzes the full final state (for example, `planned-values`), or the proposed changes only (for example, `resource-changes`).

Default: If the `--scan` option is not specified, scan the proposed changes only by default. Example 1: `--scan=planned-values` (full state scan)\
Example 2: `--scan=resource-changes` (proposed changes scan)

### `--target-name=<TARGET_NAME>`

This can be used in combination with the `--report` option.

Set or override the project name for the repository.&#x20;

Note: This flag will supersede the `--remote-repo-url`, if used together.

### `--target-reference=<TARGET_REFERENCE>`

This can be used in combination with the `--report` option.

Specify a reference which differentiates this project, for example, a branch name or version. Projects having the same reference can be grouped based on that reference.

Example, setting to the current Git branch:

`snyk iac test myproject/ --report --target-reference="$(git branch --show-current)"`

\
Example, setting to the latest Git tag:

`snyk iac test myproject/ --report --target-reference="$(git describe --tags --abbrev=0)"`

### `--var-file=<PATH_TO_VARIABLE_FILE>`

Use this option to load a terraform variable definitions file that is located in a different directory from the scanned one.

Example:

`$ snyk iac test myproject/staging/networking --var-file=myproject/vars.tf`

## Examples for snyk iac test command

For more information see [Snyk CLI for Infrastructure as Code](https://docs.snyk.io/products/snyk-infrastructure-as-code/snyk-cli-for-infrastructure-as-code)

### Test a CloudFormation file

```
$ snyk iac test /path/to/cloudformation_file.yaml
```

### Test a Kubernetes file

```
$ snyk iac test /path/to/kubernetes_file.yaml
```

### Test a Terraform file

```
$ snyk iac test /path/to/terraform_file.tf
```

### Test a Terraform plan file

```
$ terraform plan -out=tfplan.binary
$ terraform show -json tfplan.binary > tf-plan.json
$ snyk iac test tf-plan.json
```

### Test an ARM file

```
$ snyk iac test /path/to/arm_file.json
```

### Test matching files in a directory

```
$ snyk iac test /path/to/directory
```

### Test matching files in a directory using a local custom rules bundle

```
$ snyk iac test /path/to/directory --rules=bundle.tar.gz
```
