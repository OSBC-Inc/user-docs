# 연습 - 테스트

`Containerize Application` 랩에서 애플리케이션을 빌드하는 방법을 보았습니다. 이 연습에서는 보안 취약점이 발견되어 실패할 빌드를 실행하려고 합니다. 일반적으로 코드 개발 단계에서 수행되지만 취약성을 수정한 다음 연습을 다시 실행하여 빌드가 성공하는지 확인하는 프로세스를 안내합니다.

변경 사항을 저장:

```
git commit -am "snyk"
```

_Push_:

```
git push -f codecommit master
```

이제 CodeBuild에서 **build history**를 살펴봅니다. 새 스캔이 실행되는 데 1\~2분 정도 걸릴 수 있습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk\_4\_build.png)

이것이 실패한 이유를 살펴보겠습니다. 보안 취약점이 발견되고 **해결 방법**을 알려드립니다!

```
Testing /usr/src/app...
✗ Medium severity vulnerability found in org.primefaces:primefaces
Description: Cross-site Scripting (XSS)
Info: https://snyk.io/vuln/SNYK-JAVA-ORGPRIMEFACES-31642
Introduced through: org.primefaces:primefaces@6.1
From: org.primefaces:primefaces@6.1
Remediation:
Upgrade direct dependency org.primefaces:primefaces@6.1 to org.primefaces:primefaces@6.2 (triggers upgrades to org.primefaces:primefaces@6.2)
✗ Medium severity vulnerability found in org.primefaces:primefaces
Description: Cross-site Scripting (XSS)
Info: https://snyk.io/vuln/SNYK-JAVA-ORGPRIMEFACES-31643
Introduced through: org.primefaces:primefaces@6.1
From: org.primefaces:primefaces@6.1
Remediation:
Upgrade direct dependency org.primefaces:primefaces@6.1 to org.primefaces:primefaces@6.2 (triggers upgrades to org.primefaces:primefaces@6.2)
Organisation: sample-integrations
Package manager: maven
Target file: pom.xml
Open source: no
Project path: /usr/src/app
Tested 37 dependencies for known vulnerabilities, found 2 vulnerabilities, 2 vulnerable paths.
The command '/bin/sh -c ./snyk test' returned a non-zero code: 1
[Container] 2018/11/09 03:46:22 Command did not exit successfully docker build --build-arg snyk_auth_token=$SNYK_AUTH_TOKEN -t $REPOSITORY_URI:latest . exit status 1
[Container] 2018/11/09 03:46:22 Phase complete: BUILD Success: false
[Container] 2018/11/09 03:46:22 Phase context status code: COMMAND_EXECUTION_ERROR Message: Error while executing command: docker build --build-arg snyk_auth_token=$SNYK_AUTH_TOKEN -t $REPOSITORY_URI:latest .. Reason: exit status 1
```
