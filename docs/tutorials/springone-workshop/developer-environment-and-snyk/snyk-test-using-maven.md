# Snyk test using Maven

## Snyk Maven 플러그인을 사용하여 SPC 테스트

Snyk CLI를 사용하면 개발자가 CLI를 사용하여 애플리케이션을 테스트하고 모니터링할 수 있습니다. 개발자들이 Snyk이 일상적인 빌드의 일부가 되기를 원한다면 Snyk Maven 플러그인을 사용할 수 있습니다. 아래 단계는 Snyk 플러그인을 실행하도록 Maven을 구성하는 방법을 보여줍니다. 로컬 배포에서 실행되도록 구성합니다.

SPC 애플리케이션의 루트 디렉터리에서 다음을 실행합니다.

```
vi pom.xml
```

플러그인 섹션에서 이전에 생성한 Snyk 조직과 일치하도록 이름을 찾아 변경합니다. 다음 단계에서 maven 명령줄을 통해 SNYK\_TOKEN을 전달합니다.

{% hint style="info" %}
Snyk에서 조직 이름을 찾으려면 다음 단계를 참조하십시오.
{% endhint %}

```
<plugin>
  <groupId>io.snyk</groupId>
  <artifactId>snyk-maven-plugin</artifactId>
  <version>1.2.6</version>
  <executions>
    <execution>
      <id>snyk-test</id>
      <phase>test</phase>
      <goals>
        <goal>test</goal>
      </goals>
    </execution>
    <execution>
      <id>snyk-monitor</id>
      <phase>install</phase>
      <goals>
        <goal>monitor</goal>
      </goals>
    </execution>
  </executions>
  <configuration>
    <apiToken>${SNYK_TOKEN}</apiToken>
    <failOnSeverity>false</failOnSeverity>
    <!-- Replace with your Org name -->
    <org>springone-workshop</org>
  </configuration>
</plugin>
```

설정에서 조직 이름을 검색할 수 있습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/getting\_org\_name.png)

## Maven을 실행하여 결과 보기

pom.xml 파일을 구성한 후 Snyk test를 실행하면 결과를 볼 준비가 된 것입니다. 개인 API 토큰으로 아래 명령을 실행하십시오.

```
mvn snyk:test -DSNYK_TOKEN=add_your_personal_token
```

{% hint style="info" %}
인증 중에 개인 API 토큰을 검색했습니다.
{% endhint %}

Snyk test 결과는 아래 출력과 유사한 색상으로 구분된 취약점 정보를 표시합니다. Snyk 플러그인은 각 취약점 및 관련 심각도 수준에 대한 세부 정보를 제공합니다. 개발자는 심각도 수준에 따라 빌드를 실패하거나 빌드를 통과하도록 선택할 수 있습니다.

```
Downloading from central: https://repo.maven.apache.org/maven2/org/apache/logging/log4j/log4j-api-java9/2.13.3/log4j-api-java9-2.13.3.pom
[WARNING] The POM for org.apache.logging.log4j:log4j-api-java9:zip:2.13.3 is missing, no dependency information available
[WARNING] ✗ medium severity vulnerability found on com.google.guava:guava@18.0
[WARNING] - desc: Deserialization of Untrusted Data
[WARNING] - info: https://snyk.io/vuln/SNYK-JAVA-COMGOOGLEGUAVA-32236
[WARNING] - from: org.springframework.samples:spring-petclinic@2.3.1.BUILD-SNAPSHOT > org.springframework.boot:spring-boot-starter-data-jpa@2.3.1.RELEASE > org.springframework.data:spring-data-jpa@2.3.1.RELEASE > com.querydsl:querydsl-apt@4.3.1 > com.querydsl:querydsl-codegen@4.3.1 > com.querydsl:querydsl-core@4.3.1 > com.google.guava:guava@18.0
[WARNING]
[WARNING] ✗ high severity vulnerability found on log4j:log4j@1.2.16
[WARNING] - desc: Deserialization of Untrusted Data
[WARNING] - info: https://snyk.io/vuln/SNYK-JAVA-LOG4J-572732
[WARNING] - from: org.springframework.samples:spring-petclinic@2.3.1.BUILD-SNAPSHOT > org.springframework.boot:spring-boot-starter-data-jpa@2.3.1.RELEASE > org.hibernate:hibernate-core@5.4.17.Final > org.jboss.logging:jboss-logging@3.4.1.Final > log4j:log4j@1.2.16
[WARNING]
[WARNING] ✗ medium severity vulnerability found on org.apache.tomcat.embed:tomcat-embed-core@9.0.36
[WARNING] - desc: Denial of Service (DoS)
[WARNING] - info: https://snyk.io/vuln/SNYK-JAVA-ORGAPACHETOMCATEMBED-584427
[WARNING] - from: org.springframework.samples:spring-petclinic@2.3.1.BUILD-SNAPSHOT > org.springframework.boot:spring-boot-starter-web@2.3.1.RELEASE > org.springframework.boot:spring-boot-starter-tomcat@2.3.1.RELEASE > org.apache.tomcat.embed:tomcat-embed-core@9.0.36
[WARNING]
[WARNING] ✗ high severity vulnerability found on org.hibernate:hibernate-core@5.4.17.Final
[WARNING] - desc: SQL Injection
[WARNING] - info: https://snyk.io/vuln/SNYK-JAVA-ORGHIBERNATE-584563
[WARNING] - from: org.springframework.samples:spring-petclinic@2.3.1.BUILD-SNAPSHOT > org.springframework.boot:spring-boot-starter-data-jpa@2.3.1.RELEASE > org.hibernate:hibernate-core@5.4.17.Final
```

{% hint style="info" %}
Snyk URL에 문제가 있는 경우 조직 또는 API 토큰이 올바르지 않을 것입니다.
{% endhint %}

{% hint style="info" %}
이 빌드를 완료하는 데 약 45초가 걸립니다.
{% endhint %}
