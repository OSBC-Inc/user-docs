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

관련 명령 목록은 Synk [IaC](iac.md)를 참조하십시오. `iac --help`

## 종료 코드

가능한 종료 코드와 그 의미는 다음과 같습니다.

**0**: 성공, drift를 찾을 수 없음\
**1**: drifts 또는 관리되지 않는 리소스 발견\
**2**: 실패

## Snyk CLI 구성

Snyk API로 연결하기 위해 환경 변수를 사용하고 변수를 설정할 수 있습니다. [Snyk CLI 구성을](../snyk-cli.md) 참조하십시오.

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

특정 조직에 연결된 Snyk command를 실행하려면 `<ORG_ID>`를 지정하십시오. [계정 설정](https://app.snyk.io/login?redirectUri=L2FjY291bnQ%3D\&from=snyk\_auth\_link)에서 현재 선호하는 조직인 기본 `<ORG_ID>`를 무시합니다.

`--org=<orgslugname>`을 사용할 수도 있습니다 . `ORG_ID`는 CLI와 API 모두에서 작동합니다. 조직 슬래그 이름은 CLI에서 작동하지만 API에서는 작동하지 않습니다.

자세한 내용은 문서 [How to select the organization to use in the CLI](https://support.snyk.io/hc/en-us/articles/360000920738-How-to-select-the-organization-to-use-in-the-CLI)를 참조하십시오.

### `--from=<STATE>[,<STATE>...]`

읽을 여러 Terraform 상태 파일을 지정합니다. Glob 패턴이 지원됩니다.

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

`iac describe` 구성에 사용되는 디렉토리 경로(기본값 $HOME)를 변경합니다. 예로 /`tmp` 폴더만 사용할 수 있는 AWS Lambda 함수에서 이 명령을 호출하려는 경우에 유용합니다.

## 리소스 포함 및 제외 옵션

### `--service=<SERVICE>[,<SERVICE>...]`

리소스가 드리프트 또는 관리되지 않는 리소스에 대해 검사되는 서비스를 지정합니다.

이 옵션은 `.snyk` drift 무시 규칙과 함께 사용할 수 없습니다. `.snyk`의 내용은 무시됩니다.

지원되는 서비스: `aws_s3`, `aws_ec2`, `aws_lambda`, `aws_rds`, `aws_route53`, `aws_iam` , `aws_vpc`, `aws_api_gateway`, `aws_apigatewayv2`, `aws_sqs`, `aws_sns`, `aws_ecr`, `aws_cloudfront`, `aws_kms`, `aws_dynamodb`, `azure_base`, `azure_compute`, `azure_storage`, `azure_network`, `azure_container`, `azure_database`, `azure_loadbalancer`, `azure_private_dns`, `google_cloud_platform`, `google_cloud_storage`, `google_compute_engine`, `google_cloud_dns`, `google_cloud_bigtable`, `google_cloud_bigquery`, `google_cloud_functions`, `google_cloud_sql`, `google_cloud_run`

### `--filter`

필터 규칙을 사용합니다.

필터 규칙을 사용하여 리소스 집합을 리포트에서 포함하거나 제외하는 JMESPath 식을 작성할 수 있습니다.

리소스 특성을 기준으로 필터링하려면 심층 모드를 사용하도록 설정해야 합니다. 딥 모드는 `--all` 및 `--only-managed`에 대해 기본적으로 사용 가능합니다. `--only-unmanaged`를 사용하는 동안 딥 모드를 사용하려면 `--deep` 옵션을 사용하십시오.

자세한 내용은 [Filter results](https://docs.snyk.io/products/snyk-infrastructure-as-code/detect-drift-and-manually-created-resources/filter-results)를 참조하십시오.

### `--deep`

딥 모드를 활성화합니다. 심층 모드를 사용하면 `--filter` 옵션을 사용하여 속성에 따라 리포트에 리소스를 포함하거나 제외할 수 있습니다.

딥 모드는 `--all` 및 `--only-managed`에 대해 기본적으로 사용 가능합니다.

자세한 내용은 [Filter results](https://docs.snyk.io/products/snyk-infrastructure-as-code/detect-drift-and-manually-created-resources/filter-results)를 참조하십시오.

### `--strict`

엄격모드를 활성화합니다.

`iac describe` 명령은 기본적으로 서비스 연결 리소스(예: 서비스 연결 AWS IAM 역할, 해당 정책 및 정책 연결)를 무시합니다. 보고서에 이러한 리소스를 포함하려면 엄격 모드를 활성화할 수 있습니다. AWS 계정과 함께 사용하면 소음이 발생할 수 있습니다.

### `--ignore-policy`

설정된 모든 정책, `.snyk` 파일의 현재 정책, 조직 수준 무시 및 Snyk 웹 UI의 프로젝트 정책을 무시합니다.

### `--policy-path=<PATH_TO_POLICY_FILE>`

`.snyk` 정책 파일에 대한 경로를 수동으로 전달합니다.

## Options for output

### `--quiet`

스캔 결과만 표준 출력합니다.

### `--json`

보고서를 JSON형식으로 표준 출력합니다.

### `--html`

보고서를 html형식으로 표준 출력합니다.

### `--html-file-output=<OUTPUT_FILE_PATH>`

보고서를 파일에 html형식으로 출력합니다.

## snyk iac 설명 command의 예

더 많은 예는 [IaC describe command examples](https://docs.snyk.io/products/snyk-infrastructure-as-code/detect-drift-and-manually-created-resources/iac-describe-command-examples)를 참조하십시오.

### 단일 로컬 Terraform 상태로 AWS에서 드리프트 및 관리되지 않는 리소스 감지

```
$ snyk iac describe --all --from="tfstate://terraform.tfstate"
```

### AWS 자격 증명 지정

```
$ AWS_ACCESS_KEY_ID=XXX AWS_SECRET_ACCESS_KEY=XXX snyk iac describe --all
```

### AWS 명명된 프로필 사용

```
$ AWS_PROFILE=profile_name snyk iac describe --all
```

### S3 백엔드에 저장된 단일 Terraform 상태 사용

```
$ snyk iac describe --from="tfstate+s3://my-bucket/path/to/state.tfstate"
```

### 여러 Terraform 상태 집계

```
$ snyk iac describe --all --from="tfstate://terraform_S3.tfstate,tfstate://terraform_VPC.tfstate"
```

### glob 패턴을 사용하여 많은 Terraform 상태 집계

```
$ snyk iac describe --all --from="tfstate://path/to/**/*.tfstate"
```
