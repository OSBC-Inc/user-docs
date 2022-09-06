# Monitor

## 사용법

`snyk monitor [<OPTIONS>]`

## 설명

`snyk monitor` 명령은 Snyk 계정에 프로젝트를 생성하여 오픈 소스 취약성 및 라이선스 문제를 지속적으로 모니터링합니다. 이 명령을 실행한 후 Snyk 웹사이트에 로그인하고 프로젝트를 확인하여 모니터를 확인합니다.

Snyk 컨테이너는 [`snyk 컨테이너` 도움말](undefined-3.md)을 참조하세요.

`monitor` 명령은 Snyk 코드에 대해 지원되지 않습니다.

Snyk Infrastructure as Code의 경우 Infrastructure as Code용 Snyk CLI에서 "IaC 파일을 정기적으로 테스트" 의 지침을 따르십시오.

## 종료 코드

사용 가능한 종료 코드 및 그 의미:

**0**: 성공, 스냅샷 생성됨\
**2**: 실패, 명령을 다시 실행하십시오.\
**3**: 실패, 지원되는 프로젝트가 감지되지 않음

## Snyk CLI 구성

Snyk API로 연결하기 위해 환경 변수를 사용하고 변수를 설정할 수 있습니다. [Snyk CLI 구성](../snyk-cli.md)을 참조하십시오.

## Debug

`-d` 옵션을 사용하여 디버그 로그를 출력합니다.

## 옵션

마지막으로 지정하는 특정 빌드 환경, 패키지 관리자, 언어 및 `[<CONTEXT-SPECIFIC OPTIONS>]` 옵션에 대한 후속 섹션도 참조하십시오.

### `--all-projects`

작업 디렉토리(Yarn 작업 공간 포함)의 모든 프로젝트를 자동 감지합니다.

자세한 내용은 [Does the Snyk CLI support monorepos or multiple manifest files?](https://support.snyk.io/hc/en-us/articles/360000910577-Does-the-Snyk-CLI-support-monorepos-or-multiple-manifest-files-) 문서를 참조하십시오.

### `--fail-fast`

`--all-projects`와 함께 사용하면 오류가 발생할 때 스캔이 중단되고 이러한 오류를 사용자에게 다시 보고합니다.

종료 코드는 2이고 스캔이 종료됩니다. 오류가 발생하지 않은 프로젝트에 대한 취약점 정보는 보고되지 않습니다.

스캔을 수행하려면 오류를 해결하고 다시 스캔하십시오.

주: `--fail-fast`를 사용하지 않으면 Snyk 모든 프로젝트를 스캔하지만 잘못된 구성이나 다른 오류로 인해 스캔할 수 없는 프로젝트에 대한 취약점은 보고하지 않습니다.

### `--detection-depth=<DEPTH>`

`--all-projects` 또는 `--yarn-workspaces`와 함께 사용하여 검색할 하위 디렉터리 수를 나타냅니다. DEPTH는 `1` 이상의 숫자여야 합니다. 영(0)은 현재 디렉토리입니다.

기본값: 4, 현재 작업 디렉토리(0) 및 4개의 하위 디렉토리.

예: `--detection-depth=3`은 지정된 디렉터리(또는 `<PATH>` 가 지정되지 않은 경우 현재 디렉터리)와 세 가지 수준의 하위 디렉터리로 검색을 제한합니다. 영(0)은 현재 디렉토리입니다.

### `--exclude=<NAME>[,<NAME>]...>`

`--all-projects` 및 `--yarn-workspaces`와 함께 사용하여 제외할 디렉터리 이름 및 파일 이름을 나타낼 수 있습니다. 쉼표로 구분해야 합니다.

예: `$ snyk test --all-projects --exclude=dir1,file2`

이렇게 하면 프로젝트 매니페스트 파일을 검색할 때 "dir1" 및 "file2"라는 이름의 디렉터리 및 파일이 제외됩니다. 예: "./dir1", "./src/dir1", "./file2", "./src/file2" 등.

### `--prune-repeated-subdependencies`, `-p`

종속성 트리를 정리하여 중복 하위 종속성을 제거합니다.

계속해서 모든 취약성을 찾지만 취약한 경로를 모두 찾지 못할 수 있습니다.

### `--print-deps`

분석을 위해 보내기 전에 종속성 트리를 인쇄합니다.

### `--remote-repo-url=<URL>`

모니터링하려는 리포지토리의 원격 URL을 설정하거나 재정의합니다.

### `--dev`

개발 전용 종속성을 포함합니다. 일부 패키지 관리자(예: npm의 `devDependencies` 또는 Gemfile의 :`development` dependencies) 에만 적용할 수 있습니다.

기본값: 프로덕션 종속성만 스캔합니다.

### `--org=<ORG_ID>`

특정 조직에 연결된 Snyk 명령을 실행하려면 `<ORG_ID>`를 지정하십시오. `<ORG_ID>`는 일부 기능 가용성 및 비공개 테스트 제한에 영향을 줍니다.

여러 조직이 있는 경우 다음을 사용하여 CLI에서 기본값을 설정할 수 있습니다:

`$ snyk config set org=<ORG_ID>`

새로 모니터링되는 모든 프로젝트가 기본 조직에서 생성되도록 기본값을 설정합니다. 기본값을 재정의해야 하는 경우 `--org=<ORG_ID>` 옵션을 사용합니다.

기본값: [계정 설정](https://app.snyk.io/login?redirectUri=L2FjY291bnQ%3D\&from=snyk\_auth\_link)에서 현재 선호하는 조직인 `<ORG_ID>`

**Note**: `--org=<orgslugname>`를 사용할 수도 있습니다. `ORG_ID`는 CLI와 API 모두에서 작동합니다. 조직 슬러그 이름은 CLI에서 작동하지만 API에서는 작동하지 않습니다.

자세한 내용은 [How to select the organization to use in the CLI](https://support.snyk.io/hc/en-us/articles/360000920738-How-to-select-the-organization-to-use-in-the-CLI) 문서를 참조하십시오.

### `--file=<FILE>`

패키지 파일을 지정합니다.

로컬에서 테스트하거나 프로젝트를 모니터링할 때 Snyk이 패키지 정보를 검사해야 하는 파일을 지정할 수 있습니다. 파일이 지정되지 않은 경우 Snyk은 프로젝트에 적합한 파일을 감지하려고 시도합니다.

### `--package-manager=<PACKAGE_MANAGER_NAME>`

`--file=<FILE>` 옵션으로 지정한 파일 이름이 표준이 아닌 경우 패키지 관리자의 이름을 지정합니다. 이렇게 하면 Snyk이 파일을 찾을 수 있습니다.

예: `$ snyk monitor --file=req.txt --package-manager=pip`

### `--unmanaged`

C++의 경우에만 모든 파일에서 알려진 오픈 소스 종속성을 검색합니다.

`--unmanaged`와 함께 사용할 수 있는 옵션은 [`--unmanaged`를 사용한 검사 옵션](monitor.md#options-for-scanning-using-unmanaged)을 참조하세요.

자세한 내용은 [C/C++용 Snyk](../../../snyk-products/snyk-open-source/language-and-package-manager-support/snyk-for-c-c++.md)를 참조하세요.

### `--ignore-policy`

설정된 모든 정책, `.snyk` 파일의 현재 정책, 조직 수준 무시 및 snyk.io의 프로젝트 정책을 무시합니다.

### `--trust-policies`

종속성 Snyk 정책의 무시 규칙을 적용하고 사용합니다. 그렇지 않으면 종속성의 무시 규칙은 제안으로만 표시됩니다.

### `--project-name=<PROJECT_NAME>`

사용자 정의 Snyk 프로젝트 이름을 지정하십시오.

예: `$ snyk monitor --project-name=my-project`

### `--target-reference=<TARGET_REFERENCE>`

이 프로젝트를 구별하는 참조를 지정하십시오(예: 분기 이름 또는 버전). 참조가 동일한 프로젝트는 해당 참조를 기반으로 그룹화할 수 있습니다. Snyk 오픈 소스에 대해 지원되며 `--unmanaged`와 함께 사용합니다.

자세한 내용은 [분기 또는 버전별로 프로젝트 분리](../secure-your-projects-in-the-long-term/separating-projects-by-branch-or-version.md)를 참조하세요.

### `--policy-path=<PATH_TO_POLICY_FILE>`

`.snyk` 정책 파일에 대한 경로를 수동으로 전달합니다.

### `--json`

결과를 JSON 형식으로 인쇄합니다.

### `--project-environment=<ENVIRONMENT>[,<ENVIRONMENT>]...>`

프로젝트 환경 프로젝트 속성을 하나 이상의 값(쉼표로 구분)으로 설정하십시오. 프로젝트 환경을 지우려면 `--project-environment=` 로 설정합니다.

허용되는 값: `frontend, backend, internal, external, mobile, saas, onprem, hosted, distributed`

자세한 내용은  [프로젝트 속성](../../../getting-started/introduction-to-snyk-projects/view-project-information/project-attributes.md)을 참조하세요.

### `--project-lifecycle=<LIFECYCLE>[,<LIFECYCLE>]...>`

프로젝트 수명 주기 프로젝트 속성을 하나 이상의 값(쉼표로 구분)으로 설정합니다. 프로젝트 수명 주기를 지우려면 `--project-lifecycle=` 로 설정합니다.

허용되는 값: `production, development, sandbox`

자세한 내용은  [프로젝트 속성](../../../getting-started/introduction-to-snyk-projects/view-project-information/project-attributes.md)을 참조하세요.

### `--project-business-criticality=<BUSINESS_CRITICALITY>[,<BUSINESS_CRITICALITY>]...>`

프로젝트의 비즈니스 중요도 프로젝트 속성을 하나 이상의 값(쉼표로 구분)으로 설정하십시오. 프로젝트 비즈니스 중요도 설정을 지우려면 `--project-business-criticality=` 로 설정합니다.

허용되는 값: `critical, high, medium, low`

자세한 내용은  [프로젝트 속성](../../../getting-started/introduction-to-snyk-projects/view-project-information/project-attributes.md)을 참조하세요.

### `--project-tags=<TAG>[,<TAG>]...>`

프로젝트 태그를 하나 이상의 값("=" 구분 기호가 있는 쉼표로 구분된 키 값 쌍)으로 설정합니다(예: `--project-tags=department=finance,team=alpha`). 프로젝트 태그를 지우려면 `--project-tags=`로 설정합니다.

### `--tags=<TAG>[,<TAG>]...>`

이것은 `--project-tags`의 별칭입니다.

## Maven 프로젝트를 위한 옵션

Maven CLI 옵션에 대한 자세한 내용은 [Java 및 Kotlin용 Snyk](../../../snyk-products/snyk-open-source/language-and-package-manager-support/snyk-for-java-gradle-maven.md)을 참조하세요.

### `--maven-aggregate-project`

Maven 집계 프로젝트, 즉 모듈 및 상속을 사용하는 프로젝트를 스캔할 때 `--all-projects` 대신 `--maven-aggregate-project`를 사용합니다.

이러한 유형의 프로젝트를 스캔할 때 Snyk는 컴파일을 수행하여 Maven 리액터에서 모든 모듈을 확인할 수 있는지 확인합니다.

루트 pom.xml 파일과 동일한 디렉토리에서 스캔을 실행해야 합니다.

Snyk은 pom.xml 파일별로 테스트 결과를 보고합니다.

### `--scan-all-unmanaged`

지정된 디렉토리에서 maven jar, aars 및 wars를 자동 감지합니다. 개별적으로 모니터링하려면 `--file=<JAR_FILE_NAME>`을 사용하십시오.

**주의**: 사용자 정의 빌드된 jar 파일은 오픈 소스 종속성이 있더라도 범위를 벗어납니다.

## Gradle 프로젝트를 위한 옵션

Gradle CLI 옵션에 대한 자세한 내용은 [Java 및 Kotlin용 Snyk](../../../snyk-products/snyk-open-source/language-and-package-manager-support/snyk-for-java-gradle-maven.md)을 참조하세요.

### `--sub-project=<NAME>`, `--gradle-sub-project=<NAME>`

Gradle "다중 프로젝트" 구성의 경우 특정 하위 프로젝트를 모니터링합니다.

### `--all-sub-projects`

"다중 프로젝트" 구성의 경우 모든 하위 프로젝트를 모니터링합니다.

### `--configuration-matching=<CONFIGURATION_REGEX>`

지정된 Java 정규식과 일치하는 구성만 사용하여 종속성을 해결합니다.

예: `^releaseRuntimeClasspath$`

### `--configuration-attributes=<ATTRIBUTE>[,<ATTRIBUTE>]...`

종속성을 설치하고 종속성 해결을 수행하려면 구성 속성의 특정 값을 선택하십시오.

예: `buildtype:release,usage:java-runtime`

### `--init-script=<FILE`

Gradle 초기화 스크립트가 포함된 프로젝트에 사용합니다.

## NuGet 프로젝트에 대한 옵션

### `--assets-project-name`

NuGet `PackageReference`를 사용하여 .NET 프로젝트를 모니터링할 때 `project.assets.json`이 있는 경우 프로젝트 이름을 사용합니다.

### `--packages-folder`

패키지 폴더에 대한 사용자 정의 경로를 지정하십시오.

### `--project-name-prefix=<PREFIX_STRING>`

.NET 프로젝트를 모니터링할 때 이 옵션을 사용하여 원하는 구분 기호와 함께 프로젝트 내부의 파일 이름에 사용자 지정 접두사를 추가합니다.

예: `snyk monitor --file=my-project.sln --project-name-prefix=my-group/`

이는 다른 `.sln` 파일에 동일한 이름을 가진 여러 프로젝트가 있는 경우에 유용합니다.

## npm 프로젝트를 위한 옵션

### `--strict-out-of-sync=true|false`

동기화되지 않은 잠금 파일 모니터링을 제어합니다.

기본값: true

## Yarn 프로젝트에 대한 옵션

### `--strict-out-of-sync=true|false`

동기화되지 않은 잠금 파일 모니터링을 제어합니다.

기본값: true

### `--yarn-workspaces`

Yarn 작업 공간을 감지하고 스캔합니다. `--detection-depth`를 사용하여 검색할 하위 디렉터리 수를 지정하고 `--exclude`를 사용하여 디렉터리와 파일을 제외할 수 있습니다. 또는 `--all-projects`를 사용하여 다른 프로젝트와 함께 Yarn 작업 공간을 스캔합니다.

## CocoaPods 프로젝트를 위한 옵션

### `--strict-out-of-sync=true|false`

동기화되지 않은 잠금 파일 모니터링을 제어합니다.

기본값: false

## Python 프로젝트를 위한 옵션

### `--command=<COMMAND>`

Python 버전에 따라 사용할 특정 Python 명령을를 지정합니다. 기본값은 기본 파이썬 버전을 실행하는 파이썬입니다. 'python -V'를 실행하여 버전을 확인합니다. 여러 Python 버전을 사용하는 경우 이 매개변수를 사용하여 실행할 올바른 Python 명령을 지정하십시오.

기본값: `python` 예: `--command=python3`

### `--skip-unresolved=true|false`

환경에서 찾을 수 없는 패키지 건너뛰기를 허용합니다.

## `--unmanaged`를 사용한 스캔 옵션

다음 snyk 모니터 옵션은 이 도움말에 설명된 대로 `--unmanaged`와 함께 사용할 수 있습니다.

`--org=<ORG_ID>`

`--json`

`--remote-repo-url=<URL>`

`--target-reference=<TARGET_REFERENCE>`

특별한 옵션도 있습니다.

### `--target-dir`

현재 디렉토리 대신 인수에 지정된 경로를 스캔하십시오.

또는 `snyk test --unmanaged`를 실행합니다.

### `--max-depth`

아카이브 추출의 최대 레벨을 지정하십시오.

사용법: `--max-depth=1`&#x20;

아카이브 추출을 완전히 비활성화하려면 0을 사용하십시오.

### `--print-dep-paths`

종속성을 표시합니다.

식별된 각 종속성에 기여한 파일을 보려면 이 옵션을 사용하십시오.

Snyk이 식별된 종속성과 해당 버전에 대해 얼마나 확신하는지 확인하려면 `--print-deps` 또는 `--print-dep-paths` 옵션을 사용하십시오.

C/C++ 프로젝트용 CLI 옵션 사용에 대한 자세한 내용은 [C/C++용 Snyk](../../../snyk-products/snyk-open-source/language-and-package-manager-support/snyk-for-c-c++.md)를 참조하십시오.

### `--project-name=c-project`

snyk monitor `--unmanaged` 명령과 함께 사용하여 Snyk가 원하는 이름을 입력하여 스냅샷에 제공하는 기본 이름을 재정의합니다.

## 빌드 도구 옵션

### `-- [<CONTEXT-SPECIFIC_OPTIONS>]`

전체 Snyk 명령 뒤에 이중 대시(`--`)를 사용하여 빌드 도구(예: Gradle 또는 Maven)에 직접 이어지는 옵션(인수, 플래그)을 전달합니다.

형식은 `snyk <command> -- [<context-specific_options>]`

예: `snyk monitor -- --build-cache`
