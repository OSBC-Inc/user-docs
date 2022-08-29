# Monitor

## 사용법

`snyk monitor [<OPTIONS>]`

## 설명

`snyk monitor` command는 Snyk 계정에 프로젝트를 생성하여 오픈 소스 취약성 및 라이선스 문제를 지속적으로 모니터링합니다. 이 명령을 실행한 후 Snyk 웹사이트에 로그인하고 프로젝트를 확인하여 모니터를 확인합니다.

Snyk 컨테이너는 [`snyk 컨테이너` 도움말](undefined-3.md)을 참조하세요.

`monitor` command는 Snyk 코드에 대해 지원되지 않습니다.

Snyk Infrastructure as Code의 경우 Infrastructure as Code용 Snyk CLI에서 "IaC 파일을 정기적으로 테스트" 의 지침을 따르십시오.

## 종료 코드

사용 가능한 종료 코드 및 그 의미:

**0**: 성공, 스냅샷 생성됨\
**2**: 실패, 명령을 다시 실행하십시오.\
**3**: 실패, 지원되는 프로젝트가 감지되지 않음

## Snyk CLI 구성

Snyk API로 연결하기 위해 환경 변수를 사용하고 변수를 설정할 수 있습니다. [Snyk CLI 구성을](../snyk-cli.md) 참조하십시오.

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

Include development-only dependencies. Applicable only for some package managers, for example, `devDependencies` in npm or `:development` dependencies in Gemfile.

Default: scan only production dependencies.

### `--org=<ORG_ID>`

Specify the `<ORG_ID>` to run Snyk commands tied to a specific organization. The `<ORG_ID>` influences some features availability and private test limits.

If you have multiple organizations, you can set a default from the CLI using:

`$ snyk config set org=<ORG_`ID`>`

Set a default to ensure all newly monitored projects are created under your default organization. If you need to override the default, use the `--org=<ORG_ID>` option.

Default: `<ORG_ID>` that is the current preferred organization in your [Account settings](https://app.snyk.io/account)

Note that you can also use `--org=<orgslugname>`. The `ORG_ID` works in both the CLI and the API. The organization slug name works in the CLI, but not in the API.

For more information see the article [How to select the organization to use in the CLI](https://support.snyk.io/hc/en-us/articles/360000920738-How-to-select-the-organization-to-use-in-the-CLI)

### `--file=<FILE>`

Specify a package file.

When testing locally or monitoring a project, you can specify the file that Snyk should inspect for package information. When the file is not specified, Snyk tries to detect the appropriate file for your project.

### `--package-manager=<PACKAGE_MANAGER_NAME>`

Specify the name of the package manager when the filename specified with the `--file=<FILE>` option is not standard. This allows Snyk to find the file.

Example: `$ snyk monitor --file=req.txt --package-manager=pip`

### `--unmanaged`

For C++ only, scan all files for known open source dependencies.

For options you can use with `--unmanaged` see [Options for scanning using `--unmanaged`](https://docs.snyk.io/snyk-cli/commands/monitor#options-for-scanning-using-unmanaged)

For more information see [Snyk for C/C++](https://docs.snyk.io/products/snyk-open-source/language-and-package-manager-support/snyk-for-c-c++)\`\`

### `--ignore-policy`

Ignore all set policies, the current policy in the `.snyk` file, org level ignores, and the project policy on snyk.io.

### `--trust-policies`

Apply and use ignore rules from the Snyk policies your dependencies; otherwise ignore rules in the dependencies are only shown as a suggestion.

### `--project-name=<PROJECT_NAME>`

Specify a custom Snyk project name.

Example: `$ snyk monitor --project-name=my-project`

### `--target-reference=<TARGET_REFERENCE>`

Specify a reference which differentiates this project, for example, a branch name or version. Projects having the same reference can be grouped based on that reference. Supported for Snyk Open Source and use with `--unmanaged`.

For more information see [Separating projects by branch or version](https://docs.snyk.io/snyk-cli/secure-your-projects-in-the-long-term/grouping-projects-by-branch-or-version)

### `--policy-path=<PATH_TO_POLICY_FILE>`

Manually pass a path to a `.snyk` policy file.

### `--json`

Print results in JSON format.

### `--project-environment=<ENVIRONMENT>[,<ENVIRONMENT>]...>`

Set the project environment project attribute to one or more values (comma-separated). To clear the project environment set `--project-environment=`

Allowed values: `frontend, backend, internal, external, mobile, saas, onprem, hosted, distributed`

For more information see [Project attributes](https://docs.snyk.io/getting-started/introduction-to-snyk-projects/view-project-information/project-attributes)

### `--project-lifecycle=<LIFECYCLE>[,<LIFECYCLE>]...>`

Set the project lifecycle project attribute to one or more values (comma-separated). To clear the project lifecycle set `--project-lifecycle=`

Allowed values: `production, development, sandbox`

For more information see [Project attributes](https://docs.snyk.io/getting-started/introduction-to-snyk-projects/view-project-information/project-attributes)

### `--project-business-criticality=<BUSINESS_CRITICALITY>[,<BUSINESS_CRITICALITY>]...>`

Set the project business criticality project attribute to one or more values (comma-separated). To clear the project business criticality set `--project-business-criticality=`

Allowed values: `critical, high, medium, low`

For more information see [Project attributes](https://docs.snyk.io/getting-started/introduction-to-snyk-projects/view-project-information/project-attributes)

### `--project-tags=<TAG>[,<TAG>]...>`

Set the project tags to one or more values (comma-separated key value pairs with an "=" separator), for example, `--project-tags=department=finance,team=alpha` To clear the project tags set `--project-tags=`

### `--tags=<TAG>[,<TAG>]...>`

This is an alias for `--project-tags`

## Options for Maven projects

For more information about Maven CLI options see [Snyk for Java and Kotlin](https://docs.snyk.io/products/snyk-open-source/language-and-package-manager-support/snyk-for-java-gradle-maven)

### `--maven-aggregate-project`

Use `--maven-aggregate-project` instead of `--all-projects` when scanning Maven aggregate projects, that is, ones that use modules and inheritance.

When scanning these types of projects, Snyk performs a compile to ensure all modules are resolvable by the Maven reactor.&#x20;

Be sure to run the scan in the same directory as the root pom.xml file.&#x20;

Snyk reports test results per pom.xml file.

### `--scan-all-unmanaged`

Auto-detect maven jars, aars, and wars in given directory. To monitor individually use `--file=<JAR_FILE_NAME>`

**Note**: Custom-built jar files, even with open source dependencies, are out of scope.

## Options for Gradle projects

For more information about Gradle CLI options see [Snyk for Java and Kotlin](https://docs.snyk.io/products/snyk-open-source/language-and-package-manager-support/snyk-for-java-gradle-maven)

### `--sub-project=<NAME>`, `--gradle-sub-project=<NAME>`

For Gradle "multi project" configurations, monitor a specific sub-project.

### `--all-sub-projects`

For "multi project" configurations, monitor all sub-projects.

### `--configuration-matching=<CONFIGURATION_REGEX>`

Resolve dependencies using only configuration(s) that match the specified Java regular expression.

Example: `^releaseRuntimeClasspath$`

### `--configuration-attributes=<ATTRIBUTE>[,<ATTRIBUTE>]...`

Select certain values of configuration attributes to install dependencies and perform dependency resolution.

Example: `buildtype:release,usage:java-runtime`

### `--init-script=<FILE`

Use for projects that contain a Gradle initialization script.

## Options for NuGet projects

### `--assets-project-name`

When monitoring a .NET project using NuGet `PackageReference` use the project name in `project.assets.json`, if found.

### `--packages-folder`

Specify a custom path to the packages folder.

### `--project-name-prefix=<PREFIX_STRING>`

When monitoring a .NET project, use this option to add a custom prefix to the name of files inside a project along with any desired separators.

Example: `snyk monitor --file=my-project.sln --project-name-prefix=my-group/`

This is useful when you have multiple projects with the same name in other `.sln` files.

## Option for npm projects

### `--strict-out-of-sync=true|false`

Control monitoring out-of-sync lockfiles.

Default: true

## Options for Yarn projects

### `--strict-out-of-sync=true|false`

Control monitoring out-of-sync lockfiles.

Default: true

### `--yarn-workspaces`

Detect and scan Yarn workspaces. You can specify how many sub-directories to search using `--detection-depth` and exclude directories and files using `--exclude`. Alternatively scan Yarn workspaces with other projects using `--all-projects`

## Option for CocoaPods projects

### `--strict-out-of-sync=true|false`

Control monitoring out-of-sync lockfiles.

Default: false

## Options for Python projects

### `--command=<COMMAND>`

Indicate which specific Python commands to use based on Python version. The default is `python` which executes your default python version. Run 'python -V' to find out what version it is. If you are using multiple Python versions, use this parameter to specify the correct Python command for execution.

Default: `python` Example: `--command=python3`

### `--skip-unresolved=true|false`

Allow skipping packages that are not found in the environment.

## Options for scanning using `--unmanaged`

The following `snyk monitor` options can be used with `--unmanaged` as documented in this help.

`--org=<ORG_ID>`

`--json`

`--remote-repo-url=<URL>`

`--target-reference=<TARGET_REFERENCE>`

There are also special options.

### `--target-dir`

Scan the path specified in the argument instead of the current directory.

Alternatively, run `snyk test --unmanaged`

### `--max-depth`

Specify the maximum level of archive extraction.

Usage: `--max-depth=1`&#x20;

Use 0 to disable archive extraction completely.

### `--print-dep-paths`

Display dependencies.

Use use this option to see what files contributed to each dependency identified.

To see how confident Snyk is about the identified dependency and its version, use the `--print-deps` or `--print-dep-paths` option.

For more information on uses of CLI options for C/C++ projects see [Snyk for C / C++](https://docs.snyk.io/products/snyk-open-source/language-and-package-manager-support/snyk-for-c-c++)

### `--project-name=c-project`

Use with the `snyk monitor --unmanaged` command to override the default name Snyk gives your snapshots by entering the desired name.

## Options for build tools

### `-- [<CONTEXT-SPECIFIC_OPTIONS>]`

Use a double dash (`--`) after the complete Snyk command to pass options (arguments, flags) that follow directly to the build tool, for example Gradle or Maven.

The format is `snyk <command> -- [<context-specific_options>]`

Example: `snyk monitor -- --build-cache`
