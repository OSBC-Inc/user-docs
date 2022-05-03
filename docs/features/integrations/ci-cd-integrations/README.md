# Snyk CI/CD 통합

## Snyk을 게이트키퍼로 사용CI/CD 배포 방법

{% hint style="info" %}
이 모든 방법은 동일한 Snyk 엔진에 의존하기 때문에 동일한 결과를 제공합니다. 따라서 선택한 배포 방법에 관계없이 동일한 인수 또는 옵션이 적용됩니다.
{% endhint %}

파이프라인 내에서 Snyk를 구성하는 방법은 다양합니다. 환경 및 기본 설정에 따라 방법을 선택합니다. 모든 방법이 성공적인 실행으로 이어지기를 기대할 수 있습니다.

### Snyk 네이티브 플러그인 사용

Snyk 네이티브 플러그인은 대부분의 일반적인 CI/CD 도구에 사용할 수 있습니다. 이러한 플러그인을 사용하는 것이 가장 쉬운 설정 및 시작 방법입니다. 플러그인에는 사용자 인터페이스(UI)의 가장 일반적인 매개 변수 및 옵션이 포함됩니다.

### **npm method**를 사용하여 Snyk CLI 배포

[CLI를 로컬로 설치](../../snyk-cli/install-the-snyk-cli/)할 때와 유사한 단계를 수행하십시오. 파이프라인 스크립트에서 npm 명령을 실행할 수 있어야 합니다. 이 방법은 CLI 경험과 완전히 일치하므로 문제를 쉽게 해결하고 구성할 수 있다는 장점이 있습니다.

### Snyk CLI 바이너리 버전 배포

바이너리 설치의 장점은 로컬 환경과의 종속성이 없다는 것입니다. 예를 들어 파이프라인에서 npm 명령을 실행할 수 없는 경우에 유용합니다.

CLI 바이너리 파일은 [CLI GitHub repository](https://github.com/snyk/cli/tags)에서 사용할 수 있습니다.

Snyk은 Linux, Windows 및 다른 버전을 가지고 있습니다.

### Snyk 컨테이너 배포

[Dockerhub](https://hub.docker.com/r/snyk/snyk)의 Snyk 이미지 중 하나를 사용하여 파이프라인에 Snyk를 배포할 수 있습니다.

### Snyk CI/CD 통합 예시

[CI/CD examples](https://github.com/snyk-labs/snyk-cicd-integration-examples)는 다양한 CI/CD 도구에 대한 바이너리 및 npm 통합의 몇 가지 예시를 제공합니다.

## 일반적인 채택 단계

개발 팀은 일반적으로 다음과 같은 단계에서 Snyk을 채택합니다.

1. [취약점 노출](./#stage-1-expose-vulnerabilities-snyk-monitor) (`snyk monitor`)
2. [Snyk을 게이트 키퍼로 사용](./#stage-2-use-snyk-as-a-gatekeeper-snyk-test) (`snyk test`)
3. [지속적인 모니터링](./#stage-3-continuous-monitoring-snyk-test-and-snyk-monitor) (`snyk test` and `snyk monitor`)

### **1** 단계**:** 취약점 노출 **(snyk monitor)**

일반적인 접근 방식은 Snyk 결과를 사용하여 개발 프로세스 중에 취약점을 노출하는 것입니다. 이렇게 하면 팀 구성원 간의 취약점에 대한 가시성이 향상됩니다.

파이프라인에서 Snyk를 처음 구현할 때는 snyk monitor 명령만 사용하는 것이 좋습니다. Snyk CI 플러그인 중 하나를 사용하는 경우 빌드에 실패하지 않도록 플러그인을 구성하는 것이 좋습니다.

이는 모든 프로젝트에 취약점이 있으며 Snyk를 빌드에 실패하도록 설정한 후에는 모든 빌드가 Snyk으로 인해 실패하기 때문입니다. 이로 인해 팀이 실패 메시지로 빠르게 처리되는 문제가 발생할 수 있습니다.

`snyk monitor`를 사용하여 결과를 노출하면 프로세스를 중단하지 않고 정보를 제공합니다.

`snyk monitor`에 대한 자세한 내용은 [`monitor` command help](../../../snyk-cli/commands/monitor.md)를 참조하십시오.

### **2** 단계**:** Snyk을 게이트 키퍼로 사용 **(snyk test)**

Snyk을 게이트 키퍼로 사용하면 새로운 취약점(때로는"stopping the bleeding"라고도 함)이 발생하는 것을 방지할 수 있습니다.

팀이 애플리케이션의 취약점을 파악하고 개발 주기 초기에 이를 수정하기 위한 프로세스를 개발하면 Snyk이 빌드에 실패하도록 구성하여 애플리케이션에 취약점이 유입되는 것을 방지할 수 있습니다.

`snyk test`를 빌드에 추가하거나 실패 기능을 활성화하여 Snyk가 빌드에 실패하도록 하여 결과 출력을 콘솔에 제공합니다. 개발자 또는 DevOps 팀은 결과를 사용하여 빌드를 중지할지 아니면 계속할지 결정할 수 있습니다.

`snyk test`에 대한 자세한 내용은 [`test` command help](../../../snyk-cli/commands/test.md)를 참조하십시오.

### **3** 단계**:** 지속적인 모니터링 **(snyk test** and **snyk monitor)**

취약점이 감지될 때 빌드에 실패하도록 Snyk을 구성한 후 지속적인 모니터링을 위해 프로젝트의 성공적인 빌드의 스냅샷을 Snyk으로 보내도록 Snyk을 구성할 수 있습니다.

이렇게 하려면 `snyk test`가 종료 코드를 성공적으로 반환할 경우 `snyk monitor`를 실행하도록 파이프라인을 구성하십시오.

## 기술적 구현

파이프라인에서 실행하도록 Snyk를 구성하려면 Snyk 계정에서 주요 구성 입력을 검색합니다.

### 대상 조직

CI/CD 플랫폼에서 Snyk을 실행하는 경우 일반적으로 검토 및 지속적인 모니터링을 위해 테스트 결과를 Snyk에 게시하려고 합니다.

**대상 조직을 정의하지 않으면** Snyk은 사용하는 인증 토큰에 기본 조직을 사용합니다.

* 사용자 계정의 경우 구성은 사용자가 선호하는 구성입니다(사용자 설정에서 구성 가능).
* 조직 서비스 계정의 경우 계정이 생성된 조직입니다.

`--org` CLI 옵션을 사용하여 URL slug 또는 조직 ID로 Snyk CLI에서 **대상 조직을 정의**할 수 있습니다.

* Snyk UI에서 브라우저의 주소 표시줄에 표시되는 URL slug(orgslugname)를 사용하여 대상 조직을 정의할 수 있습니다.
* 또는 조직의 설정 페이지에서 `ORG_ID`를 사용하여 대상 조직을 정의할 수 있습니다.

![Organization ID](../../../.gitbook/assets/image1.png)

자세한 내용은 [How to select the organization to use in the CLI](https://support.snyk.io/hc/en-us/articles/360000920738-How-to-select-the-organization-to-use-in-the-CLI)을 참조하십시오.

### Snyk 인증 토큰

`snyk test`를 실행하려면 대상 조직에 대한 액세스 권한이 있는 인증 토큰이 필요합니다. 유효한 인증 토큰을 사용할 수 있지만 서비스 계정을 사용하는 것이 좋습니다. 자세한 내용은 [snyk auth commands 도움말](../../snyk-cli/commands/auth.md) 및 [서비스 계정](../managing-integrations/service-accounts.md)을 참조하십시오.

### 설정

Snyk은 빌드 파이프라인에 테스트를 추가하기 위해 다음과 같은 접근 방식을 지원합니다.

* **Snyk 통합 플러그인**: Snyk은 [Jenkins](https://docs.snyk.io/integrations/ci-cd-integrations/jenkins-integration-overview), [Team City](https://docs.snyk.io/integrations/ci-cd-integrations/teamcity-integration-overview)[, Bitbucket Pipelines](https://docs.snyk.io/integrations/ci-cd-integrations/bitbucket-pipelines-integration-overview) 및 [Azure Pipelines](https://docs.snyk.io/integrations/ci-cd-integrations/azure-pipelines-integration)를 포함한 여러 CI 서버에 사전 구축된 플러그인을 제공합니다.
* **Snyk CLI:** 더 복잡한 워크플로우가 존재하거나 Snyk 사전 빌드 플러그인이 없는 빌드 시스템을 사용하는 경우 CI/CD 설정 중 Snyk CLI 도구를 사용할 수 있습니다. 자세한 내용은 [Snyk CLI를 사용하는 설정](./#setting-up-using-snyk-cli)을 참조하십시오.
* **Snyk API**: 복잡한 요구 사항이 있는 경우 Snyk은 REST API를 제공하며, 이 API는 검색, 새 프로젝트 onboarding, 임의 라이브러리 테스트 등의 기능을 사용할 수 있습니다. 자세한 내용은 [Snyk API](../../snyk-api-info/)를 참조하십시오.

### Snyk CLI를 사용하는 설정

Snyk CLI는 대부분의 CI/CD 환경에 쉽게 통합할 수 있도록 개발자가 직접 스크립팅할 수 있는 NodeJS 애플리케이션이며, npm 애플리케이션, 사전 패키지된 바이너리 또는 컨테이너 이미지로 사용할 수 있습니다. 자세한 내용은 [Snyk CLI 설치](../../snyk-cli/install-the-snyk-cli/)를 참조하십시오.

Snyk CLI는 다음과 같이 구성할 수 있습니다.

* 특정 기준이 충족될 때만 0이 아닌 오류 코드를 반환합니다. 예를 들어, 높은 심각도의 취약점이 존재하는 경우에만 오류 코드를 사용하여 종료합니다.
* 유연성을 높이기 위해 모든 데이터를 JSON으로 출력합니다.

### **Exit Codes**

`snyk test`명령은 동기식이며 종료 코드로 끝납니다. 빌드 시스템은 종료 코드를 사용하여 테스트 결과에 따라 빌드를 통과하거나 실패할 수 있습니다. 종료 코드의 의미는 [CLI reference](../../../snyk-cli/cli-reference/)를 참조하십시오.

`snyk monitor` 명령은 프로젝트에 대한 디펜던시 트리의 스냅샷을 Snyk 계정에 게시하고 해당 스냅샷에 취약점이 있는지 모니터링합니다. 취약점 상태를 기준으로 종료 코드로 끝나지 않는 비동기 명령입니다. `snyk monitor`의 경우 종료 코드는 모니터링할 스냅샷을 생성하는 데 성공했는지 여부를 나타냅니다.

빌드 단계에 실패하지 않도록 `snyk test` 명령에 대한 snyk CLI 종료 코드를 무시하려면 명령 끝에 `|| true`를 사용합니다. `|| true`는 스캔의 종료 코드를 0으로 설정합니다. 취약점이 존재하는 경우에도 CI/CD 파이프라인을 계속 사용하는 데 사용할 수 있습니다.

접근 방식과 목표에 따라 파이프라인에서 `snyk monitor` 명령과 `snyk test` 명령을 모두 사용해야 할 수도 있습니다.

### 빌드 파이프라인에서 CLI 예시

`snyk monitor`를 사용하여 취약점을 노출하고 지속적인 모니터링을 위해 snyk UI에 게시합니다.

```
snyk monitor --all-projects --org=snyk-apps
```

심각도가 높은 문제에 대해 `snyk test`를 사용하여 빌드에 실패합니다.

```
snyk test --all-projects --org=snyk-apps --severity-threshold=high
```

CLI의 전체 옵션 목록을 확인하려면 `snyk test --help`, `snyk monitor --help` 및 `snyk container --help` commands 명령을 실행하거나 [help docs](../../../snyk-cli/commands/)를 참조하십시오.

### 빌드 실패에 대한 옵션 구성

`snyk test` 명령에 옵션을 추가하여 빌드에 실패할 수 있는 매개 변수를 세분화할 수 있습니다.

* `--severity-threshold=high`: 높은 심각도 문제에 대해서만 빌드 실패
* `--fail-on=upgradable`: 업그레이드 가능한 문제에 대해서만 빌드를 실패함(Snyk 수정 조언으로 수정할 수 있음)

또한 Snyk JSON 출력의 다른 매개 변수(예: CVSS 점수)에 대한 빌드를 실패하거나, [snyk-filter](https://github.com/snyk-tech-services/snyk-filter)와 같은 래퍼 또는 [snyk-delta](https://github.com/snyk-tech-services/snyk-delta)와 같은 추가 도구를 사용하여 마지막 빌드 이후 발견된 문제에 대해서만 빌드를 실패할 수 있습니다. snyk-filter 및 snyk-delta 사용에 대한 자세한 내용은 [Advanced failing of builds in the Snyk CLI](../../../snyk-cli/test-for-vulnerabilities/advanced-failing-of-builds-in-snyk-cli.md)를 참조하십시오.

### 사용자 정의 빌드 아티팩트 생성

Snyk 명령의 JSON 출력을 사용하여 [snyk-to-html](https://github.com/snyk/snyk-to-html) 유틸리티 또는 사용자가 개발한 기타 사용자 지정 처리를 사용하여 빌드 아티팩트로 사용자 지정 테스트 보고서를 만들 수 있습니다.

### 새 취약성에 대한 작업 항목 생성

Snyk를 사용하면 JIRA에서 새 작업 항목을 자동으로 만들 수 있습니다([Jira integration](https://docs.snyk.io/integrations/untitled-3/jira) 참조). 특정 요구 사항에 맞게 이 코드를 사용자 정의하거나 다른 작업 관리 시스템과 함께 작동하도록 조정할 수 있습니다.

시작하려면 [새로운 취약점에 대한 Jira 티켓](https://github.com/snyk-tech-services/jira-tickets-for-new-vulns)을 참조하거나, [API를 검토하여 Jira 티켓을 생성](https://snyk.docs.apiary.io/#reference/projects/project-jira-issues)하십시오.

### Issues 무시

기본적으로 문제가 무시되지 않거나 [snyk-delta](https://github.com/snyk-tech-services/snyk-delta)를 사용하지 않는 경우 문제가 발견되면 파이프라인의 `snyk test`가 빌드에 실패합니다. 이러한 문제를 해결하지 않고 빌드를 계속할 수 있도록 하려면 다음을 수행할 수 있습니다.

* [Ignore issues using a .snyk policy file](https://docs.snyk.io/snyk-cli/fix-vulnerabilities-from-the-cli/ignore-vulnerabilities-using-snyk-cli)
* [Ignore issues from the Snyk UI](https://support.snyk.io/hc/en-us/articles/360000923498-How-can-I-ignore-a-vulnerability-)
* [Ignore issues from the Snyk API](https://snyk.docs.apiary.io/#reference/projects/project-ignores-by-issue/add-ignore)
* 대량 무시에는 Snyk Python API를 사용합니다. [https://github.com/snyk-labs/pysnyk](https://github.com/snyk-labs/pysnyk) and [https://github.com/snyk-labs/pysnyk/blob/master/examples/api-demo-9c-bulk-ignore-vulns-by-issueIdList.py](https://github.com/snyk-labs/pysnyk/blob/master/examples/api-demo-9c-bulk-ignore-vulns-by-issueIdList.py)를 참조하십시오.

## Snyk 오픈 소스별 전략

이러한 전략은 Snyk SCA ([Software Composition Analysis](https://snyk.io/blog/what-is-software-composition-analysis-sca-and-does-my-company-need-it/)) 테스트 기능을 사용하는 팀에 유용합니다.

### Gradle and Scala

* 다중 프로젝트 구성의 경우 모든 하위 프로젝트를 테스트합니다. `monitor` 또는 `test` 명령어 `--all-sub-projects`와 함께 이 옵션을 사용합니다.
* 특정 구성을 검색하려면 구성 특성의 특정 값을 선택하여 종속성을 해결합니다. 이 옵션은 `test`또는 `monitor` 명령 `--configuration-attributes=`와 함께 사용합니다.

### Python

*   Snyk는 Python을 사용하여 의존성을 검색하고 찾습니다. Snyk은 스캔을 시작하려면 Python 버전이 필요하며, 기본값은 "python"입니다. 여러 Python 버전을 사용하는 경우 `test` 또는 `monitor` 명령과 함께 `--command=`옵션을 사용하여 실행에 올바른 Python 명령을 지정합니다.

    ```
    snyk test --command=python3
    ```
* 매니페스트 파일이 표준 요구 사항이 아니기 때문에 Pip 프로젝트를 검색하고 `--file=` option because your manifest file is not the standard `requirements.txt`, you must use the following option to specify Pip as the package manager `--package-manager=pip.`

### .Net

If you use a `.sln` file, you can specify the path to the file, and Snyk scans all the sub projects that are part of the repo, for example:

```
snyk test --file=sln/.sln
```

### Yarn

For Yarn workspaces use the `--yarn-workspaces` option to test and monitor your packages. The root lockfile will be referenced for scans of all the packages. Use the `--detection-depth` option to find sub-folders that are not auto discovered by default.

{% hint style="info" %}
**Note**\
Yarn workspaces support is for the `snyk test` and `snyk monitor` commands only at this time.
{% endhint %}

Example: scan only the packages that belong to any discovered workspaces in the current directory and 5 sub-directories deep.

```
snyk test --yarn-workspaces --detection-depth=6
```

You can use a common [`.snyk` policy file](../../../snyk-cli/test-for-vulnerabilities/the-.snyk-file.md) if you maintain ignores and patches in one place to be applied for all detected workspaces, by providing the policy path as follows:

```
snyk test --yarn-workspaces --policy-path=src/.snyk
```

### Monorepo

Some customers have complex projects, with multiple languages, package managers, and projects in a single repository. To facilitate this, you can take different approaches:

*   As you build **each project and language**, add a directive to run `snyk test` and target a specific project file, for example:

    ```
    snyk test --file=package.json
    ```

    After you install the dependencies of each project, make a similar call pointing to the specific artifact (such as `pom.xml`). This is fast and efficient, but can be difficult to scale, especially if you are not familiar with the project.
* When you use the `--all-projects` and `--detection-depth` options, the Snyk CLI or CI/CD plugin searches up to the `--detection-depth` in the folder structure for any manifests that match the supported file types. **Each project** is scanned and has its own result. Similarly, if you are using `snyk monitor,` a separate result is created for each project. This provides a good way to automate scanning, especially if you have projects spanning node, .net, python, and so on.
* For most **Gradle projects**, using `--all-projects` works, as it invokes gradle-specific options behind the scenes in the form of: `snyk test --file=build.gradle --all-sub-projects` when it finds the build file as part of the `--all-projects` search.
* **Gradle** may require additional configuration parameters. If so, target the other artifacts using `--file=` for each manifest of the other languages and package managers. You must then use `--all-sub-projects` and potentially `--configuration-matching` to scan a complex Gradle project.

See [Snyk for Java and Kotlin](../../../products/snyk-open-source/language-and-package-manager-support/snyk-for-java-gradle-maven.md) for more information.

## Snyk Container-specific strategies

The best stage to implement Snyk Container in your pipeline is after the container image is built (after running the equivalent of “docker build”), and before your image is either pushed into your registry (“docker push”) or deployed to your running infrastructure (“helm install”, “kubectl apply” and so on).

Typically, the way you run your container build-test-deploy pipeline depends on whether or not a Docker daemon is available to the build agent.

### **Running pipeline if a Docker daemon is available**

If the following circumstances exist:

* You are running your build tooling (such as Jenkins) directly on a host that has Docker natively installed.
* Your pipeline tasks are run inside containers that have the Docker socket \[/var/run/docker.sock] bind-mounted to the host.
* You are running a Docker-inside-Docker setup.

Snyk can help as follows:

* When you run `snyk container test $IMAGE_NAME`, Snyk looks for that image in your local daemon storage, and if the image does not exist, does the equivalent of a **docker pull** to download it from your upstream registry.
* For registry authentication, Snyk uses the credentials you already configured (with something like **docker login**).
* You can specify `--file=Dockerfile` on the command line to link the image vulnerability results with the Dockerfile that built the image, to receive inline fix advice and alternate base image suggestions.

### **Running pipeline if a Docker daemon is not available**

If the following circumstances exist:

* You containerize each build task but do not mount the Docker socket for security and performance reasons.
* Pipeline tasks are split across hosts (or even clusters) and rely on artifacts to be handed off though a central volume or intermediate registry/object store.
* You work exclusively in an ecosystem that only uses OCI-compliant container images.

Snyk can help as follows:

* Run either `snyk container test docker-archive:archive.tar` or `snyk container test oci-archive:archive.tar` to get Snyk vulnerability results against tar-formatted container images (either in Docker or OCI format) without relying on the Docker daemon.
* The tar archive can be generated by your build process using the equivalent of **docker save** and stored in a shared volume or object store. This can be accessed by the build agent container running the Snyk binary, with no other dependencies required.

### Good practice recommendations for integration with container images

* Regardless of how you integrate with container images during CI, run a Snyk Container scan as a separate build step from your Snyk Open Source (application SCA) test. This allows you to isolate build failures to vulnerabilities within either the container/OS layer or the application layer, respectively. This also enables more easily containerized build tasks.
* Use CLI flags like `--fail-on` and `--severity-threshold` to customize the failure status for the build task. For more advanced usage, you can use `--json` to generate a JSON file containing the full vulnerability report, and set your own build failure status based on the JSON data.
* Pass `--exclude-base-image-vulns` to report only vulnerabilities introduced by your user layers, rather than vulnerabilities that come from the base image of the container (the image you specify in the FROM line in the Dockerfile).
* Run `snyk container monitor` following `snyk container test` (or simply check the **Monitor** box on your plugin settings), to keep a record of the bill of materials for this container within the Snyk UI and proactively monitor for new vulnerabilities on a daily basis. This is useful when pushing new releases into production environments. You can use `--project-name` to specify a unique identifier for the release to ensure production containers are tracked separately from others in your build process.

## Snyk IaC-specific strategies

The best way to implement Snyk Infrastructure As Code in your pipeline is as part of the stages, but after the SCA and the Containers stage.

Snyk Infrastructure as Code supports:

* Deployments, Pods, and Services.
* CronJobs, Jobs, StatefulSet, ReplicaSet, DaemonSet, and ReplicationController.

See [Test your Kubernetes files with Snyk CLI](https://docs.snyk.io/snyk-infrastructure-as-code/snyk-cli-for-infrastructure-as-code/test-your-kubernetes-files-with-our-cli-tool) for more details.

## CI/CD troubleshooting and advanced tips

This section provides a few tips to help troubleshoot or scale CI/CD integrations.

### Step 1: Try to replicate with Snyk CLI

If CLI and pipeline are running the same engine, try to clone the project and scan with CLI.

Play with the CLI options. Use the Snyk CLI tool to find and fix known vulnerabilities as you run it in the pipeline. For more information see the [CLI reference](../../../snyk-cli/cli-reference/).

### Step 2: Get logs

If you are able to replicate with CLI and the problem still exists, ask the CLI to output the debug logging using the following command: `DEBUG=*` or use the `-d` option to capture logs:

```
snyk test -d
```

or

```
DEBUG=* snyk test
```

### Step 3: Use the CLI instead of the plugin

Try to replace the native plugin with the CLI by installing the CLI. See [Install the Snyk CLI ](../../../snyk-cli/install-the-snyk-cli/)for instructions.

## Common CLI options in a CI/CD integration

Among the most common options used in a CI/CD integration are the following:

`-- all-projects`: Auto-detect all projects in working directory

`-p`: Prune dependency trees, removing duplicate sub-dependencies. Continues to find all vulnerabilities, but may not find all of the vulnerable paths.

\--org=\<ORG\_ID>: Specify the ORG\_ID to run Snyk commands tied to a specific organization. This influences where new projects are created after running the `monitor` command, some features availability, and private tests limits. If you have multiple organizations, you can set a default from the CLI using:

```
$ snyk config set org=<ORG_ID>
```

Set a default to ensure all newly tested or monitored projects are tested under your default organization. If you need to override the default, use the `--org=<ORG_ID>` option.

Default: `<ORG_ID>` that is the current preferred organization in your [Account settings](https://app.snyk.io/account).

## **Useful resources**

The following repo shares some examples of binary and npm integrations for various CI/CD tools: [GitHub CI/CD examples](https://github.com/snyk-labs/snyk-cicd-integration-examples).

To earn more about CI/CD see [What is CI/CD? CI/CD Pipeline and Tools Explained](https://snyk.io/learn/what-is-ci-cd-pipeline-and-tools-explained/).

## Configure your continuous integration

To continuously avoid known vulnerabilities in your dependencies, integrate Snyk into your continuous integration (build) system. In addition to the documentation here, you're also invited to check out [integration configuration examples](https://github.com/snyk/actions#snyk-github-actions) in the Snyk GitHub repository.

## Set up automatic monitoring

If you monitor a project with Snyk, you’ll be notified if the dependencies in your project are affected by newly disclosed vulnerabilities. To make sure the list of dependencies Snyk has for your project is up to date, refresh it continuously by running Snyk monitor in your deployment process. Configure your environment to include the SNYK\_TOKEN environment variable. You can find your API token on the dashboard after logging in.

## API token configuration

Make sure you do not check your API token into source control, to avoid exposing it to others. Instead, use your CI environment variables to configure it.

See guidance for how to do this on:

* [Travis](https://docs.travis-ci.com/user/environment-variables/)
* [Circle](https://circleci.com/docs/environment-variables/)
* [Codeship](https://codeship.com/documentation/continuous-integration/set-environment-variables/)

You can find others through a [Google search](https://www.google.co.uk/search?q=setting+up+env+variables+in+CI).
