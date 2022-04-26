# Snyk 소개

Snyk은 [자체코드](broken-reference), [오픈소스 디펜던시](broken-reference), [컨테이너 이미지](broken-reference), [IaC(Infrastructure as Code) 구성](broken-reference)의 취약점을 테스트하고 ~~_컨텍스트(?)_~~, 우선순위 지정 및 수정을 제공합니다.

### Snyk 제품

* [Snyk Open Source](https://docs.snyk.io/snyk-open-source): 개발자가 오픈소스 취약점을 쉽게 찾고 자동으로 수정할 수 있도록 합니다. Snyk Open Source에는 오픈소스 라이선스 사용을 관리하는 데 도움이 되는 [Snyk 라이선스 컴플라이언스](broken-reference)가 포함되어 있습니다.
* [Snyk Code](https://snyk.io/product/snyk-code/): 개발 프로세스 중에 애플리케이션 코드의 취약점을 실시간으로 찾아 수정합니다.
* [Snyk Container](https://docs.snyk.io/snyk-container): 컨테이너 이미지 및 Kubernetes 애플리케이션의 취약점을 찾아 수정합니다.
* [Snyk IaC(Infrastructure as Code)](https://docs.snyk.io/snyk-infrastructure-as-code): Terraform 및 Kubernetes 코드에서 안전하지 않은 구성을 찾아 수정합니다.

### 지원되는 언어

Snyk은 Java, JavaScript, .NET, Python, Golang, Swift, Objective-C, Ruby, Scala, PHP and Elixir 등 다양한 언어를 지원한다.

지원되는 언어/OS는 관련 Snyk 제품에 따라 다릅니다.

### 지원되는 통합

개발자 우선 보안 방식을 채택한 Snyk은 최고의 IDE, 저장소, CI/CD, 런타임, 레지스트리 및 이슈 관리 툴과 통합됩니다.

소프트웨어 개발 프로세스를 위한 [Snyk 통합](https://docs.snyk.io/integrations)에는 다음이 포함됩니다.

* **소스코드 관리:** 클라우드 및 Github와 같은 자체 호스팅 SCM. [Git 저장소(SCM) 통합](../features/integrations/git-repository-scm-integrations/)을 참조하십시오.
* **컨테이너 레지스트리 및 Kubernetes:** Docker Hub 및 Kubernetes와 같은 컨테이너 레지스트리. [Snyk Container](https://docs.snyk.io/snyk-container)를 참조하십시오.
* **CI(Continuous integration)**: Jenkins 및 TeamCity와 같은 CI 도구. [CI/CD 통합](https://docs.snyk.io/integrations/ci-cd-integrations)을 참조하십시오.
* **IDE 플러그인:** Eclipse와 같은 IDE 도구. [IDE 도구](https://docs.snyk.io/integrations/ide-tools)를 참조하십시오.
* **Artifact repositories:** 예를 들어 Artifactory. [비공개 레지스트리 게이트키퍼 플러그인](https://docs.snyk.io/integrations/private-registry-gatekeeper-plugins) 및 [비공개 레지스트리 통합](https://docs.snyk.io/integrations/private-registry-integrations)을 참조하십시오.
* **Serverless**: 예를 들어 AWS Lambda. [Serverless 통합](https://docs.snyk.io/integrations/serverless-integrations)을 참조하십시오.
* **Platform as a service:** 예를 들어 Heroku. [Platform as a service 통합](https://docs.snyk.io/integrations/platform-as-a-service-integrations)을 참조하십시오.
* **알림**: 예를 들어 Slack. [알림 및 티켓팅 시스템 통합](https://docs.snyk.io/integrations/notifications-ticketing-system-integrations)을 참조하십시오.
* **취약점 도구:** 예를 들어 RiskSense. [취약점 관리 도구](../features/integrations/vulnerability-management-tools/)를 참조하십시오.

### Snyk CLI

Snyk CLI를 사용하여 로컬 시스템에서 스캔 및 모니터링을 진행하고 이를 파이프라인에 통합할 수 있습니다. Snyk CLI를 사용하여 애플리케이션, 컨테이너 및 인프라 구성에 대한 보안 취약점을 스캔할 수 있습니다. npm, Homebrew, Scoop을 이용하거나 수동으로 설치할 수 있습니다.

[Snyk CLI 시작하기](broken-reference)

### Snyk API

Snyk의 확장성과 API를 통해 개발자는 Snyk의 보안 자동화를 특정 워크플로우에 맞게 조정할 수 있어 일관된 플랫폼 거버넌스를 보장할 수 있습니다.

[Snyk API 문서](https://support.snyk.io/hc/en-us/articles/360000914857-Does-Snyk-have-an-API-)에서 자세하게 확인이 가능합니다. [Twilio 및 Spotify](https://snyk.io/blog/snyk-watcher-keep-snyk-in-sync/)에서 Snyk API를 사용하는 방법을 확인하십시오.
