# Snyk 사용자 가이드

{% hint style="danger" %}
Log4Shell 취약점([CVE-2021-44228](https://security.snyk.io/vuln/SNYK-JAVA-ORGAPACHELOGGINGLOG4J-2314720))이 공개되었습니다. 최신 버전으로 업데이트하여 Log4j RCE를 방지합니다.\
[**더 보기**](https://snyk.io/blog/log4j-rce-log4shell-vulnerability-cve-2021-4428/)
{% endhint %}

### **Snyk**이란?~~(수정필요)!~~

Snyk 개발 도구 및 자동화 파이프라인에 직접 통합되어 코드, 종속성, 컨테이너 및 인프라의 보안 취약점을 쉽게 찾고 우선 순위를 정하며 수정할 수 있습니다. 업계 최고의 취약점 인텔리전스를 기반으로 개발자가 설계한 Snyk은 툴킷에 보안 전문 지식을 담을 수 있도록 개발 프로세스 적합합니다.

### Snyk은 어떤 제품을 제공하나요?

* [Snyk Open Source](https://snyk.io/product/open-source-security-management/): 오픈 소스 취약점 검색 및 자동 수정
* [Snyk Code](https://snyk.io/product/snyk-code/): 응용프로그램 코드에서 실시간 취약점 찾기
* [Snyk Container](https://snyk.io/product/container-vulnerability-management/): 컨테이너 이미지 및 Kubernetes 워크로드의 취약점 찾기 및 수정
* [Snyk Infrastructure as Code (IaC)](https://snyk.io/product/infrastructure-as-code-security/): Terraform, CloudFormation, Kubernetes 및 Azure 템플릿에서 잘못된 구성을 찾아 수정

### **What does it cost?**

Snyk은 여러 가지 [요금제](https://snyk.io/plans/) 중 선택할 수 있습니다:

* **Free**: For individual developers and small teams looking to secure while they build. Limited tests.
* **Team**: For dev teams looking to build security into their development process with shared visibility into projects. Unlimited tests.
* **Business**: Empower developers across an organization and provide reporting and advanced controls to manage teams and control to shift security left. Unlimited tests.
* **Enterprise**: Standardize dev-first security across the enterprise, with centralized policy governance. Unlimited tests.

### 누가 Snyk을 사용하나요?

Google, Salesforce, Datadog, Atlassian, Twilio, Revolut 등 많은 업체들은 자사의 코드를 보호하고 취약점을 모니터링하기 위해 Snyk를 사용하고 있습니다.

### 어떻게 Snyk을 사용하나요?

1. [회원가입](https://snyk.io/login?cta=sign-up\&loc=nav\&page=support\_docs\_page) 후 자신의 프로젝트에 연결합니다.
2. 프로젝트에 대해 테스트를 실행합니다.
3. 결과를 검토하여 취약점을 식별합니다.
4. Pull Requests를 통해 이러한 취약점을 수정합니다.
5. 모니터링을 통해 보안을 유지합니다.

자세한 내용은 [Getting started guides](https://docs.snyk.io/getting-started)를 참조하십시오.

{% hint style="success" %}
[무료로 Snyk을 사용하려면 회가입하세요!](https://snyk.io/login?cta=sign-up\&loc=nav\&page=support\_docs\_page)
{% endhint %}

{% hint style="info" %}
Snyk 데이터 처리에 대한 자세한 내용은 [Snyk 데이터 처리 방법](more-info/how-snyk-handles-your-data.md)을 참조하십시오.
{% endhint %}

