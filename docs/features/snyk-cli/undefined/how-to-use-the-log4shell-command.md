# log4shell command 사용 방법

### 소개

`snyk log4shell` 은 **log4Shell** 취약성([CVE-2021-44228](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-44228))의 영향을 받는 **log4j** 라이브러리가 매니페스트 파일(예: pom.xml 또는 build.gradle)에 선언되지 않았더라도 이 라이브러리의 추적을 찾는 데 도움이 되는 Snyk CLI command입니다.

이 command는 빌드된 프로젝트 및 타사 응용 프로그램을 테스트하며 `snyk test` 및 `snyk test --scan-all-unmanaged` command 보완합니다.

\{% hint style="info" %\} [Snyk VulnDB ](https://security.snyk.io/vuln/SNYK-JAVA-ORGAPACHELOGGINGLOG4J-2314720)항목의 Log4Shell 취약성에 대해 자세히 알아보십시오. \{% endhint %\}

패키지 관리자 매니페스트 파일을 사용하여 Java 프로젝트를 테스트하려면 [Snyk for java(Gradle, Maven)](https://github.com/snyk/user-docs/blob/5e52535b78618f57eda40eb08fc8fbf91e16f1f0/docs/products/snyk-open-source/language-and-package-manager-support/snyk-for-java-gradle-maven.md)를 참조하십시오. `snyk test --scan-all-unmanaged` 에 대한 자세한 내용은 [CLI reference의 메이븐 옵션 섹션](https://docs.snyk.io/snyk-cli/cli-reference#maven-options)을 참조하십시오.

### 사용법

`synk log4shell` 을 사용하여 Java 프로젝트를 스캔하고 프로젝트에 다음이 포함되어 있는지 확인합니다.

* 취약한 버전의 log4j가 있는 `.jar` 또는 `.war` 파일입니다.
* log4j 라이브러리의 취약한 버전에 있는 것으로 알려진 모든 파일. 이러한 결과는 전체 log4j가 포함될 수 있음을 나타냅니다.

### 실행 방법

1. Install the latest version of the Snyk CLI - see [Install the Snyk CLI](https://github.com/snyk/user-docs/blob/5e52535b78618f57eda40eb08fc8fbf91e16f1f0/docs/features/snyk-cli/install-the-snyk-cli).
2. Make sure you have built the project.
3. Navigate to the project directory to scan.
4. Enter `snyk log4shell`.\
   **Note**: this command does not require (nor support) any additional arguments.

### 스캔 결과

Results appear after the scan finishes.

For example:

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

If no traces of a vulnerable log4j library are found, the results show this:

```
$ snyk log4shell
Please note this command is for already built artifacts. To test source code please use `snyk test`.

Results:
No known vulnerable version of log4j was detected
```

### Fix advice

For more details about fixing the affected packages, see the Snyk [Log4Shell fix cheatsheet](https://snyk.io/blog/log4shell-remediation-cheat-sheet).

### 제한 사항

* The Snyk CLI compares file signatures to a database of known files. If the Log4Shell vulnerability is fixed in a different way from updating the log4j library, the library is still reported in the results.
* If the source code of the log4j library has been modified, it is detected.
