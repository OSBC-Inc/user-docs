# 컨테이너

## 사용법

`snyk container <SUBCOMMAND> [<OPTIONS>] [<IMAGE>]`

## 설명

`snyk container` 명령은 컨테이너 이미지의 취약성을 테스트합니다.

자세한 내용은  [Snyk CLI for container security](https://docs.snyk.io/products/snyk-container/snyk-cli-for-container-security) 참조하십시오.

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

컨테이너 명령에 적용되는 환경 변수가 있습니다. [Configure the Snyk CLI](https://docs.snyk.io/features/snyk-cli/configure-the-snyk-cli) 참조

## 디버그

`-d` 옵션을 사용하여 디버그 로그를 출력합니다.

## 컨테이너 테스트 및 컨테이너 모니터 하위 명령 옵션

### `--print-deps`

분석을 위해 보내기 전에 종속성 트리를 출하십시오.

### `--org=<ORG_ID>`

`<ORG_ID>`를 지정하여 특정 조직에 연결된 Snyk 명령을 실행합니다. `<ORG_ID>`는 일부 기능 가용성 및 개인 테스트 제한에 영향을 미칩니다.

조직이 여러 개인 경우 다음을 사용하여 CLI에서 기본값을 설정할 수 있습니다.

`$ snyk config set org=<ORG_ID>`

새로 테스트되고 모니터링되는 모든 프로젝트가 기본 조직에서 테스트 되고 모니터링 되도록 하려면 기본 값을 설정합니다. 기본 값을 재정의해야 하는 경우 `--org=<ORG_ID>` 옵션을 사용하십시오.

기본값: `<ORG_ID>` 는 사용자의 [Account settings](https://app.snyk.io/account)에서 현재 선호되는 조직입니다.

`--org=<orgslugname>`도 사용할 수 있습니다. `ORG_ID` 는 CLI 와 API 모두 작동합니다. The organization slug name 은 CLI에서는 작동하지만 API에서는 작동하지 않습니다.

자세한 내용은 [How to select the organization to use in the CLI](https://support.snyk.io/hc/en-us/articles/360000920738-How-to-select-the-organization-to-use-in-the-CLI) 참조하십시오.

### `--file=<FILE_PATH>`

자세한 내용을 보려면 이미지에 대한 Docker 파일의 경로를 포함하십시오.

### `--project-name=<PROJECT_NAME>`

사용자 지정 Snyk 프로젝트 이름을 지정하십시오.

### `--policy-path=<PATH_TO_POLICY_FILE>`

경로를 수동으로 `.synk` 정책 파일에 전달합니다.

### `--json`

결과를 JSON 형식으로 출력하여 다른 도구와의 통합에 유용합니다.

Example: `$ snyk container test --json`

### `--json-file-output=<OUTPUT_FILE_PATH>`

`--json` 옵션을 사용하는지 여부에 관계없이 JSON 형식의 테스트 출력을 지정된 파일에 직접 저장합니다.

이 기능은 stdout을 사용하여 사람이 읽을 수 있는 테스트 출력을 표시하고 동시에 JSON 형식 출력을 파일에 저장하려는 경우에 특히 유용합니다.

Example: `$ snyk container test --json-file-output=vuln.json`

### `--sarif`

결과를 SARIF 형식으로 반환합니다. 이렇게 하려면 `--file`로도 테스트를 실행해야 합니다.

### `--sarif-file-output=<OUTPUT_FILE_PATH>`

`--sarif` 옵션 사용 여부에 관계없이 SARIF 형식의 테스트 출력을 직접 `<OUTPUT_FILE_PATH>` 파일에 저장합니다.

이 기능은 stdout을 사용하여 사람이 읽을 수 있는 테스트 출력을 표시하고 동시에 SARIF 형식 출력을 파일에 저장하려는 경우에 특히 유용합니다.

### `--project-environment=<ENVIRONMENT>[,<ENVIRONMENT>]...>`

프로젝트 환경을 하나 이상의 값(쉼표로 구분)으로 설정합니다. 프로젝트 환경 집합을 지우려면 `--project-environment=` 을 설정하십시오.

허용 값: `frontend`, `backend`, `internal`, `external`, `mobile`, `saas`, `onprem`, `hosted`, `distributed`

자세한 내용은 [Project attributes](https://docs.snyk.io/getting-started/introduction-to-snyk-projects/view-project-information/project-attributes) 참조하십시오.

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
