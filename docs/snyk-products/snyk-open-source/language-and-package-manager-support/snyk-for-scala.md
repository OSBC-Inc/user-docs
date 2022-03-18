# Scala용 Snyk

Snyk은 디펜던시를 [sbt](https://www.scala-sbt.org)에서 관리하는 Scala 프로젝트 테스트를 Snyk CLI와 UI를 통해 지원합니다.

{% hint style="info" %}
**Note**\
sbt 1.2 이하 버전에서 Snyk CLI를 사용하면 먼저 [sbt-dependency-graph 플러그인 설치](https://support.snyk.io/hc/en-us/articles/360004167317)를 진행해야 합니다.
{% endhint %}

## Scala 프로젝트 테스트 : 작동 방식

build.sbt를 검사하고 Scala 프로젝트를 스캔하여 프로젝트의 모든 직접적이고 deep한 디펜던시의 특정 버전을 [Maven 취약점 데이터베이스](https://security.snyk.io/?type=maven)와 비교합니다.
