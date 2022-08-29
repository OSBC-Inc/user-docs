# Log4shell

## 사용법

`snyk log4shell`

## 설명

snyk log4shell 명령은 Log4Shell 취약점 [CVE-2021-44228](https://security.snyk.io/vuln/SNYK-JAVA-ORGAPACHELOGGINGLOG4J-2314720)의 영향을 받는 Log4J 라이브러리의 흔적을 찾습니다.

이 명령은 매니페스트 파일(예: pom.xml 또는 build.gradle)에 선언되지 않은 경우에도 Log4J 라이브러리의 추적을 찾습니다.

## 관리되는 프로젝트

패키지 관리자 매니페스트 파일을 사용하여 Java 프로젝트의 Log4Shell 취약성을 테스트하려면 `snyk test` command를 사용하십시오. [테스트 command 도움말](test.md)(`snyk test --help`) 및 [Java 및 Kotlin용 Snyk](../../../snyk-products/snyk-open-source/language-and-package-manager-support/snyk-for-java-gradle-maven.md)을 참조하세요.

관리되지 않는 파일을 테스트하려면 `snyk test --scan-all-unmanaged`를 사용하십시오.

&#x20;[테스트 command 도움말](test.md)의 Maven 옵션 섹션을 참조하십시오.; `snyk test --help`

## 종료 코드

사용 가능한 종료 코드 및 그 의미:

**0**: 성공, Log4Shell을 찾을 수 없음\
**1**: action\_needed, Log4Shell을 찾음\
**2**: 실패, command 다시 실행하십시오.

## Debug

`-d` 옵션을 사용하여 디버그 로그를 출력합니다.
