# Snyk for Scala

Snyk은 디펜던시를 [sbt](https://www.scala-sbt.org)에서 관리하는 Scala 프로젝트 테스트를 Snyk CLI와 UI를 통해 지원합니다.

{% hint style="info" %}
**Note**\
sbt 1.2 이하 버전에서 Snyk CLI를 사용하면 먼저 [install the sbt-dependency-graph plugin](https://support.snyk.io/hc/en-us/articles/360004167317)을 진행해야 합니다.
{% endhint %}

## Scala 프로젝트 테스트 : 작동 방식

build.sbt를 검사하여 Scala 프로젝트를 스캔하여 프로젝트의 모든 직접적이고 깊은 디펜던시의 특정 버전을 [Maven vulnerability database](https://snyk.io/vuln?type=maven)와 비교합니다.
