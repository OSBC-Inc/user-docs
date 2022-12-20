# 프로젝트 디펜던시 트리 검토

## 디펜던시 트리 보기

Snyk은 애플리케이션의 패키지 매니저를 사용하여 디펜던시 트리를 빌드하고 Snyk UI에 표시합니다. 디펜던시 트리는 취약점을 도입하는 컴포넌트를 시각화하고 Snyk이 적절한 수정 조언을 결정하는 데 도움이 됩니다.

샘플 애플리케이션에서 직접 의존성 **org.springframework.boot:spring-boot-starter-web@2.3.1.RELEASE**를 조사함으로써 간접 의존성이 어떻게 애플리케이션에 취약점을 도입했는지 확인합니다. 개발자는 pom.xml 파일을 통해 이 라이브러리를 소스코드에 직접 포함했으며 **org.springframework.boot:spring-boot-starter-web@2.3.1.RELEASE** 라이브러리는 다른 의존성 **org.apache.tomcat.embed:tomcat-embed-core@9.0.36**을 갖는 **org.springframework.boot:spring-boot-starter-tomcat@2.3.1.RELEASE**에 의존성을 가지고 있습니다. 이를 통해 애플리케이션에 의존성이 도입된 방법과 Snyk이 Issue를 해결할 수 있는 방법을 이해하는 데 도움이 됩니다.

{% hint style="info" %}
**org.apache.tomcat.embed:tomcat-embed-core@9.0.36** 라이브러리는 간접 의존성으로 인해 여러 번 포함됩니다.
{% endhint %}

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/screen-shot-2020-08-21-at-4.49.51-pm.png)
