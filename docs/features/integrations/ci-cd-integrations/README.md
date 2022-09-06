# Snyk CI/CD 통합

## Snyk을 게이트키퍼로 사용CI/CD 배포 방법

{% hint style="info" %}
이 모든 방법은 동일한 Snyk 엔진에 의존하기 때문에 동일한 결과를 제공합니다. 따라서 선택한 배포 방법에 관계없이 동일한 인수 또는 옵션이 적용됩니다.
{% endhint %}

파이프라인 내에서 Snyk를 구성하는 방법은 다양합니다. 환경 및 기본 설정에 따라 방법을 선택합니다. 모든 방법이 성공적인 실행으로 이어지기를 기대할 수 있습니다.

### Snyk 네이티브 플러그인 사용

Snyk 네이티브 플러그인은 대부분의 일반적인 CI/CD 도구에 사용할 수 있습니다. 이러한 플러그인을 사용하는 것이 가장 쉬운 설정 및 시작 방법입니다. 플러그인에는 사용자 인터페이스(UI)의 가장 일반적인 매개 변수 및 옵션이 포함됩니다.

### **npm method**를 사용하여 Snyk CLI 배포

[CLI를 로컬로 설치](../../snyk-cli/install-or-update-the-snyk-cli.md#npm-yarn-snyk-cli)할 때와 유사한 단계를 수행하십시오. 파이프라인 스크립트에서 npm 명령을 실행할 수 있어야 합니다. 이 방법은 CLI 경험과 완전히 일치하므로 문제를 쉽게 해결하고 구성할 수 있다는 장점이 있습니다.

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

1. [취약점 노출](./#1-snyk-monitor) (`snyk monitor`)
2. [Snyk을 게이트 키퍼로 사용](./#2-snyk-snyk-test) (`snyk test`)
3. [지속적인 모니터링](./#3-snyk-test-and-snyk-monitor) (`snyk test` and `snyk monitor`)

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

### **3** 단계**:** 지속적인 모니터링 **(snyk test** 및 **snyk monitor)**

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

![조직 ID](../../../.gitbook/assets/image1.png)

자세한 내용은 [How to select the organization to use in the CLI](https://support.snyk.io/hc/en-us/articles/360000920738-How-to-select-the-organization-to-use-in-the-CLI)을 참조하십시오.

### Snyk 인증 토큰

`snyk test`를 실행하려면 대상 조직에 대한 액세스 권한이 있는 인증 토큰이 필요합니다. 유효한 인증 토큰을 사용할 수 있지만 서비스 계정을 사용하는 것이 좋습니다. 자세한 내용은 [snyk auth commands 도움말](../../snyk-cli/cli-command/undefined.md) 및 [서비스 계정](../managing-integrations/service-accounts.md)을 참조하십시오.

### 설정

Snyk은 빌드 파이프라인에 테스트를 추가하기 위해 다음과 같은 접근 방식을 지원합니다.

* **Snyk 통합 플러그인**: Snyk은 [Jenkins](jenkins-integration-overview.md), [Team City](teamcity-integration-overview/), [Bitbucket Pipelines](bitbucket-pipelines-integration-overview.md) 및 Azure Pipelines를 포함한 여러 CI 서버에 사전 구축된 플러그인을 제공합니다.
* **Snyk CLI:** 더 복잡한 워크플로우가 존재하거나 Snyk 사전 빌드 플러그인이 없는 빌드 시스템을 사용하는 경우 CI/CD 설정 중 Snyk CLI 도구를 사용할 수 있습니다. 자세한 내용은 [Snyk CLI를 사용하는 설정](./#snyk-cli-1)을 참조하십시오.
* **Snyk API**: 복잡한 요구 사항이 있는 경우 Snyk은 REST API를 제공하며, 이 API는 검색, 새 프로젝트 onboarding, 임의 라이브러리 테스트 등의 기능을 사용할 수 있습니다. 자세한 내용은 [Snyk API](../../snyk-api-info/)를 참조하십시오.

### Snyk CLI를 사용하는 설정

Snyk CLI는 대부분의 CI/CD 환경에 쉽게 통합할 수 있도록 개발자가 직접 스크립팅할 수 있는 NodeJS 애플리케이션이며, npm 애플리케이션, 사전 패키지된 바이너리 또는 컨테이너 이미지로 사용할 수 있습니다. 자세한 내용은 [Snyk CLI 설치](../../snyk-cli/install-or-update-the-snyk-cli.md)를 참조하십시오.

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

Snyk를 사용하면 JIRA에서 새 작업 항목을 자동으로 만들 수 있습니다([Jira integration](../notifications-ticketing-system-integrations/jira.md) 참조). 특정 요구 사항에 맞게 이 코드를 사용자 정의하거나 다른 작업 관리 시스템과 함께 작동하도록 조정할 수 있습니다.

시작하려면 [새로운 취약점에 대한 Jira 티켓](https://github.com/snyk-tech-services/jira-tickets-for-new-vulns)을 참조하거나, [API를 검토하여 Jira 티켓을 생성](https://snyk.docs.apiary.io/#reference/projects/project-jira-issues)하십시오.

### Issues 무시

기본적으로 문제가 무시되지 않거나 [snyk-delta](https://github.com/snyk-tech-services/snyk-delta)를 사용하지 않는 경우 문제가 발견되면 파이프라인의 `snyk test`가 빌드에 실패합니다. 이러한 문제를 해결하지 않고 빌드를 계속할 수 있도록 하려면 다음을 수행할 수 있습니다.

* [`.snyk` 정책 파일을 사용하여 문제 무시](../../snyk-cli/fix-vulnerabilities-from-the-cli/ignore-vulnerabilities-using-snyk-cli.md)
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
* 매니페스트 파일이 표준 요구 사항 `requirements.txt`가 아니기 때문에 Pip 프로젝트를 검색하고 `--file=` 옵션을 사용하는 경우 다음 옵션을 사용하여 Pip을 패키지 관리자 `--package-manager=pip`로 지정해야 합니다.

### .Net

`.sln` 파일을 사용하는 경우 파일의 경로를 지정할 수 있으며, Snyk는 다음과 같은 repo의 일부인 모든 하위 프로젝트를 검색합니다.

```
snyk test --file=sln/.sln
```

### Yarn

Yarn 워크스페이스의 경우 `--yarn-workspaces` 옵션을 사용하여 패키지를 테스트하고 모니터링합니다. 루트 잠금 파일은 모든 패키지의 검색을 위해 참조됩니다. `--detection-depth` 옵션을 사용하여 기본적으로 자동으로 검색되지 않는 하위 폴더를 찾습니다.

{% hint style="info" %}
**Note**\
Yarn 워크스페이스 지원은 현재 `snyk test` 및 `snyk monitor` 명령어에서만 지원합니다.
{% endhint %}

Example: 현재 디렉터리와 5개의 하위 디렉터리에서 검색된 작업 공간에 속하는 패키지만 검색합니다.

```
snyk test --yarn-workspaces --detection-depth=6
```

정책 경로를 다음과 같이 제공하여 탐지된 모든 작업 공간에 적용할 무시 및 패치를 한 곳에 유지 관리하는 경우 일반적으로 [`.snyk` policy file](../../../snyk-cli/test-for-vulnerabilities/the-.snyk-file.md)을 사용할 수 있습니다.

```
snyk test --yarn-workspaces --policy-path=src/.snyk
```

### Monorepo

일부 고객은 여러 언어, 패키지 관리자 및 프로젝트를 단일 저장소에 포함하는 복잡한 프로젝트를 가지고 있습니다. 이를 위해 다음과 같은 다양한 방법을 사용할 수 있습니다.

*   각 프로젝트 및 언어를 작성할 때 `snyk test`를 실행하고 특정 프로젝트 파일을 대상으로 하는 지시문을 추가하는 예시는 다음과 같습니다.

    ```
    snyk test --file=package.json
    ```

    각 프로젝트의 종속성을 설치한 후 특정 아티팩트(예: `pom.xml`)를 가리키는 유사한 호출을 수행합니다. 이는 빠르고 효율적이지만 특히 프로젝트에 익숙하지 않은 경우 확장하기가 어려울 수 있습니다.
* `--all-projects` 및 `--detection-depth` 옵션을 사용하면 Snyk CLI 또는 CI/CD 플러그인이 지원되는 파일 유형과 일치하는 매니페스트를 폴더 구조에서 `--detection-depth` 까지 검색합니다. **각 프로젝트**는 검색되고 고유한 결과가 있습니다. 마찬가지로 `snyk monitor`를 사용하는 경우 각 프로젝트에 대해 별도의 결과가 생성됩니다. 이렇게 하면 특히 node, .net, python 등에 걸친 프로젝트가 있는 경우 검색을 자동화할 수 있습니다.
* 대부분의 **Gradle 프로젝트**의 경우`--all-projects` 를 사용하면 `--all-projects` 검색의 일부로 빌드 파일을 찾을 때 `snyk test --file=build.gradle --all-sub-projects` 형식으로 장면 뒤에 있는 그래들별 옵션을 호출할 수 있습니다.
* **Gradle**에는 추가 구성 매개 변수가 필요할 수 있습니다. 그렇다면 다른 언어 및 패키지 관리자의 각 매니페스트에 대해 `--file=` 을 사용하여 다른 아티팩트를 대상으로 지정합니다. 그런 다음 `--all-sub-projects` 및 잠재적으로 `--configuration-matching`을 사용하여 복잡한 Gradle 프로젝트를 검색해야 합니다.

자세한 내용은 [Snyk for Java and Kotlin](../../../products/snyk-open-source/language-and-package-manager-support/snyk-for-java-gradle-maven.md)을 참조하십시오.

## Snyk Container별 전략

파이프라인에서 Snyk Container를 구현하는 가장 좋은 단계는 컨테이너 이미지가 빌드된 후(“docker build”에 해당하는 실행 후)이미지가 레지스트리에 푸시되거나 (“docker push”) 실행 중인 인프라(“helm install”, “kubectl apply”등)에 배포되기 전입니다.

일반적으로 컨테이너 build-test-deploy파이프라인을 실행하는 방법은 빌드 에이전트에서 도커 데몬을 사용할 수 있는지 여부에 따라 달라집니다.

### **Docker daemon**을 사용할 수 있는 경우 파이프라인 실행

다음과 같은 상황이 존재하는 경우 실행할 수 있습니다.

* Docker가 기본적으로 설치된 호스트에서 빌드 도구(예: Jenkins)를 직접 실행하고 있습니다.
* 파이프라인 작업은 호스트에 바인딩된 Docker 소켓 \[/var/run/docker.sock]이 있는 컨테이너 내부에서 실행됩니다.
* Docker-inside-Docker 설치를 실행하고 있습니다.

Snyk은 다음과 같이 도움을 줄 수 있습니다.

* When you run `snyk container test $IMAGE_NAME`을 실행하면 snyk은 로컬 데몬 저장소에서 해당 이미지를 찾습니다. 이미지가 존재하지 않는 경우 Docker가 해당 이미지를 업스트림 레지스트리에서 다운로드합니다.
* 레지스트리 인증의 경우 Snyk은 사용자가 이미 구성한 인증 정보(**docker login**)를 사용합니다.
* command line에 `--file=Dockerfile`을 지정하여 이미지 취약성 결과를 이미지를 빌드한 Docker 파일과 연결하고 인라인 수정 권고 및 대체 기본 이미지 제안을 받을 수 있습니다.

### **Docker daemon**을 사용할 수 없는 경우 파이프라인 실행

다음과 같은 상황이 발생합니다.

* 각 빌드 작업을 컨테이너화하지만 보안 및 성능상의 이유로 Docker 소켓을 마운트하지 않습니다.
* 파이프라인 작업은 호스트(또는 클러스터)로 분할되며 중앙 볼륨 또는 중간 레지스트리/개체 저장소를 통해 전달되는 아티팩트에 의존합니다.
* OCI 인증 컨테이너 이미지만 사용하는 에코시스템에서만 작업합니다.

Snyk은 다음과 같이 도움을 줄 수 있습니다.

* `snyk container test docker-archive:archive.tar` 또는 `snyk container test oci-archive:archive.tar`를 실행하여 Docker daemon에 의존하지 않고 tar 형식의 컨테이너 이미지에 대한 Snyk 취약점 결과를 가져옵니다.
* tar archive는 **docker save**과 동등한 기능을 사용하여 빌드 프로세스에서 생성하고 공유 볼륨 또는 개체 저장소에 저장할 수 있습니다. 다른 종속성이 필요 없이 Snyk 바이너리 파일을 실행하는 빌드 에이전트 컨테이너에서 액세스할 수 있습니다.

### 컨테이너 이미지와의 통합을 위한 권장 사항

* CI 중에 컨테이너 이미지와 통합하는 방법에 관계없이 Snyk Open Source (application SCA) 테스트와는 별도의 빌드 단계로 Snyk Container 스캔을 실행합니다. 이를 통해 빌드 오류를 각각 컨테이너/OS 계층 또는 애플리케이션 계층 내의 취약점으로 분리할 수 있습니다. 이를 통해 컨테이너형 빌드 작업도 더 쉽게 수행할 수 있습니다.
* `--fail-on` 및 `--severity-threshold` 와 같은 CLI 플래그를 사용하여 빌드 태스크의 오류 상태를 사용자 정의합니다. `--json`을 사용하여 전체 취약점 보고서가 포함된 JSON 파일을 생성하고 JSON 데이터를 기반으로 자체 빌드 실패 상태를 설정할 수 있습니다.
* `--exclude-base-image-vulns`를 전달하여 컨테이너의 기본 이미지(Docker 파일의 FROM 줄에 지정한 이미지)에서 발생하는 취약점 대신 사용자 계층에서 도입된 취약점만 보고합니다.
* `snyk container test` 후 `snyk container monitor`를 실행하십시오(또는 플러그인 설정의 Monitor 확인 선택). 이 컨테이너에 대한 BOM(Bill of Material) 기록을 Snyk UI 내에 유지하고 새로운 취약점을 매일 사전 모니터링합니다. 이 기능은 새 릴리스를 프로덕션 환경에 푸시할 때 유용합니다. `--project-name`을 사용하여 릴리스의 고유 식별자를 지정하여 프로덕션 컨테이너가 빌드 프로세스에서 다른 컨테이너와 별도로 추적되도록 할 수 있습니다.

## Snyk IaC 관련 전략

파이프라인에서 Snyk Infrastructure As Code를 구현하는 가장 좋은 방법은 단계 중 일부이지만 SCA 및 Containers 단계 이후입니다.

Snyk Infrastructure as Code는 다음을 지원합니다.

* Deployments, Pods 및 Services.
* CronJobs, Jobs, StatefulSet, ReplicaSet, DaemonSet 및 ReplicationController.

자세한 내용은 [CLI를 사용하여 Kubernetes 파일 테스트](../../../snyk-products/snyk-infrastructure-as-code/snyk-cli-for-infrastructure-as-code/test-your-kubernetes-files-with-our-cli-tool.md)를 참조하십시오.

## CI/CD 문제 해결 및 고급 팁

이 섹션에서는 CI/CD 통합 문제를 해결하거나 확장하는 데 도움이 되는 몇 가지 팁을 제공합니다.

### 1단계: Snyk CLI로 복제 시도

CLI와 파이프라인이 동일한 엔진을 실행하는 경우 프로젝트를 복제하고 CLI를 사용하여 검색해 보십시오.

CLI 옵션을 사용합니다. Snyk CLI 도구를 사용하여 파이프라인에서 실행할 때 알려진 취약점을 찾아 수정합니다. 자세한 내용은 [CLI reference](../../../snyk-cli/cli-reference/)를 참조하십시오.

### 2단계: 로그 가져오기

CLI를 사용하여 복제할 수 있지만 문제가 여전히 존재하는 경우 CLI에 `DEBUG=*` 명령을 사용하여 디버그 로깅을 출력하도록 요청하거나 `-d` 옵션을 사용하여 로그를 캡처합니다.

```
snyk test -d
```

or

```
DEBUG=* snyk test
```

### 3단계: 플러그인 대신 CLI 사용

CLI를 설치하여 기본 플러그인을 CLI로 교체해 보십시오. 자세한 내용은 [Install the Snyk CLI](../../../snyk-cli/install-the-snyk-cli/)를 참조하십시오.

## CI/CD 통합의 일반 CLI 옵션

CI/CD 통합에 사용하는 가장 일반적인 옵션은 다음과 같습니다.

`-- all-projects`: 작업 디렉토리의 모든 프로젝트 자동 검색

`-p`: 디펜던시 트리를 제거하여 중복된 하위 종속성을 제거합니다. 모든 취약점을 계속 찾지만 모든 취약한 경로를 찾지는 못할 수 있습니다.

\--org=\<ORG\_ID>: 특정 조직에 연결된 Snyk 명령을 실행할 ORG\_ID 를 지정합니다. 이는 `monitor` 명령을 실행한 후 새 프로젝트가 생성되는 위치, 일부 기능 가용성 및 개인 테스트 제한에 영향을 미칩니다. 조직이 여러 개인 경우 다음을 사용하여 CLI에서 기본값을 설정할 수 있습니다.

```
$ snyk config set org=<ORG_ID>
```

새로 테스트되거나 모니터링되는 모든 프로젝트가 기본 조직 아래에서 테스트되도록 기본값을 설정합니다. 기본값을 재정의해야 하는 경우 `--org=<ORG_ID>`를 사용하십시오.

Default: [Account settings](https://app.snyk.io/account)에서 현재 선호하는 조직인`<ORG_ID>`입니다.

## 유용한 **resources**

[GitHub CI/CD examples](https://github.com/snyk-labs/snyk-cicd-integration-examples)는 다양한 CI/CD 도구에 대한 바이너리 및 npm 통합의 몇 가지 예를 공유합니다.

CI/CD에 대한 자세한 내용은 [What is CI/CD? CI/CD Pipeline and Tools Explained](https://snyk.io/learn/what-is-ci-cd-pipeline-and-tools-explained/)를 참조하십시오.

## 지속적인 통합 구성

디펜던시의 알려진 취약점을 지속적으로 방지하려면 Snyk를 연속 통합(구축) 시스템에 통합하십시오. 해당 설명서와 더불어 Snyk GitHub 저장소의 [integration configuration examples](https://github.com/snyk/actions#snyk-github-actions)를 확인하십시오.

## 자동 모니터링 설정

Snyk로 프로젝트를 모니터링하면 프로젝트의 디펜던시가 새로 공개된 취약점의 영향을 받는 경우 알림이 표시됩니다. 프로젝트에 대해 Snyk이 가지고 있는 종속성 목록을 최신 상태로 유지하려면 배포 프로세스에서 Snyk monitor를 실행하여 해당 목록을 계속 새로 고칩니다. SNYK\_TOKEN 환경 변수를 포함하도록 환경을 구성합니다. 로그인 후 대시보드에서 API 토큰을 찾을 수 있습니다.

## API 토큰 구성

다른 사람에게 노출되지 않도록 API 토큰을 소스 컨트롤에 체크인하지 마십시오. 대신 CI 환경 변수를 사용하여 구성하십시오.

다음 문서에서 이 작업을 수행하는 방법을 참조하십시오.

* [Travis](https://docs.travis-ci.com/user/environment-variables/)
* [Circle](https://circleci.com/docs/environment-variables/)
* [Codeship](https://codeship.com/documentation/continuous-integration/set-environment-variables/)

[Google search](https://www.google.co.uk/search?q=setting+up+env+variables+in+CI)를 통해 다른 사람들을 찾을 수 있습니다.
