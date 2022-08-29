# 컨테이너

## 사용법

`snyk container <SUBCOMMAND> [<OPTIONS>] [<IMAGE>]`

## 설명

`snyk container` 명령은 컨테이너 이미지의 취약성을 테스트합니다.

자세한 내용은  [컨테이너 보안을 위한 Snyk CLI](../../../snyk-products/snyk-container/snyk-cli-for-container-security/) 참조하십시오.

## 하위 명령

### `test`

알려진 취약성을 테스트합니다.

### `monitor`

컨테이너 이미지 레이어 및 종속성을 캡처하고 [snyk.io](https://snyk.io) 에 대한 취약점을 모니터링 합니다.&#x20;

## 종료 코드

가능한 종료 코드와 그 의미는 다음과 같습니다.

**0**: 성공, 취약점 없음\
**1**: 작업 필요, 취약성 발견\
**2**: 실패, 명령 재실행 시도\
**3**: 실패, 지원되는 프로젝트가 검색되지 않음

## Snyk CLI 구성

환경 변수를 사용하여 Snyk CLI를 구성하고 Snyk API로 연결하기 위한 변수를 설정할 수 있습니다.

컨테이너 명령에 적용되는 환경 변수가 있습니다. [Snyk CLI 구성](../snyk-cli.md) 참조

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

자세한 내용은 [How to select the organization to use in the CLI](https://support.snyk.io/hc/en-us/articles/360000920738-How-to-select-the-organization-to-use-in-the-CLI)를 참조하십시오.

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

자세한 내용은 [Project attributes](https://docs.snyk.io/getting-started/introduction-to-snyk-projects/view-project-information/project-attributes)를 참조하십시오.

### `--project-lifecycle=<LIFECYCLE>[,<LIFECYCLE]...>`

프로젝트 수명 주기를 하나 이상의 값(쉼표로 구분)으로 설정합니다. 프로젝트 수명 주기 집합을 지우려면 `--project-lifecycle=` 을 설정하십시오.

허용 값: `production, development, sandbox`

자세한 내용은 [Project attributes](https://docs.snyk.io/getting-started/introduction-to-snyk-projects/view-project-information/project-attributes) 를 참조하십시오.

### `--project-business-criticality=<BUSINESS_CRITICALITY>[,<BUSINESS_CRITICALITY>]...>`

프로젝트 비즈니스 중요도를 하나 이상의 값(쉼표로 구분)으로 설정합니다. 프로젝트 비즈니스 중요도 집합을 지우려면 `--project-business-criticality=` 을 설정하십시오.

허용 값: `critical`, `high`, `medium`, `low`

자세한 내용은 [Project attributes](https://docs.snyk.io/getting-started/introduction-to-snyk-projects/view-project-information/project-attributes)를 참조하십시오.

### `--project-tags=<TAG>[,<TAG>]...>`

프로젝트 태그를 하나 이상의 값으로 설정합니다("=" 구분 기호가 있는 쉼표로 구분된 키-값 쌍).

Example: `--project-tags=department=finance,team=alpha`

project tags set 를 지우려면 `--project-tags=` 를 수정하십시오.

### `--tags=<TAG>[,<TAG>]...>`

이건 `--project tags` 에 대한 별칭입니다.

### `--severity-threshold=<low|medium|high|critical>`

지정된 수준 이상의 취약성만 보고합니다.

### &#x20;--fail-on=\<all|upgradable>

수정할 수 있는 취약성이 있는 경우에만 실패합니다.

* `all`: 업그레이드하거나 패치를 적용할 수 있는 취약성이 하나 이상 있는 경우 실패합니다.
* `upgradable`: 업그레이드할 수 있는 취약성이 하나 이상 있는 경우 실패합니다.

취약점(기본 동작)에서 실패하려면 `--fail-on` 옵션을 사용하지 마십시오. 취약성에 수정 사항이 없고 이 옵션을 사용하는 경우 테스트가 통과됩니다.

### `--app-vulns`

컨테이너 이미지 뿐만 아니라 운영 체제에서도 애플리케이션 종속성의 취약성을 한 번의 검색으로 모두 탐지할 수 있습니다.

CLI 버전 1.962.0 이상에서는 `--app-vuls` 옵션과 `--json` 옵션을 함께 사용하여 운영 체제와 JSON 형식의 응용 프로그램 취약성을 결과에서 확인합니다.

자세한 내용은 [컨테이너 이미지에서 애플리케이션 취약점 탐지](../../../snyk-products/snyk-container/getting-around-the-snyk-container-ui/detecting-application-vulnerabilities-in-container-images.md)를 참조하세요.

### `--nested-jars-depth`

`--app-vulns`를 사용하는 경우 u`-nested-jars-depth` 옵션을 사용하여 Snyk이 풀 중첩된 jars의 수준을 설정합니다. 깊이는 숫자여야 합니다.

### `--exclude-base-image-vulns`

기본 이미지에 의해 도입된 취약점만 표시하지 않습니다. `snyk container test`를 사용할 때만 표할 수 있습니다.

### `--platform=<PLATFORM>`

다중 아키텍처 이미지의 경우 테스트할 플랫폼을 지정합니다.

지원되는 플랫폼: `linux/amd64`, `linux/arm64`, `linux/riscv64`, `linux/ppc64le`, `linux/s390x`, `linux/386`, `linux/arm/v7`, or `linux/arm/v6`

### `--username=<CONTAINER_REGISTRY_USERNAME>`

컨테이너 레지스트리에 연결할 때 사용할 사용자 이름을 지정합니다. 이는 Docker가 있을 때 로컬 Docker 이진 자격 증명을 위해 무시됩니다.

### `--password=<CONTAINER_REGISTRY_PASSWORD>`

컨테이너 레지스트리에 연결할 때 사용할 암호를 지정하십시오. 이는 Docker가 있을 때 로컬 Docker 이진 자격 증명을 위해 무시됩니다.

## 컨테이너 테스트 명령의 예

### Docker 이미지 스캔 및 모니터링

`$ snyk container test <image>`

`$ snyk container monitor <image>`

### 기본 이미지 수정을 포함한 추가 정보를 얻는 옵션

`--file=path/to/Dockerfile`

### 지정된 정책 경로를 사용하여 지정된 Docker 파일을 사용하여 생성된 Docker 이미지 검색

`$ snyk container test app:latest --file=Dockerfile`

`$ snyk container test app:latest --file=Dockerfile --policy-path=path/to/.snyk`

자세한 내용과 예시는 [고급 Snyk Container CLI 사용](../../../snyk-products/snyk-container/snyk-cli-for-container-security/advanced-snyk-container-cli-usage.md)을 참조하십시오.
