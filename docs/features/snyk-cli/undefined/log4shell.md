# log4shell 명령 사용 방법

### 소개

`snyk log4shell` 은 **log4Shell** 취약성([CVE-2021-44228](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-44228))의 영향을 받는 **log4j** 라이브러리가 매니페스트 파일(예: pom.xml 또는 build.gradle)에 선언되지 않았더라도 이 라이브러리의 추적을 찾는 데 도움이 되는 Snyk CLI 명령입니다.

이 명령은 빌드된 프로젝트 및 타사 응용 프로그램을 테스트하며 `snyk test` 및 `snyk test --scan-all-unmanaged` 명령을 보완합니다.

\{% hint style="info" %\} [Snyk VulnDB ](https://security.snyk.io/vuln/SNYK-JAVA-ORGAPACHELOGGINGLOG4J-2314720)항목의 Log4Shell 취약성에 대해 자세히 알아보십시오. \{% endhint %\}

패키지 관리자 매니페스트 파일을 사용하여 Java 프로젝트를 테스트하려면 [Snyk for java(Gradle, Maven)](https://github.com/snyk/user-docs/blob/5e52535b78618f57eda40eb08fc8fbf91e16f1f0/docs/products/snyk-open-source/language-and-package-manager-support/snyk-for-java-gradle-maven.md)를 참조하십시오. `snyk test --scan-all-unmanaged` 에 대한 자세한 내용은 [CLI reference의 메이븐 옵션 섹션](https://docs.snyk.io/snyk-cli/cli-reference#maven-options)을 참조하십시오.

### 사용법

`synk log4shell` 을 사용하여 Java 프로젝트를 스캔하고 프로젝트에 다음이 포함되어 있는지 확인합니다.

* 취약한 버전의 log4j가 있는 `.jar` 또는 `.war` 파일입니다.
* log4j 라이브러리의 취약한 버전에 있는 것으로 알려진 모든 파일. 이러한 결과는 전체 log4j가 포함될 수 있음을 나타냅니다.

### 실행 방법

1. 최신 버전의 Snyk CLI를 설치합니 - [Snyk CLI 설치](https://github.com/snyk/user-docs/tree/5e52535b78618f57eda40eb08fc8fbf91e16f1f0/docs/features/snyk-cli/install-the-snyk-cli)를 참조하십시오.
2. 프로젝트를 구축했는지 확인합니다.
3. 검색할 프로젝트 디렉토리로 이동합니다.
4. `snyk log4shell` 을 입력합니다.\
   **NOTE**: 이 명령에는 추가 인수가 필요하거나 지원되지 않습니다.

### 스캔 결과

스캔 완료 후 결과가 나타납니다.

예는 다음과 같습니다:

```
$ snyk log4shell
Please note this command is for already built artifacts. To test source code please use `snyk test`.

Results:
A vulnerable version of log4j was detected: 
         demo-0.0.1-SNAPSHOT/WEB-INF/lib/log4j-core-2.14.1.jar
         demo-0.0.1-SNAPSHOT.war/WEB-INF/lib/log4j-core-2.14.1.jar
         demo-0.0.1-SNAPSHOT.war.original/WEB-INF/lib/log4j-core-2.14.1.jar

 We highly recommend fixing this vulnerability. If it cannot be fixed by upgrading, see mitigation information here:
        - https://security.snyk.io/vuln/SNYK-JAVA-ORGAPACHELOGGINGLOG4J-2314720
        - https://snyk.io/blog/log4shell-remediation-cheat-sheet/
```

취약한 log4j 라이브러리의 흔적을 찾을 수 없는 경우 결과에 다음과 같이 표시됩니다.

```
$ snyk log4shell
Please note this command is for already built artifacts. To test source code please use `snyk test`.

Results:
No known vulnerable version of log4j was detected
```

### Fix advice

영향을 받는 패키지를 수정하는 방법에 대한 자세한 내용은  [Log4Shell fix cheatsheet](https://snyk.io/blog/log4shell-remediation-cheat-sheet)를 참조하십시오.

### 제한 사항

* Snyk CLI는 파일 서명을 알려진 파일의 데이터베이스와 비교합니다. Log4Shell 취약성이 log4j 라이브러리 업데이트와 다른 방식으로 해결된 경우에도 라이브러리는 결과에 계속 보고됩니다.
* log4j 라이브러리의 소스 코드가 수정된 경우 해당 코드가 감지됩니다.
