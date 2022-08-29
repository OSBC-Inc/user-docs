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

Use to indicate how many subdirectories to search. `DEPTH` must be a number, 1 or greater; zero (0) is the current directory.

Default: no limit.

Example: `--detection-depth=3` limits search to the specified directory (or the current directory if no `<PATH>` is specified) plus three levels of subdirectories; zero (0) is the current directory.

### `--org=<ORG_ID>`

Specify the `<ORG_ID>` to run Snyk commands tied to a specific organization. The `<ORG_ID>` influences private test limits.

If you have multiple organizations, you can set a default from the CLI using:

`$ snyk config set org=<ORG_ID>`

Set a default to ensure all newly tested projects are tested under your default organization. If you need to override the default, use the `--org=<ORG_ID>` option.

Default: `<ORG_ID>` that is the current preferred organization in your [Account settings](https://app.snyk.io/account)

Note that you can also use `--org=<orgslugname>`. The `ORG_ID` works in both the CLI and the API. The organization slug name works in the CLI, but not in the API.

For more information see the article [How to select the organization to use in the CLI](https://support.snyk.io/hc/en-us/articles/360000920738-How-to-select-the-organization-to-use-in-the-CLI)

### `--ignore-policy`

Ignore all set policies, the current policy in the `.snyk` file, org level ignores, and the project policy on snyk.io.

### `--policy-path=<PATH_TO_POLICY_FILE>`

Manually pass a path to a `.snyk` policy file.

### `--json`

Print results in JSON format.

Example: `$ snyk iac test --json`

### `--json-file-output=<OUTPUT_FILE_PATH>`

Save test output in JSON format directly to the specified file, regardless of whether or not you use the `--json` option.

This is especially useful if you want to display the human-readable test output using stdout and at the same time save the JSON format output to a file.

Example: `$ snyk iac test --json-file-output=vuln.json`

### `--sarif`

Return results in SARIF format.

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
