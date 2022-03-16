# Snyk for Java (Gradle, Maven)

Snyk은 CLI 및 애플리케이션 UI(app.snyk.io)를 통해 취약점에 대한 보안 스캔을 제공합니다.

**지원하는 버전**: 공식적으로 지원되는 Java 버전, 운영 체제 및 Node.js 버전은 [Gradle support](https://github.com/snyk/snyk-gradle-plugin#support) 와 [Maven support](https://github.com/snyk/snyk-mvn-plugin#support)를 참조하십시오.

## 특징

다음 표는 언어 별로 제공되는 일반적인 기능에 대한 개요를 제공합니다. 이러한 기능 외에도 관련된 추가 기능을 제공합니다.

{% hint style="info" %}
요금제에 따라서 일부 기능을 사용하지 못할 수 있습니다. 자세한 내용은 [pricing plans](https://snyk.io/plans/)을 참조하십시오.
{% endhint %}

| Package managers / Features       | CLI support | Git support | License scanning | Fixing                                                                                                                          | Runtime monitoring |
| --------------------------------- | ----------- | ----------- | ---------------- | ------------------------------------------------------------------------------------------------------------------------------- | ------------------ |
| [Maven](https://maven.apache.org) | ✔︎          | ✔︎          | ✔︎               | ✔︎                                                                                                                              | ✔︎                 |
| [Gradle](https://gradle.org)      | ✔︎          | ✔︎          | ✔︎               | [Fix advice](../../../features/fixing-and-prioritizing-issues/starting-to-fix-vulnerabilities/fix-your-vulnerabilities.md) only |                    |

## Java 프로젝트(CI/CD)에서 Snyk CLI 사용하기

Snyk이 디펜던시를 분석하고 구축하는 방식은 프로젝트의 언어 및 패키지 관리자에 따라 다릅니다.

다음과 같이 Java 프로젝트에 도구를 사용하는법을 안내합니다.

* Gradle이 포함된 Snyk CLI: 디펜던시 그래프를 빌드하기 위해 Snyk은 Gradle과 통합하고 빌드에서 반환된 디펜던시를 검사합니다. 다음 매니페스트 파일이 지원됩니다. `build.gradle, build.gradle.kts`
* Maven이 포함된 Snyk CLI: 디펜던시 트리를 빌드하기 위해 Snyk은 `pom.xml`파일을 분석합니다.

## CLI parameters for Java

이 섹션에서는 다음과 같이 Java 기반 프로젝트로 작업할 때 사용할 수 있는 CLI 명령어에 대해 설명합니다.

### 전제 조건

* Snyk CLI를 사용하기 전에 관련 패키지 매니저를 설치하십시오.
* 테스트 진행 이전에 Snyk에서 지원하는 관련 매니페스트 파일을 포함합니다.
* [Snyk CLI](../../../features/snyk-cli/install-the-snyk-cli/)를 설치하고 인증하여 로컬 환경에서 프로젝트 분석을 시작합니다.

### Snyk CLI 파라미터

CLI에서 Gradle 프로젝트로 작업할 때 다음 옵션을 추가하여 스캔 작동 방식을 세분화할 수 있습니다.

| **Option**                    | **Description**                                                                                                                                                                             |
| ----------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `--sub-project=`              | "multi-project" 구성의 경우 특정 하위 프로젝트를 테스트합니다.                                                                                                                                                  |
| `--all-sub-projects`          | "multi-project" 구성의 경우 모든 하위 프로젝트를 테스트합니다.                                                                                                                                                  |
| `--configuration-matching=`   | 제공된 Java 정규식과 일치하는 구성만 사용하여 디펜던시를 해결합니다. 예: `'^releaseRuntimeClasspath$'`                                                                                                                   |
| `--configuration-attributes=` | 디펜던시를 해결하려면 구성 속성의 특정 값을 선택하세요. 예: `'buildtype:release,usage:java-runtime'`                                                                                                                 |
| `--all-projects`              | monorepos에 사용됩니다. 지원되는 모든 매니페스트가 감지됩니다. Gradle monorepos의 경우 Snyk은 root의 **build.gradle / build.gradle.kts** 파일만 찾고 이후 동일한 논리를 적용합니다. `--all-sub-projects`는 nomorepo의 root에서 실행되도록 설계되었습니다. |

### Snyk CLI를 통해 추가 인수를 Gradle 또는 Maven에 직접 전달

다음과 같이 Snyk 명령어 뒤에 제공하여 추가 인수를 **gradle** 또는 **mvn**에 직접 전달할 수 있습니다.

```
snyk test -- --build-cache
```

**Snyk CLI에서 Maven 인수를 사용하는 방법 예시**

"prod"라는 특정 Maven 프로필을 테스트합니다.

```
snyk test -- -prod
```

pom.xml 파일에서 시스템 속성을 추가합니다.

예제는 다음과 같습니다.

패키지 버전은 pom.xml에 나타납니다.

```
${pkg_version}
```

다음과 같이 시스템 속성을 정의합니다.

```
snyk test -- -Dpkg_version=1.4
```

## Gradle 프로젝트에 대한 CLI help

### 하위 프로젝트

Gradle 빌드는 여러 하위 프로젝트로 구성될 수 있으며, 각 하위 프로젝트에는 자체 build.gradle 파일이 있는 반면 root 프로젝트에는 setting.gradle 파일도 포함되어 있습니다. 하위 프로젝트는 root 프로젝트에 따라 다르지만 다른 방식으로 구성할 수 있습니다.

기본적으로 Snyk CLI는 현재 프로젝트(현재 폴더의 root에 있는 프로젝트)또는 `--file=path/to/build.gradle`로 지정된 프로젝트만 검색합니다.

*   모든 프로젝트를 한번에 스캔하려면(권장) `--all-sub-projects` 플래그를 사용하세요.

    ```
    snyk test --all-sub-projects
    ```

**Note:** 개별 하위 프로젝트는 UI에서 별도의 Snyk 프로젝트로 나타납니다.

*   특정 프로젝트를 스캔하려면(예: myapp) 다음과 같이 진행합니다.

    ```
    snyk test --sub-project=myapp
    ```

### 구성

Gradle 디펜던시는 특정 범위에 대해 선언되며 각 범위는 [Configurations](https://docs.gradle.org/current/userguide/declaring\_dependencies.html#sec:what-are-dependency-configurations)의 도움으로 Gradle로 표시됩니다.

* 개발 디펜던시를 위한 **compileOnly**
* 컴파일 및 런타임 디펜던시를 포함하는 **compile**

기본적으로 Snyk은 프로젝트/프로젝트의 모든 구성에 대한 디펜던시의 합계를 기반으로 Gradle에서 반환된 모든 구성을 디펜던시 그래프에 병합합니다.

특정 구성을 테스트하기위해 다음과 같이 진행합니다.

* `--configuration-matching` 파라미터로 [Java 정규식](https://docs.oracle.com/javase/tutorial/essential/regex/)(대소문자 구분 안 함)과 함께 옵션을 사용하세요. 이후 일치하는 구성이 테스트됩니다. 여러 구성이 일치하면 모두 병합되어 함께 해결됩니다. 예:`'^releaseRuntimeClasspath$|^compile$'`
* 다른 하위 프로젝트에 다은 구성이 포함된 경우 각 하위 프로젝트를 개별적으로 스캔합니다.

**--configuration-matching을 사용하는 방법의 예:**

* `--configuration-matching=compile` compile, testCompile, compileOnly 등과 일치합니다.
* `--configuration-matching=^compile$` 컴파일만 일치합니다.
* `--configuration-matching='^(debug|release)compile$'` debugCompile 및 releaseCompile과 일치합니다.

### Android 빌드 변형

Android Gradle은 [빌드 변형](https://developer.android.com/studio/build/build-variants)을 구성하여 다양한 버전의 앱 생성을 지원합니다.

Snyk은 기본적으로 사용 가능한 모든 구성을 병합하기 때문에 변형으로 병합할 수 없는 구성이 충돌하게 됩니다.

이 경우 Snyk 스캔은 다음 메시지 중 하나를 포함할 수 있는 Gradle의 오류와 함께 실패합니다.

* _Cannot choose between the following configurations of `project :mymodulewithvariants`_
* _Cannot choose between the following variants of `project :mymodulewithvariants`_
* _Could not select value from candidates_

이러한 충돌을 피하기 위해서 다음과 같이 진행합니다.

*   **특정 구성 사용**: 모든 필수 속성이 있고 구성이 테스트에 포함된 모든 하위 프로젝트에서 동일한 빌드 구성을 알고 있는 경우 해당 구성을 지정합니다.

    ```
    --configuration-matching=prodReleaseRuntimeClasspath
    ```
*   **디펜던시 구성을 명시적으로 지정합니다**: 특정 구성을 사용하도록 builde.gradle 파일에서 프로젝트 내 디펜던시를 수정합니다.

    ```
      dependencies {
          implementation project(path: ':mymodulewithvariants', configuration: 'default')
      }
    ```
*   **구성 속성 제한**: 명령을 실행할 때 오류가 수신되면 오류는 사용 가능한 소성 값을 나타낼 수 있으며 Gradle의 오류 세부 정보는 어떤 종속성 변형이 어떤 속성과 일치하는지도 나타냅니다. 이러한 세부 정보를 사용하여 속성 필터옵션을 추가합니다.

    ```
    snyk test --configuration-attributes=buildtype:release,usage:java-runtime,mode:demo
    ```

    또는 다음의 명령어를 사용하여 변형을 일치 시킵니다. `com.android.build.api.attributes.BuildTypeAttr=release` and `org.gradle.usage=java-runtime`

### 데몬

기본적으로 Snyk은 `gradle build --no-daemon`을 실행하여 background에서 `snyk test`와 `snyk monitor`를 진행합니다. 문제가 발생하면 다음과 같이 진행하십시오.

1. Gradle 데몬을 시작합니다.
2. `snyk test` 또는 `snyk monitor`에 `--daemon`을 추가하십시오.

### Lockfiles

Gradle 프로젝트에서 구성당 단일 **gradle.lock** 파일 또는 여러 **\*.lock** 파일을 사용하는 경우 다음과 같은 문제가 발생합니다.

**Gradle Error (short): > Could not resolve all dependencies for configuration ':compileOnly'. > Locking strict mode: Configuration ':compileOnly' is locked but does not have lock state.**

**compileOnly 구성은 더 이상 사용되지 않으며** 프로젝트가 잠금 파일을 성공적으로 생성하더라도 이 구성을 확인할 수 없으므로 compileOnly 상태는 포함하지 않습니다. 확인 가능한 구성만 종속성 그래프를 계산합니다. 이 문제를 해결하려면 **dependencyLocking 논리를 포함하는 build.gradle을 다음 명령으로 업데이트하는 것이 좋습니다.**

```
compileOnly {resolutionStrategy.deactivateDependencyLocking() }
```

이렇게 하면 **compileOnly가 무시**되고 프로젝트 분석에 필요한 정보만 저장됩니다.

### Support

Snyk으로 Gradle 프로젝트를 테스트하는데 문제가 발생하는 경우 다음 세부 정보를 수집하여 [`support@snyk.io`](mailto:support@snyk.io)로 보내주시면 도와드리겠습니다.

* `build.gradle`
* `settings.gradle` (especially if we did not pick up a version of a package)
* 다음 명령어를 통한 출력된 내용
  * `$ snyk test -d`
  * `$ gradle dependencies -q`

## Maven 프로젝트를 위한 Git Services

가져올 프로젝트를 선택한 후 `pom.xml` 파일을 기반으로 디펜던시 트리를 빌드합니다.

## Gradle 프로젝트를 위한 Git Services

가져올 프로젝트를 선택한 후 `build.gradle` 파일 및 `gradle.lockfile`(선택사항)을 기반으로 디펜던시 트리를 빌드합니다.

`build.gradle.kts` 파일은 현재 Git에서 지원하지 않습니다.

lockfile이 있는 경우 Snyk은 이를 사용하여 프로젝트에 사용된 디펜던시의 최종 버전을 정확하게 해결합니다.

Gradle lockfile은 다른 이점 중에서도 재현 가능한 빌드를 가능하게 하는 옵트인 기능입니다. 자세한 내용은 [Gradle 디펜던시 잠금](https://docs.gradle.org/current/userguide/dependency\_locking.html)을 참조하십시오.

## Git settings for Java

Snyk UI에서는 Artifactory for Maven에서 패키지를 확인하려는 미러 또는 저장소를 지정할 수 있습니다.

artifactory 통합 구성에 대한 자세한 내용은 아래 페이지를 참조하십시오.

{% content-ref url="../../../features/integrations/private-registry-integrations/artifactory-registry-for-maven.md" %}
[artifactory-registry-for-maven.md](../../../features/integrations/private-registry-integrations/artifactory-registry-for-maven.md)
{% endcontent-ref %}

## Additional Snyk support for Java

Snyk CLI 및 UI 기능 외에도 이러한 통합을 통해 Java 프로젝트를 확인할 수 있습니다.

{% content-ref url="../../../features/integrations/ci-cd-integrations/maven-plugin-integration.md" %}
[maven-plugin-integration.md](../../../features/integrations/ci-cd-integrations/maven-plugin-integration.md)
{% endcontent-ref %}
