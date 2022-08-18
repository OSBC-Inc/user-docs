# 컨테이너

## 사용법

`snyk container <SUBCOMMAND> [<OPTIONS>] [<IMAGE>]`

## 설명

`snyk container` 명령은 컨테이너 이미지의 취약성을 테스트합니다.`-d` 옵션을 사용하여 디버그 로그를 출력합니다.

## 하위 명령

### `test`

알려진 취약성을 테스트합니다.

### `monitor`

컨테이너 이미지 레이어 및 종속성을 캡처하고 [snyk.io](https://snyk.io) 에 대한 취약점을 모니터링 합니다.&#x20;

## Exit codes

가능한 종료 코드와 그 의미는 다음과 같습니다.

**0**: 성공, 취약점 없음\
**1**: 작업 필요, 취약성 발견\
**2**: 실패, 명령 재실행 시도\
**3**: 실패, 지원되는 프로젝트가 검색되지 않음

## Snyk CLI 구성

환경 변수를 사용하여 Snyk CLI를 구성하고 Snyk API로 연결하기 위한 변수를 설정할 수 있습니다.

컨테이너 명령에 적용되는 환경 변수가 있습니다. [Configure the Snyk CLI](https://docs.snyk.io/features/snyk-cli/configure-the-snyk-cli) 참

## 디버그

Use the `-d` option to output the debug logs.

### 컨테이너 테스트 및 컨테이너 모니터 하위 명령 옵션

### `--print-deps`

분석을 위해 보내기 전에 종속성 트리를 출하십시오.

### `--org=<ORG_ID>`

`<ORG_ID>`를 지정하여 특정 조직에 연결된 Snyk 명령을 실행합니다. `<ORG_ID>`는 일부 기능 가용성 및 개인 테스트 제한에 영향을 미칩니다.

조직이 여러 개인 경우 다음을 사용하여 CLI에서 기본값을 설정할 수 있습니다.

`$ snyk config set org=<ORG_ID>`

새로 테스트되고 모니터링되는 모든 프로젝트가 기본 조직에서 테스트 되고 모니터링 되도록 하려면 기본 값을 설정합니다. 기본 값을 재정의해야 하는 경우 `--org=<ORG_ID>` 옵션을 사용하십시오.

기본값: `<ORG_ID>` 는 사용자의 [Account settings](https://app.snyk.io/account)ㅁ

Note that you can also use `--org=<orgslugname>`. The `ORG_ID` works in both the CLI and the API. The organization slug name works in the CLI, but not in the API.

For more information see the article [How to select the organization to use in the CLI](https://support.snyk.io/hc/en-us/articles/360000920738-How-to-select-the-organization-to-use-in-the-CLI)

### `--file=<FILE_PATH>`

For more detailed advice, include the path to the Dockerfile for the image.

### `--project-name=<PROJECT_NAME>`

Specify a custom Snyk project name.

### `--policy-path=<PATH_TO_POLICY_FILE>`

Manually pass a path to a `.snyk` policy file.

### `--json`

Print results in JSON format, useful for integrating with other tools

Example: `$ snyk container test --json`

### `--json-file-output=<OUTPUT_FILE_PATH>`

Save test output in JSON format directly to the specified file, regardless of whether or not you use the `--json` option.

This is especially useful if you want to display the human-readable test output using stdout and at the same time save the JSON format output to a file.

Example: `$ snyk container test --json-file-output=vuln.json`

### `--sarif`

Return results in SARIF format. Note this requires the test to be run with `--file` as well.

### `--sarif-file-output=<OUTPUT_FILE_PATH>`

Save test output in SARIF format directly to the `<OUTPUT_FILE_PATH>` file, regardless of whether or not you use the `--sarif` option.

This is especially useful if you want to display the human-readable test output using stdout and at the same time save the SARIF format output to a file.

### `--project-environment=<ENVIRONMENT>[,<ENVIRONMENT>]...>`

Set the project environment to one or more values (comma-separated). To clear the project environment set `--project-environment=`

Allowed values: `frontend`, `backend`, `internal`, `external`, `mobile`, `saas`, `onprem`, `hosted`, `distributed`

For more information see [Project attributes](https://docs.snyk.io/getting-started/introduction-to-snyk-projects/view-project-information/project-attributes)

### `--project-lifecycle=<LIFECYCLE>[,<LIFECYCLE]...>`

Set the project lifecycle to one or more values (comma-separated). To clear the project lifecycle set `--project-lifecycle=`

Allowed values: `production, development, sandbox`

For more information see [Project attributes](https://docs.snyk.io/getting-started/introduction-to-snyk-projects/view-project-information/project-attributes)

### `--project-business-criticality=<BUSINESS_CRITICALITY>[,<BUSINESS_CRITICALITY>]...>`

Set the project business criticality to one or more values (comma-separated). To clear the project business criticality set `--project-business-criticality=`

Allowed values: `critical`, `high`, `medium`, `low`

For more information see [Project attributes](https://docs.snyk.io/getting-started/introduction-to-snyk-projects/view-project-information/project-attributes)

### `--project-tags=<TAG>[,<TAG>]...>`

Set the project tags to one or more values (comma-separated key values pairs with an "=" separator).

Example: `--project-tags=department=finance,team=alpha`

To clear the project tags set `--project-tags=`

### `--tags=<TAG>[,<TAG>]...>`

This is an alias for `--project tags`

### `--severity-threshold=<low|medium|high|critical>`

Report only vulnerabilities at the specified level or higher.

### &#x20;--fail-on=\<all|upgradable>

Fail only when there are vulnerabilities that can be fixed.

* `all`: fail when there is at least one vulnerability that can be either upgraded or patched.
* `upgradable`: fail when there is at least one vulnerability that can be upgraded.

To fail on any vulnerability (the default behavior), do not use the `--fail-on` option. If vulnerabilities do not have a fix and this option is being used, tests pass.

### `--app-vulns`

Allow detection of vulnerabilities in your application dependencies from container images, as well as from the operating system, all in one single scan.

In CLI version 1.962.0 and higher, use the `--app-vulns` option with the the `--json` option to see the operating system as well as application vulnerabilities in JSON format in the results.

For more information see [Detecting application vulnerabilities in container images](https://docs.snyk.io/products/snyk-container/getting-around-the-snyk-container-ui/detecting-application-vulnerabilities-in-container-images)

### `--nested-jars-depth`

When using `--app-vulns` use the `--nested-jars-depth` option to set how many levels of nested jars Snyk is to unpack. Depth must be a number.

### `--exclude-base-image-vulns`

Do not show vulnerabilities introduced only by the base image. Available when using `snyk container test` only.

### `--platform=<PLATFORM>`

For multi-architecture images, specify the platform to test.

Supported platforms are: `linux/amd64`, `linux/arm64`, `linux/riscv64`, `linux/ppc64le`, `linux/s390x`, `linux/386`, `linux/arm/v7`, or `linux/arm/v6`

### `--username=<CONTAINER_REGISTRY_USERNAME>`

Specify a username to use when connecting to a container registry. This is ignored in favor of local Docker binary credentials when Docker is present.

### `--password=<CONTAINER_REGISTRY_PASSWORD>`

Specify a password to use when connecting to a container registry. This is ignored in favor of local Docker binary credentials when Docker is present.

## Examples for the container test command

### Scan and monitor Docker images

`$ snyk container test <image>`

`$ snyk container monitor <image>`

### Option to get more information including base image remediation

`--file=path/to/Dockerfile`

### Scan a Docker image created using the given Dockerfile and with a specified policy path

`$ snyk container test app:latest --file=Dockerfile`

`$ snyk container test app:latest --file=Dockerfile --policy-path=path/to/.snyk`

For more information and examples see [Advanced Snyk Container CLI usage](https://docs.snyk.io/snyk-container/snyk-cli-for-container-security/advanced-snyk-container-cli-usage)
