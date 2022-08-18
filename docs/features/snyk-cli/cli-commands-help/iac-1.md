# IaC 설명

## 사용법

**참고**: 이 기능은 Snyk CLI 버전 v1.876.0 이상에서 사용할 수 있습니다.

`snyk iac describe [<OPTIONS>]`

## 설명

`snyk iac describe` 명령은  infrastructure drift 및 관리되지 않는 리소스를 감지합니다. Terraform 상태 파일의 리소스를 클라우드 공급자의 실제 리소스와 비교하고 보고서를 출력합니다.

* Terraform 상태 파일의 리소스는 **관리되는 리소스**입니다.
* Terraform 상태 파일에 반영되지 않은 관리 리소스의 변경 내용은 **drifts** 입니다.
* 재하지만 Terraform 상태 파일에 없는 리소스는 **관리되지 않는 리소스**입니다.

자세한 정보 및 예제를 보려면 [IaC describe command examples](https://docs.snyk.io/products/snyk-infrastructure-as-code/detect-drift-and-manually-created-resources/iac-describe-command-examples)를 참조하십시오.

관련 명령 목록은 synk [iac help](https://docs.snyk.io/snyk-cli/commands/iac)를 참조하십시오. `iac --help`

## 종료 코드

가능한 종료 코드와 그 의미는 다음과 같습니다.

**0**: 성공, drift를 찾을 수 없음\
**1**: drifts 또는 관리되지 않는 리소스 발견\
**2**: 실패

## Snyk CLI 구성

Snyk API로 연결하기 위해 환경 변수를 사용하고 변수를 설정할 수 있습니다. [Configure the Snyk CLI](https://docs.snyk.io/snyk-cli/configure-the-snyk-cli)를 참조하십시오.

## Terraform 공급자 구성

`describe` 명령에 사용되는 Terraform 공급자를 구성하도록 환경 변수를 설정할 수 있습니다. [Configure cloud providers](https://docs.snyk.io/products/snyk-infrastructure-as-code/detect-drift-and-manually-created-resources/configure-cloud-providers)를 참조하십시오.

## 디버그

`-d` 옵션을 사용하여 디버그 로그를 출력합니다.

## 필수 옵션

**참고:** `describe` 명령어를 사용한다면 다음 옵션 중 하나를 사용해야 합니다.&#x20;

### `--only-unmanaged`

Terraform 상태에서 보고서 리소스를 찾을 수 없습니다.

### `--only-managed` or `--drift`

Terraform 상태에 있는 관리되는 리소스에서 변경 사항을 검색합니다.

### `--all`

관리되는 리소스와 관리되지 않는 리소스를 모두 검색합니다.

## 옵션 인자

### `--org=<ORG_ID>`

Specify the `<ORG_ID>` to run Snyk commands tied to a specific organization. Overrides the default `<ORG_ID>` that is the current preferred organization in your [Account settings](https://app.snyk.io/account)

Note that you can also use `--org=<orgslugname>`. The `ORG_ID` works in both the CLI and the API. The organization slug name works in the CLI, but not in the API.

For more information see the article [How to select the organization to use in the CLI](https://support.snyk.io/hc/en-us/articles/360000920738-How-to-select-the-organization-to-use-in-the-CLI)

### `--from=<STATE>[,<STATE>...]`

Specify multiple Terraform state files to be read. Glob patterns are supported.

지원되는 IaC 소스 목록 및 사용 방법을 포함한 자세한 내용을 보려면 [IAC Sources usage](https://docs.snyk.io/products/snyk-infrastructure-as-code/detect-drift-and-manually-created-resources/iac-sources-usage)를 참조하십시오.

### `--to=<PROVIDER+TYPE>`

스캔할 클라우드 공급자를 지정합니다(기본값: AWS with Terraform).

지원되는 제공업체:

* `github+tf` (GitHub with Terraform)
* `aws+tf` (Amazon Web Services with Terraform)
* `gcp+tf` (Google Cloud Platform with Terraform)
* `azure+tf` (Azure with Terraform)

### `--tf-provider-version`

사용할 Terraform 공급자 버전을 지정합니다. 아무 것도 지정하지 않으면 기본 버전이 다음과 같이 사용됩니다.

* aws@3.19.0
* github@4.4.0
* google@3.78.0
* azurerm@2.71.0

### `--tf-lockfile`

사용자 지정 경로(기본값: 현재 디렉터리)에서 Terraform 잠금 파일(.terraform.lock.hcl)을 읽습니다.

잠금 파일을 구문 분석하는 데 실패하면 오류가 기록되고 검색이 계속됩니다.

**참고**: `--tf-lockfile` 옵과 `--tf-provider-version` 옵션을 함께 사용할 경우, `--tf-provider-version` 이 우선시됩니다.

### `--fetch-tfstate-headers`

Terraform 상태를 가져올 때 HTTP 백엔드에 특정 HTTP 헤더를 사용합니다.

### `--tfc-token`

Terraform Cloud 또는 Enterprise API를 인증할 API 토큰을 지정합니다.

### `--tfc-endpoint`

조직의 Terraform Enterprise 설치와 관련된 `tfc-endpoint` 값을 전달하여 Terraform Enterprise에서 지정된 워크스페이스의 현재 상태를 읽습니다.

### `--config-dir`

Change the directory path used for `iac describe` configuration (default `$HOME`). This can be useful, for example, if you want to invoke this command in an AWS Lambda function where you can only use the `/tmp` folder.

## Options for including and excluding resources

### `--service=<SERVICE>[,<SERVICE>...]`

Specify the services whose resources are inspected for drift or unmanaged resources.

This option cannot be used with a `.snyk` drift ignore rule; the content in `.snyk` will be ignored.

지원되는 서비스: `aws_s3`, `aws_ec2`, `aws_lambda`, `aws_rds`, `aws_route53`, `aws_iam` , `aws_vpc`, `aws_api_gateway`, `aws_apigatewayv2`, `aws_sqs`, `aws_sns`, `aws_ecr`, `aws_cloudfront`, `aws_kms`, `aws_dynamodb`, `azure_base`, `azure_compute`, `azure_storage`, `azure_network`, `azure_container`, `azure_database`, `azure_loadbalancer`, `azure_private_dns`, `google_cloud_platform`, `google_cloud_storage`, `google_compute_engine`, `google_cloud_dns`, `google_cloud_bigtable`, `google_cloud_bigquery`, `google_cloud_functions`, `google_cloud_sql`, `google_cloud_run`

### `--filter`

Use filter rules.

Filter rules allow you to build a JMESPath expression to include or exclude a set of resources from the report.

To filter on resource attributes, deep mode must be enabled. Deep mode is enabled by default for `--all` and `--only-managed`. To enable deep mode while using `--only-unmanaged`, use the `--deep` option.

For more information see [Filter results](https://docs.snyk.io/products/snyk-infrastructure-as-code/detect-drift-and-manually-created-resources/filter-results)

### `--deep`

Enable deep mode. Deep mode enables you to use the `--filter` option to include or exclude resources in the report based on their attributes.

Deep mode is enabled by default for `--all` and `--only-managed`. Use `--deep` if you want to filter on attributes while using `--only-unmanaged`.

For more information see [Filter results](https://docs.snyk.io/products/snyk-infrastructure-as-code/detect-drift-and-manually-created-resources/filter-results)

### `--strict`

Enable strict mode.

The `iac describe` command ignores service-linked resources by default (like service-linked AWS IAM roles, their policies and policy attachments). To include those resources in the report you can enable **strict mode**. Note that this can create noise when used with an AWS account.

## Options for policies

### `--ignore-policy`

Ignore all set policies, the current policy in the `.snyk` file, org level ignores, and the project policy in the Snyk Web UI.

### `--policy-path=<PATH_TO_POLICY_FILE>`

Manually pass a path to a `.snyk` policy file.

## Options for output

### `--quiet`

Output only the scan result to stdout.

### `--json`

Output the report as JSON to stdout.

### `--html`

Output the report as html to stdout.

### `--html-file-output=<OUTPUT_FILE_PATH>`

Output the report as html into a file.

## Examples for snyk iac describe command

For more examples, see [IaC describe command examples](https://docs.snyk.io/products/snyk-infrastructure-as-code/detect-drift-and-manually-created-resources/iac-describe-command-examples)

### Detect drift and unmanaged resources on AWS with a single local Terraform state

```
$ snyk iac describe --all --from="tfstate://terraform.tfstate"
```

### Specify AWS credentials

```
$ AWS_ACCESS_KEY_ID=XXX AWS_SECRET_ACCESS_KEY=XXX snyk iac describe --all
```

### Use an AWS named profile

```
$ AWS_PROFILE=profile_name snyk iac describe --all
```

### Use a single Terraform state stored on an S3 backend

```
$ snyk iac describe --from="tfstate+s3://my-bucket/path/to/state.tfstate"
```

### Aggregate multiple Terraform states

```
$ snyk iac describe --all --from="tfstate://terraform_S3.tfstate,tfstate://terraform_VPC.tfstate"
```

### Aggregate many Terraform states, using glob pattern

```
$ snyk iac describe --all --from="tfstate://path/to/**/*.tfstate"
```
