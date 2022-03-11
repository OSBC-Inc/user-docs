# Snyk CI/CD 통합: 모범 사례

### 구현 옵션

{% hint style="info" %}
이 모든 방법은 동일한 Snyk 엔진에 의존하기 때문에 동일한 결과를 제공합니다. 따라서 어떤 배포 방법을 선택하든 동일한 인수나 옵션이 참이어야 합니다.
{% endhint %}

#### CI/CD 배치 방법

파이프라인 내에서 Snyk을 구성하는 다양한 방법이 있습니다. 어떤 방법을 선택할지는 주로 환경 및 선호도에 따라 결정할 수 있으며, 이러한 방법을 모두 성공적으로 실행할 수 있습니다.

**Snyk 기본 플러그인 사용**

대부분의 일반적인 CI/CD 도구에 사용할 수 있습니다. 설치 및 시작하기에 가장 쉬운 방법입니다. 플러그인에는 인터페이스 UI에서 가장 일반적인 매개 변수와 옵션이 포함되어 있습니다.

**npm을 사용하여 Snyk CLI를 배치하는 방법**

CLI를 로컬로 설치하는 것과 유사한 방법입니다. 파이프라인 스크립트에서 npm 명령을 실행할 수 있어야 합니다. 이 방법을 사용하면 CLI 환경에 완벽하게 적응할 수 있으므로 쉽게 문제를 해결하고 구성할 수 있습니다.

**Snyk CLI 바이너리 버전 배치**

바이너리 설정의 장점은 로컬 환경과의 종속성이 없다는 것입니다. 예를 들어 파이프라인에서 npm 명령을 실행할 수 없는 경우에 유용합니다.

CLI 바이너리 파일은 [https://github.com/snyk/snyk/tags](https://github.com/snyk/snyk/tags)에서 확인할 수 있습니다.

Snyk은 Linux, Windows 및 기타 버전을 가지고 있습니다.

**Snyk 컨테이너 배치**

Dockerhub의 이미지 중 하나를 사용하여 파이프라인에 Snyk을 배치할 수도 있습니다: [https://hub.docker.com/r/snyk/snyk](https://hub.docker.com/r/snyk/snyk)

#### 예

다음 저장소는 다양한 CI/CD 도구에 대한 바이너리 및 NPM 통합의 몇 가지 예를 공유합니다:

[CI/CD examples](https://github.com/snyk-labs/snyk-cicd-integration-examples)

### 일반적인 선택 방식

개발팀은 일반적으로 다음 단계를 따라 Snyk을 채택합니다:

1. [취약점 노출](snyk-cicd-integration-good-practices.md) (snyk monitor)
2. [Snyk을 gatekeeper로 사용](snyk-cicd-integration-good-practices.md) (snyk test)
3. [지속적인 모니터링](snyk-cicd-integration-good-practices.md) (snyk test + Snyk monitor)

### **1**단계\*\*:\*\* 취약점 노출 **(Snyk monitor)**

이는 일반적인 초기 접근 방식이며, 개발 프로세스 중 Snyk의 결과를 통해 팀의 취약점에 대한 가시성이 향상됩니다.

파이프라인에서 Snyk을 처음 구현할 때는 **snyk monitor** 명령만 사용하거나 Snyk의 CI 플러그인 중 하나를 사용하여 플러그인이 빌드에 실패하지 않도록 구성하는 것이 좋습니다.

모든 프로젝트가 취약하기 때문이며, 빌드에 실패하는 Snyk 설정을 한 후 Snyk으로 인해 모든 빌드가 실패하게 되는 문제가 발생할 수 있습니다.

**snyk monitor**를 사용하여 결과를 도출하면 프로세스를 중단하지 않고 정보를 제공할 수 있습니다.

### **2**단계\*\*:\*\* Snyk을 gatekeeper로 사용 **(snyk test)**

이 접근 방식은 새로운 취약점(“stopping the bleeding”이라고도 함)의 유입을 방지합니다.

팀에서 애플리케이션의 취약점을 이해하고 개발 초기에 수정하는 프로세스를 개발한 후에는 취약점에 대해 빌드에 실패하도록 Snyk을 구성하여 애플리케이션 취약점이 유입되지 않도록 할 수 있습니다.

빌드에 **snyk test**를 추가하거나 fail 기능을 활성화하여 Snyk이 빌드에 실패하도록 하여 결과를 콘솔에 출력합니다. Devs 또는 DevOps 팀은 결과를 통해 빌드를 중지할지 계속할지를 결정할 수 있습니다.

### **3**단계\*\*:\*\* 지속적인 모니터링 **(snyk test + Snyk monitor)**

취약점이 감지될 때 빌드에 실패하도록 Snyk을 구성한 후 지속적인 모니터링을 위해 프로젝트의 성공적인 빌드에 대한 스냅샷을 Snyk으로 보내도록 Snyk을 구성할 수 있습니다.

이렇게 하려면 snyk test가 성공적인 종료 코드를 반환할 경우 synk monitor를 실행하도록 파이프라인을 구성하십시오.

## 기술 구현

### 전제조건

파이프라인에서 실행되도록 Snyk를 구성하려면 Snyk 계정에서 주요 구성 입력을 검색합니다.

### 대상 조직 정의

CI/CD 플랫폼에서 Snyk을 실행할 때 일반적으로 테스트 결과 검토 및 지속적인 모니터링을 위해 Snyk에 업로드합니다.

**--org** CLI 인수를 사용하여 URL slug(URL의 마지막 백슬래시 뒤의 URL 부분) 또는 조직 ID를 사용하여 Snyk CLI에서 대상 조직을 정의할 수 있습니다:

* Snyk UI에서 대상 조직을 볼 때 브라우저의 주소 표시줄에 표시되는 URL 슬러그를 사용하여 대상 조직을 정의할 수 있습니다:
* 또는 각 조직의 설정 페이지에서 **org id**를 사용하여 대상 조직을 정의할 수 있습니다.

![](../.gitbook/assets/image1.png)

**Default organization**

대상 조직을 정의하지 않으면 Snyk은 사용하는 인증 토큰에 기본 조직을 사용합니다:

* 사용자 계정의 경우 사용자가 선호하는 조직입니다.(사용자 설정에서 구성 가능)
* 조직 서비스 계정의 경우 계정이 생성된 조직입니다.

## Snyk 인증 토큰

snyk test를 실행하려면 원하는 대상 조직에 액세스할 수 있는 인증 토큰이 필요합니다. 유효한 인증 토큰을 사용할 수 있지만 서비스 계정을 사용하는 것이 좋습니다. 자세한 내용은 [Service accounts](https://docs.snyk.io/integrations/managing-integrations/service-accounts)를 참조하십시오.

## 설정

Snyk은 빌드 파이프라인에 테스트를 추가하는 다음과 같은 접근 방식을 지원합니다:

* **Snyk integration plugins**: Snyk은 [Jenkins](https://docs.snyk.io/integrations/ci-cd-integrations/jenkins-integration-overview), [Team City](https://docs.snyk.io/integrations/ci-cd-integrations/teamcity-integration-overview)[, Bitbucket Pipelines](https://docs.snyk.io/integrations/ci-cd-integrations/bitbucket-pipelines-integration-overview) 및 [Azure Pipelines](https://docs.snyk.io/integrations/ci-cd-integrations/azure-pipelines-integration)를 포함한 여러 CI 서버를 위해 사전 구축된 플러그인을 제공합니다.[ ](https://docs.snyk.io/integrations/ci-cd-integrations/azure-pipelines-integration)자세한 내용은 [Continuous Integration](https://docs.snyk.io/integrations/ci-cd-integrations)를 참조하십시오.
* **Snyk CLI:** 워크플로우가 복잡하거나 Snyk 사전 빌드 플러그인이 없는 빌드 시스템을 사용하는 경우에는 CI/CD 설정 중에 Snyk CLI 도구를 사용할 수 있습니다. 자세한 내용은 [Setting up using Snyk CLI](snyk-cicd-integration-good-practices.md) 를 참조하십시오.
* **Snyk API**: 요구사항이 복잡한 팀을 위해 Snyk은 스캔 시작, 새 프로젝트 온보딩, 임의 라이브러리 테스트 등의 기능에 사용할 수 있는 REST API를 제공합니다. 자세한 내용은 [Snyk API documentation](https://github.com/snyk/user-docs/tree/54e0dec0fe0e081d49f34119a9018499ad5c9e96/getting-started/snyk-billing-plan-onboarding/snyk-cicd-integration-good-practices/README.md) 을 참조하십시오.

## Snyk CLI를 사용하여 설정

Snyk CLI는 대부분의 CI/CD 환경에 쉽게 통합될 수 있도록 개발자가 직접 스크립팅할 수 있는 NodeJS 애플리케이션으로, NPM 애플리케이션, 사전 패키지된 바이너리 또는 컨테이너 이미지로 제공합니다. 자세한 내용은 [Install the Snyk CLI](https://docs.snyk.io/snyk-cli/install-the-snyk-cli)를 참조하십시오.

Snyk CLI는 다음과 같이 구성할 수 있습니다.

* 특정 조건이 충족될 때만 0이 아닌 오류 코드를 반환합니다. 예를 들어 심각도가 높은 취약점이 있는 경우에만 오류 코드와 함께 종료됩니다.
* 모든 데이터를 JSON으로 출력하여 유연성을 높일 수 있습니다.

**종료 코드**

* **snyk test**는 종료 코드로 끝나는 동기 명령입니다. 종료 코드는 빌드 시스템에서 테스트 결과에 따라 빌드를 통과하거나 실패하는 데 사용할 수 있습니다. 종료 상태 및 그 의미에 대한 자세한 내용은 [CLI reference guide](https://docs.snyk.io/snyk-cli/guides-for-our-cli/cli-reference)를 참조하십시오.
* **snyk monitor**(Snyk 웹 UI에 테스트 결과를 게시함)는 비동기 명령으로, 취약점 상태에 기반한 종료 코드로 끝나지 않습니다.

접근 방식과 목표에 따라 파이프라인에서 두 명령 집합을 모두 사용해야 할 수도 있습니다.

**CLI Examples**

빌드 파이프라인에서 Snyk CLI를 실행하는 예:

1.  snyk monitor를 통해 취약점을 표시하고 지속적인 모니터링을 위해 Snyk UI에 게시합니다:

    ```
    snyk monitor --all-projects --org=snyk-apps
    ```
2.  Snyk test to fail the build on high severity issues:

    ```
    snyk test --all-projects --org=snyk-apps --severity-threshold=high
    ```

CLI에서 전체 flags 목록을 보려면 **snyk --help** 또는 **snyk container --help**를 실행합니다.

## 실패한 빌드 매개 변수 구성

**snyk test** 명령에 flags를 추가하여 빌드에 실패할 파라미터를 미세 조정할 수 있습니다.:

* **--severity-threshold=high**: 높은 심각도 문제에 대해서만 빌드 실패:
* **--fail-on=upgradable**: 업그레이드 가능한 문제에 대해서만 빌드 실패(Snyk 수정 조언을 통해 해결할 수 있음):

또한 Snyk JSON 출력의 다른 파라미터(예: CVSS 점수)에 대해 [snyk-filter](https://github.com/snyk-tech-services/snyk-filter)와 같은 wrapper를 사용하여 빌드에 실패하거나 [snyk-delta](https://support.snyk.io/hc/en-us/articles/360019979978)와 같은 추가 도구를 사용하여 마지막 빌드 이후 발견된 문제에 대해서만 빌드를 실패할 수 있습니다.

## 사용자 지정 빌드 아티팩트 작성

Snyk의 JSON 출력을 사용하여 [snyk-to-html](https://github.com/snyk/snyk-to-html) 유틸리티 또는 개발하는 기타 사용자 지정 프로세싱을 사용하여 사용자 정의 테스트 보고서를 빌드 아티팩트로 생성할 수 있습니다.

## 새 취약점에 대한 작업 항목 만들기

Snyk을 사용하면 JIRA에서 새 작업 항목을 자동으로 생성할 수 있습니다. (JIRA integration documentation 참조) 특정 요구사항에 맞게 이 코드를 사용자 정의하거나 다른 작업 관리 시스템과 함께 작동하도록 조정할 수 있습니다.

시작하려면 [Jira tickets for new vulns](https://github.com/snyk-tech-services/jira-tickets-for-new-vulns)나 [API to create Jira tickets](https://github.com/snyk/user-docs/tree/54e0dec0fe0e081d49f34119a9018499ad5c9e96/getting-started/snyk-billing-plan-onboarding/snyk-cicd-integration-good-practices/README.md#reference/projects/project-jira-issues/create-jira-issue)를 참고하십시오.

## Issues 무시

기본적으로 issues를 무시하지 않거나 Snyk-delta를 사용하지 않는 경우 문제가 발견될 때 파이프라인의 “snyk test”가 빌드에 실패합니다. 이러한 문제를 해결하지 않고 빌드를 계속하려면 다음을 수행할 수 있습니다:

* [Ignore issues using a Snyk policy file](https://docs.snyk.io/snyk-cli/fix-vulnerabilities-from-the-cli/ignore-vulnerabilities-using-snyk-cli)
* [Ignore issues from the Snyk UI](https://support.snyk.io/hc/en-us/articles/360000923498-How-can-I-ignore-a-vulnerability-)
* [Ignore issues from the Snyk API](https://snyk.docs.apiary.io/#reference/projects/project-ignores-by-issue/add-ignore)
* 대량 무시에는 Snyk Python API를 사용합니다. [https://github.com/snyk-labs/pysnyk](https://github.com/snyk-labs/pysnyk)와 [https://github.com/snyk-labs/pysnyk/blob/master/examples/api-demo-9c-bulk-ignore-vulns-by-issueIdList.py](https://github.com/snyk-labs/pysnyk/blob/master/examples/api-demo-9c-bulk-ignore-vulns-by-issueIdList.py)를 참조하십시오.

## Snyk 오픈 소스별 전략

이러한 전략은 Snyk의 SCA(Software Composition Analysis) 테스트 기능을 사용하는 팀에 유용합니다.

### Gradle & Scala

* “다중 프로젝트” 구성의 경우, 모든 하위 프로젝트를 테스트하고, monitor 또는 test 명령과 함께 다음 flag를 사용합니다. **--all-sub-projects**
* 특정 구성을 스캔하려면 디펜던시를 해결할 특정 구성 값을 선택해야 합니다. 다음 flag를 test 또는 monitor 명령과 함께 사용합니다. **--configuration-attributes=**

### Python

*   Snyk은 Python을 사용하여 사용자의 디펜던시를 스캔하고 찾습니다. Snyk은 스캔을 시작하기 위해서는 Python 버전이 필요하며 기본값은 “python”입니다. 여러 Python 버전을 사용하는 경우 이 파라미터를 사용하여 실행을 위한 올바른 Python 명령을 지정합니다.

    test 또는 monitor cmd와 함께 다음 flag를 사용하여 Python 버전을 지정합니다. **--command=** 예:

    ```
    snyk test --command=python3
    ```
* If you scan a Pip project and use the **--file=** because your manifest file isn’t the standard of **requirement.txt**, then the next flag is mandatory to specify Pip as the package manager **--package-manager=pip**

### .Net

.sln 파일을 사용하는 경우 파일의 경로를 지정할 수 있습니다. 그러면 snyk은 저장소의 일부인 모든 하위 프로젝트를 검색합니다. 예:

```
snyk test --file=sln/.sln
```

### Yarn Workspace

Yarn workspace의 경우 **--yarn-workspaces** flag를 사용하여 패키지를 테스트하고 모니터링합니다. root lockfile은 모든 패키지를 검색할 때 참조됩니다. -**-detection-depth** 파라미터를 사용하여 기본적으로 자동 검색되지 않는 하위 폴더를 찾습니다.

{% hint style="info" %}
**Note**\
Yarn workspaces는 현재 **snyk test** 및 **snyk monitor** 명령만 지원합니다.
{% endhint %}

Example:

```
snyk test --yarn-workspaces --detection-depth=6
```

이 디렉토리와 깊이 5개의 하위 디렉토리가 검색된 작업 영역에 속한 패키지만 검색합니다.

정책 경로를 제공하여 탐지된 모든 작업 공간에 적용되도록 한 곳에서 무시/패치를 유지하는 경우 공통 **.snyk** 정책 파일을 사용할 수 있습니다.

```
snyk test --yarn-workspaces --policy-path=src/.snyk
```

### Monorepo

일부 고객은 단일 저장소에 여러 언어, 패키지 관리자 및 프로젝트가 포함된 복잡한 프로젝트를 가지고 있습니다. 이를 용이하게 하기 위해 다음과 같은 다양한 방법을 사용할 수 있습니다:

*   각 프로젝트/언어를 작성할 때 snyk test를 실행하고 특정 프로젝트 파일을 대상으로 지정하는 지시문을 추가합니다. 예:

    ```
    snyk test --file=package.json
    ```

    각 프로젝트의 디펜던시를 설치한 후 특정 아티팩트(예: **pom.xml**)를 가리키는 비슷한 호출을 수행합니다. 이 방법은 빠르고 효율적이지만 특히 프로젝트가 익숙하지 않은 경우 확장하기 어려울 수 있습니다.
* **--all-projects** 및 **--detection-depth** 인수를 사용합니다. 그러면 Snyk CLI 또는 CI/CD 플러그인은 폴더 구조에서 지원되는 파일 유형과 일치하는 매니페스트에 대해 **--detection-depth**까지 검색합니다. 각 프로젝트는 검사되고 자체 결과가 있습니다. 마찬가지로 **snyk-monitor**를 사용하는 경우 각 프로젝트에 대해 별도의 결과가 작성됩니다. 이것은 특히 node, .net, python 등에 걸친 프로젝트가 있는 경우 스캔을 자동화하는 좋은 방법입니다.

**Specific to Gradle:**

* 대부분의 Gradle 프로젝트에서 **--all-projects**를 사용하면 다음과 같은 형태로 백그라운드에서 Gradle 관련 옵션을 호출할 수 있습니다:

```
  snyk test --file=build.gradle --all-sub-projects
```

when it finds the build file as part of the **--all-projects** search

* Gradle에는 추가 구성 파라미터가 필요할 수 있습니다. 이 경우 첫 번째 옵션에서 언급한 것처럼 다른 언어/패키지매니저에 대해 \*\*--file=\*\*을 사용하여 다른 아티팩트를 대상으로 지정합니다. 그런 다음 **--all-sub-projects** 및 잠재적으로 **--configuration-matching** 및 --configuration-matching을 사용하여 복잡한 gradle 프로젝트를 스캔해야 합니다.

자세한 내용은 [Snyk for Java (Gradle, Maven)](https://support.snyk.io/hc/en-us/articles/360003817357-Java-for-Snyk)를 참조하십시오.

## Snyk 컨테이너별 전략

파이프라인에서 Snyk Container를 구현하는 가장 좋은 단계는 컨테이너 이미지가 빌드된 후(“docker build”와 동등한 단계를 실행한 후)와 이미지가 레지스트리에 푸시되거나 실행중인 인프라에 배포되기 전입니다. (“helm install”, “kubectl apply” 등).

일반적으로 컨테이너 빌드 테스트 배포 파이프라인을 실행하는 방법은 빌드 에이전트에서 도커 데몬을 사용할 수 있는지 여부에 따라 달라집니다.

**도커 데몬을 사용할 수 있는 경우 파이프라인 실행**

If:

* Docker가 기본적으로 설치된 호스트에서 직접 빌드 도구(예: Jenkins)를 실행하고 있습니다.
* 파이프라인 작업은 도커 소켓 \[/var/run/docker.sock] 바인드가 호스트에 마운트된 컨테이너 내에서 실행됩니다.
* Docker-inside-Docker setup을 실행하고 있습니다.

Snyk은 다음 항목을 도울 수 있습니다.

* snyk 컨테이너 테스트 **snyk container test $IMAGE\_NAME**을 실행하면, Snyk은 로컬 데몬의 저장소에서 해당 이미지를 찾고, 이미지가 없는 경우 업스트림 레지스트리에서 도커와 동등한 작업을 수행하여 다운로드합니다.
* 레지스트리 인증의 경우 Snyk은 이미 구성한 인증을 사용합니다(**docker login** 등).
* 명령줄에 **--file=Dockerfile**을 지정하여 이미지 취약점 결과를 만든 Dockerfile과 연결하고 인라인 수정 조언 및 대체 기본 이미지 제안을 받을 수 있습니다.

**도커 데몬을 사용할 수 없는 경우 파이프라인 실행**

해당 상황은 다음과 같은 경우입니다.

* 각 빌드 작업을 컨테이너에 포함하지만 보안/성능상의 이유로 Docker 소켓을 마운트하지 않는 경우
* 파이프라인 작업은 호스트(또는 클러스터) 간에 분할되며 중앙 볼륨 또는 중간 레지스트리/오브젝트 저장소를 통해 전달할 아티팩트에 의존하는 경우
* OCI 호환 컨테이너 이미지만 사용하는 에코시스템에서만 작업하는 경우

Snyk은 다음과 같이 도울 수 있습니다.

* 도커 데몬에 의존하지 않고 tar 형식 컨테이너 이미지에 대한 Snyk 취약점 결과를 가져오려면 `snyk container test docker-archive:archive.tar` 또는 `snyk container test oci-archive:archive.tar` 를 실행합니다.
* tar 아카이브는 공유 볼륨 또는 객체 저장소에 저장 및 저장되는 **docker save**와 동등한 기능을 사용하여 빌드 프로세스에서 생성할 수 있습니다. 그런 다음 Snyk 바이너리를 실행하는 빌드 에이전트 컨테이너로 액세스할 수 있으며 다른 종속성이 필요하지 않습니다.

## 모범 사례 권장 사항

* CI 중에 컨테이너 이미지와 통합하는 방법에 관계없이 Snyk Open Source(애플리케이션 SCA) 테스트와는 별도의 빌드 단계로 Snyk Container 스캔을 실행합니다. 이를 통해 각각 컨테이너/OS 계층 또는 애플리케이션 계층 내의 취약성에 대한 build failures를 분리할 수 있습니다. 또한 컨테이너 빌드 작업을 보다 쉽게 수행할 수 있습니다.
* 빌드 작업의 실패 상태를 사용자 지정하려면 **--fail-on** 및 **--severity-threshold**와 같은 CLI 플래그를 사용합니다. 추가적인 사용을 위해 **--json**을 사용하여 전체 취약점 보고서가 포함된 JSON 파일을 생성하고 JSON 데이터 기반의 자체 빌드 실패 상태를 설정할 수 있습니다.
* 컨테이너의 기본 이미지(Dockerfile의 FROM 절에 지정한 이미지)에서 발생하는 취약점 대신 사용자 계층에서 도입된 취약점만 보고하려면 **--exclude-base-image-vulns**를 전달합니다.
* **snyk container test** 후 **snyk container monitor**를 실행(또는 plugin settings에서 **Monitor** 확인란)하여 이 컨테이너의 BOM(Bill of Material) 기록을 Snyk UI 내에 유지하고 매일 새로운 취약점을 사전에 모니터링합니다. 이 기능은 새 릴리스를 프로덕션 환경으로 push할 때 유용합니다. **--project-name**을 사용하여 릴리스의 고유 식별자를 지정하여 프로덕션 컨테이너가 빌드 프로세스에서 다른 컨테이너와 별도로 추적하도록 할 수 있습니다.

## Snyk IaC별 전략

SCA 및 Containers 단계 이후 파이프라인에 Snyk Infrastructure as Code를 구현할 수 있는 최적의 단계입니다.

Snyk Infrastructure as Code는 다음 항목을 지원합니다.

* Deployments, Pods and Services.
* CronJobs, Jobs, StatefulSet, ReplicaSet, DaemonSet, and ReplicationController.

자세한 내용은 [CLI를 사용하여 Kubernetes 파일 테스트 진행](../products/snyk-infrastructure-as-code/snyk-cli-for-infrastructure-as-code/test-your-kubernetes-files-with-our-cli-tool.md)을 참조하십시오.

### CI/CD 문제 해결 & 팁

이 섹션에서는 CI/CD 통합을 해결하거나 확장하는 데 도움이 되는 몇 가지 팁을 알려드리겠습니다.

#### 1단계: Snyk CLI를 사용한 복제 시도

CLI와 파이프라인이 동일한 엔진을 실행하고 있습니다. 프로젝트를 복제하고 CLI를 사용하여 검색하십시오.

CLI 플래그 사용 - 파이프라인에서 실행하면서 알려진 취약성을 찾고 수정하려면 Snyk CLI 도구를 사용하십시오. [플래그 링크](../features/snyk-cli/cli-reference/)

#### 2단계: 로그 가져오기

CLI를 사용하여 복제할 수 있지만 여전히 문제가 있는 경우 다음 명령을 사용하여 CLI에 디버그 로깅을 출력하도록 요청하십시오.

capture logs는 DEBUG=\* or the -d flag 입니다.

```
snyk test -d
```

또는

```
DEBUG=* snyk test
```

#### 3단계: 플러그인 대신 CLI 사용

npm 또는 바이너리 다운로드를 사용하여 snyk을 설치하여 CLI에 기본 플러그인을 교체하십시오.

npm의 경우 다음 명령어를 사용합니다.

* npm install -g snyk
* Snyk auth
* Snyk test

바이너리를 다운로드하려면 다음 링크에서 snyk을 다운로드해야 합니다.

* [Download the Snyk CLI](https://github.com/snyk/snyk/tags)

#### CI/CD 통합의 공통 플래그

CI/CD 통합에 사용되는 가장 일반적인 플래그는 다음과 같습니다.

**-- all-projects**: 작업 디렉토리에 있는 모든 프로젝트 자동 검색

**-p**: 디펜던시 트리를 제거하고 중복된 하위 디펜던시를 제거합니다. 모든 취약점을 찾지만 잠재적으로 모든 취약점 경로는 찾지 못합니다.

**--org=ORG\_NAME**: 특정 조직에 연결된 Snyk 명령을 실행할 ORG\_NAME을 지정합니다. 이는 monitor 명령을 실행한 후 새 프로젝트를 생성할 위치에 영향을 미치며, 일부 기능의 가용성 및 비공개 테스트 제한에 영향을 미칩니다. 조직이 여러 개인 경우 다음 명령어를 사용하여 CLI에서 기본값을 설정할 수 있습니다.

```
$ snyk config set org=ORG_NAME
```

기본값을 설정하면 새로 모니터링되는 모든 프로젝트가 기본 조직 아래에 만들어집니다. 기본값을 재정의해야 하는 경우 --org=ORG\_NAME 옵션을 사용할 수 있습니다.

Default: [https://app.snyk.io/account](https://app.snyk.io/account)에서 기본값으로 설정된 ORG\_NAME을 사용합니다.

**유용한 리소스**

다음 보고서는 다양한 CI/CD 도구에 대한 바이너리 및 NPM 통합의 몇 가지 예를 공유합니다.

[GitHub CI/CD examples](https://github.com/snyk-labs/snyk-cicd-integration-examples)

### 지속적인 통합 구성

디펜던시에서 알려진 취약점을 지속적으로 방지하려면 Snyk을 지속적인 통합(build) 시스템에 통합하십시오. 해당 문서 외에도 GitHub 저장소에 있는 통합 구성 예제를 확인하시기 바랍니다.

### 자동 감시 설정

Snyk으로 프로젝트를 모니터링하는 경우 새로 공개된 취약점으로 인해 프로젝트의 디펜던시가 영향을 받을 경우 알림이 표시됩니다. 프로젝트에 대한 디펜던시 목록을 최신 상태로 유지하려면 배포 프로세스에서 Snyk monitor를 실행하여 스캔을 진행하고, SNYK\_TOKEN 환경 변수를 포함하도록 환경을 구성합니다. 로그인 후 대시보드에서 API 토큰을 찾을 수 있습니다.

### API 토큰 구성

API 토큰이 다른 사람에게 노출되지 않도록 하려면 해당 토큰을 소스 제어로 체크인하지 마십시오. 대신 CI 환경 변수를 사용하여 구성하십시오.

이 작업을 수행하는 방법은 지침을 참조하십시오.

* [Travis](https://docs.travis-ci.com/user/environment-variables/)
* [Circle](https://circleci.com/docs/environment-variables/)
* [Codeship](https://codeship.com/documentation/continuous-integration/set-environment-variables/)

[Google search](https://www.google.co.uk/search?q=setting+up+env+variables+in+CI)를 통해 다른 것들을 찾을 수 있습니다.\
[CI/CD](https://snyk.io/learn/what-is-ci-cd-pipeline-and-tools-explained/)에 대해 자세히 알아봅니다.
