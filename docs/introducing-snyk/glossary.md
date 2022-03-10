# 용어 사전

## A

### Advisor

[Snyk Advisor](https://support.snyk.io/hc/en-us/articles/360017682058-Snyk-Glossary#SnykAdvisor)를 참조하십시오.

## B

### Base image

컨테이너 이미지를 구성하는 데 사용되는 상위 이미지이며, 일반적으로 Dockerfile의 FROM 지시문에 정의됩니다. base image는 다른 base image에서 구성할 수 있습니다.

### Broker

[Snyk Broker](https://docs.snyk.io/integrations/snyk-broker)를 참조하십시오.

### Build System

소스 코드를 가져와 배포 가능한 애플리케이션(예: 컨테이너)을 빌드하는 시스템입니다.

## C

### CI / CD

지속적 통합(CI), 지속적 배포(CD)가 함께 SDLC 모델을 구성하며 개발자가 작고 빈번한 변경 사항의 개발 및 배포를 자동화하도록 안내합니다. 이렇게 하면 모든 팀 구성원이 최신 소스 코드에 액세스할 수 있으며 개발 중에 커밋된 코드의 호환성을 보장할 수 있습니다.

### CLI

Command Line Interface. [Snyk CLI](glossary.md#snyk-cli)를 참조하십시오.

### Cloud Native Application Security

CI/CD 파이프라인 전체에 보안을 구현하고, 마이크로서비스에 내장된 보안을 자동화하고, 반복을 극대화하여 취약점 유입을 줄입니다. Snyk은 포괄적인 [CNAS platform](https://snyk.io/product/cloud-native-application-security/)을 제공합니다.

### Container

컨테이너를 사용하면 애플리케이션과 해당 디펜던시를 함께 패키징하여 단일 실행 가능한 단위로 배포할 수 있습니다. 컨테이너는 운영체제 커널이 제공하는 추상화이며, 시스템에서 실행 중인 다른 프로세스로부터 프로세스를 분리할 수 있습니다. [Snyk Container](https://support.snyk.io/hc/en-us/articles/360017682058-Snyk-Glossary#SnykContainer)를 참조하십시오.

### Container engine

사용자의 경우 컨테이너 이미지를 가져와 실행 중인 컨테이너로 바꾸는 애플리케이션입니다. 컨테이너 엔진은 일반적으로 컨테이너 레지스트리와 연결되며 컨테이너를 실행합니다. 컨테이너 엔진의 예로는 Docker, CRI-O 또는 LXC가 있습니다.

### Container image

컨테이너 엔진 또는 런타임에 의해 인스턴스화된 경우 실행 중인 컨테이너를 제공하는 하나 이상의 파일입니다. 이미지는 컨테이너의 패키징 및 배포 형식입니다.

### Container registry

컨테이너 이미지를 저장하고 검색할 수 있는 메커니즘을 제공하는 서버입니다.

### CVE

Common Vulnerabilities and Exposures의 약자로, 잘 알려진 취약점에 대해 널리 사용되는 식별자입니다.

### CVSS

Common Vulnerability Scoring System의 약자로, 0점(가장 낮음)에서 10점(가장 높음) 사이의 점수를 사용하여 취약성의 심각도를 평가하는 업계 표준입니다. Snyk는 CVSS를 사용합니다.

### CWE

Common Weakness Enumeration의 약자로, 소프트웨어 및 하드웨어의 약점을 다양한 유형으로 분류하는 용어집입니다. 예: **CWE-20: Input Validation**.

## D

### DAST

동적 응용 프로그램 보안 테스트(Dynamic Application Security Testing)를 말합니다. 사이트 또는 서비스를 가리킬 수 있는 애플리케이션입니다. 그런 다음 일반적으로 사이트 또는 서비스를 성능 분석한 다음 출력 및 동작을 검사하여 보안 취약점을 파악합니다. 또한 [SAST](glossary.md#sast)를 참조하십시오.

### Dependency

응용 프로그램에서 다른 패키지를 사용하면 이 다른 패키지가 사용자 소프트웨어에 종속됩니다.

* direct dependency는 사용자가 자신의 프로젝트에 포함하는 패키지입니다.
* indirect dependency(deep, chained 또는transitive dependency라고도 함)는 직접 종속성 중 하나에 사용되는 패키지입니다.

### Dependency tree\~\~(수정 필요?=직접종속성, 간접종속성이란 말 원래쓰는건지?)\~\~

종속성 경로라고도 하며, 소프트웨어 응용 프로그램의 종속성을 보여주는 계층적 그래프이다. 여기에는 직접적, 간접적 의존성이 모두 포함되며, 많은 수준의 의존성이 포함될 수 있다.

### DevOps

A set of cultural philosophies, practices, and tools that combines software development and IT operations, to shorten the systems development life cycle.

### DevSecOps

The integration of security into emerging agile IT and DevOps development as seamlessly and as transparently as possible.

### Dockerfile

도커를 사용하여 컨테이너 이미지를 작성하는 데 사용되는 텍스트 파일 형식입니다. 도커 파일에는 상위 기본 이미지 지정을 포함하여 최종 이미지를 생성하는 데 필요한 모든 명령이 포함되어 있습니다.

## E

### Exploit

취약성이 어떻게 활용될 수 있는지 보여주는 것입니다. When an exploit is widely published, it is commonly referred to as an exploit in the wild.

### Exploit Maturity

A measure of how practical an exploit for a vulnerability is, based on whether the exploit is in the wild, and how "helpful" the exploit is to attackers. [취약성 평가 및 우선 순위지정](https://docs.snyk.io/fixing-and-prioritizing-issues/issue-management/evaluating-and-prioritizing-vulnerabilities)을 참조하십시오.

## F

### Fixable / Partially fixable

A measure of whether a vulnerability can be fixed by Snyk, by applying a patch, upgrade, or pin. [Fixed in version vs. fixable attributes in vulnerabilities](https://support.snyk.io/hc/en-us/articles/4405034808209)을 참조하십시오.

### Fix PR

A pull request with an automatic fix for vulnerabilities found that Snyk can offer the user.

## G

### Git

소프트웨어 개발 중에 소스 코드의 변경 사항을 추적하기 위한 분산 버전 관리 시스템입니다.

## I

### IAC

Infrastructure as Code. [Snyk Infrastructure as Code](glossary.md) 참조하십시오.

### IAST

Interactive Application Security Testing. 이 접근 방식은 응용 프로그램을 실행하는 동안 취약성을 테스트합니다. **DAST** and **SAST**를 참조하십시오.

### IDE

통합 개발 환경(Integrated Development Environment)을 말합니다. 일반적으로 소스 코드 편집기, 빌드 자동화 도구 및 디버거와 함께 소프트웨어 개발을 위한 기능을 제공하는 응용 프로그램입니다.

### Image

The stored instance of a container that holds a set of software needed to run an application.

### Image layer

컨테이너 이미지는 일반적으로 여러 개의 서로 다른 파일 시스템 계층으로 구성되며 런타임에 단일 파일 시스템으로 결합됩니다.

### Integrations

Third-party products, applications and platforms that Snyk works with, for example SCM systems such as GitHub.

### Issue

Snyk에서 식별 및 나열한 라이센스 문제 또는 취약성입니다.

## L

### Library\~\~(수정필요)?\~\~

패키지의 특정 유형입니다.

## M

### Manifest

패키지의 파일들에 대한 메타데이터가 들어 있는 파일입니다.

### Monitor

**snyk monitor**는 프로젝트를 테스트하고 결과를 Snyk에 업로드하는 snyk의 명령어입니다.

## O

### OCI

Open Container Initiative의 약자로, An independent body set up to facilitate collaboration around standards for containers, to ensure they are interoperable between vendor solutions.

### Organization

An organization in Snyk is a way to collect and organize your projects. 그런 다음 구성원이 이러한 프로젝트에 액세스할 수 있습니다.

## P

### Package

패키지 매니저가 사용하는 파일 그룹 및 해당 파일에 대한 추가 메타데이터입니다.

### Package manager

패키지를 자동화하고 관리하는 도구 집합으로, 일반적으로 언어에 따라 다릅니다. (예: npm)

### Package registry

고객이 패키지와 코드를 한 곳에서 호스팅할 수 있는 소프트웨어 패키지 호스팅 서비스입니다.

### Pinnable

A fix type: define and "pin" a specific version of an indirect dependency, to avoid a direct dependency pulling in a vulnerable version.

### PR

Pull Request. 사용자가 소스 코드의 변경 사항을 반하고 동일한 branch 있는 다른 사용자와 협업할 수 있습니다.

### Priority Score

Snyk는 issues(취약점 및 라이선스)를 점수화하여 각각의 문제 해결의 우선순위를 정하는 데 도움이 됩니다. 점수는 CVSS 점수를 포함한 여러 요소를 기반으로 하며 0(낮음)에서 1000(높음) 사이의 범위를 가집니다. [Snyk Priority Score](https://docs.snyk.io/fixing-and-prioritizing-issues/starting-to-fix-vulnerabilities/snyk-priority-score) 참조하십시오.

### Project

An external item that Snyk scans, with configuration to define how to run that scan. Snyk 대시보드의 프로젝트 메뉴에 나타납니다. [프로젝트 소개](https://docs.snyk.io/getting-started/introduction-to-snyk-projects) 참조하십시오.

## R

### Reachability

실행 중 공격 가능한 취약한 경로의 코드가 응용 프로그램에 포함되어 있는지 여부입니다. [Reachable vulnerabilities](https://support.snyk.io/hc/en-us/articles/360010554837-Reachable-Vulnerabilities-) 참조하십시오.

### Registry

[Container registry](https://support.snyk.io/hc/en-us/articles/360017682058-Snyk-Glossary#ContainerRegistry) 또는 [Package registry](https://support.snyk.io/hc/en-us/articles/360017682058-Snyk-Glossary#PackageRegistry)를 참조하십시오.

### Repository

응용 프로그램 배포에 필요한 모든 요소를 포함하는 저장소 영역을 말합니다.

## S

### SARIF

정적 분석 결과 상호 교환 형식입니다. 정적 분석 도구의 출력을 위한 표준 JSON 기반 형식입니다.

### SAST

정적 응용 프로그램 보안 테스트(Static Application Security Testing)를 말합니다. 독점 소프트웨어의 소스 코드를 검토하고 취약점의 원인을 식별하여 소프트웨어를 보호하는 방법입니다. 또한 [DAST](glossary.md#ast) 참조하십시오.

### SBOM

Software Bill Of Materials. 소프트웨어의 구성 요소 목록입니다.

### SCA

Software Composition Analysis. Technology used to identify open-source and third-party components in use in an application, including their known security vulnerabilities, and typically adversarial license restrictions.

{% hint style="info" %}
정적 코드 분석(프로그램 실행 전에 소스 코드를 검사하여 디버깅하는 방법)과 혼동하지 마십시오.
{% endhint %}

### SCM

Source Code Management. Also known as a code repo / repository / version control system. 개발자가 소스 코드를 저장하고 코드의 변경 사항을 추적하기 위해 사용하는 방법입니다. SCM은 여러 기여자의 업데이트를 병합할 때 발생하는 충돌을 해결하는 데 도움이 됩니다. (예: GitHub)

### SDLC

소프트웨어 개발 수명 주기(Software Development Life Cycle)를 말합니다. A process followed by a development team, describing how to develop and, maintain software.

### Serverless

A method to provide pay-as-you-use backend computing services, allowing applications to be constructed entirely from functions provided by the supplier. Examples of serverless providers include AWS Lambda and Azure Functions.

### Severity

심각도 수준은 취약점 또는 라이선스 문제에 적용되어 응용 프로그램에서 해당 항목의 위험을 나타냅니다. [Severity levels](https://docs.snyk.io/introducing-snyk/snyks-core-concepts/severity-levels)을 참조하시오.

### Snapshot

An individual report within a project’s test history. Includes a tree of dependancies, and a list of vulnerabilities that was accurate at the time the test was conducted.

### Snyk

개발자가 코드 및 오픈 소스에서 컨테이너 및 클라우드 인프라에 이르기까지 전체 애플리케이션에 대한 보안을 소유 및 구축할 수 있는 CNAS(Cloud Native Application Security) 솔루션을 제공하는 플랫폼입니다. [What is Snyk?](https://snyk.io/what-is-snyk/)을 참조하시오.

Synk은 또한 Snyk 플랫폼을 제공하는 회사이다.

### Snyk Advisor

A free web application which allows you to compare software packages across open source ecosystems. It provides insights into the overall health of a particular package by combining community and security data into a single unified view. [Snyk Advisor](https://snyk.io/advisor/)을 참조하시오.

### Snyk API

개발자가 Snyk와 프로그래밍 방식으로 통합할 수 있도록 지원하는 Snyk 도구입니다. [Snyk API documentation](https://support.snyk.io/hc/en-us/categories/360000665657-Snyk-API)을 참조하시오.

### Snyk Broker

A client/server system that serves as an agent / proxy, allowing Snyk to scan private customer environments (Jira, code repositories or container registries). It relays messages and allows users to filter which messages are allowed through; for example, allowing users to expose only some Github APIs to Snyk. [Snyk Broker documentation](https://docs.snyk.io/integrations/snyk-broker) 참조하시오.

### Snyk CLI

Snyk 플랫폼 도구입니다. Snyk CLI를 사용하면 개발자가 CLI를 사용하여 종속성의 알려진 취약점을 찾아 수정할 수 있습니다. [Snyk CLI documentation](https://docs.snyk.io/snyk-cli)을 참조하시오.

### Snyk Code

Snyk의 제품 중 하나입니다. 개발자가 독점 응용프로그램 코드의 취약성을 찾아 수정할 수 있는 SAST 제품입니다. [Snyk Code documentation](https://docs.snyk.io/snyk-code)을 참조하시오.

### Snyk Container

Snyk의 제품 중 하나입니다. 개발자가 컨테이너 이미지 및 Kubernetes 응용프로그램에서 취약점을 찾아 수정할 수 있습니다. [Snyk Container documentation](https://docs.snyk.io/snyk-container)을 참조하십시오.

### Snyk Infrastructure as Code

Snyk의 제품 중 하나입니다. 개발자가 Kubernetes, Helm 및 Terraform 구성 파일의 취약점을 찾아 수정할 수 있습니다. [Snyk IaC documentation](https://docs.snyk.io/snyk-infrastructure-as-code)을 참조하시오.

### Snyk Open Source

Snyk의 제품 중 하나입니다. 개발자가 오픈 소스 취약성을 찾아 수정할 수 있습니다. [Snyk Open Source documentation](https://docs.snyk.io/snyk-open-source)을 참조하시오.

### Snyk plugin

Snyk CLI에서 특정 언어/빌드 시스템을 검색하는 데 사용하는 라이브러리입니다.

### Snyk Security Intelligence

A component powering Snyk’s cloud native application security platform.\
Incorporates **Snyk Intel Vulnerability DB**: Snyk의 취약성 데이터베이스를 통합하여 자세한 정보를 제공하고 알려진 취약성에 대한 조언을 제공합니다. [Vulnerability DB](https://snyk.io/vuln)를 참조하시오.

### Social Trends

Snyk는 트위터에서 활발하게 논의되고 있는 이슈에 대해 트렌딩 배너를 보여줍니다. [Prioritizing Social Trends](https://docs.snyk.io/fixing-and-prioritizing-issues/prioritizing-issues/prioritize-by-social-trends) 기사를 참조하시오.

### SPDX

Software Package Data Exchange. 소프트웨어가 배포되는 소프트웨어 라이센스에 대한 정보를 문서화하는 데 사용되는 파일 형식입니다.

## U

### Upgradable / Patchable

패키지 버전을 업그레이드하거나 패치를 적용하여 문제를 해결할 수 있습니다.

## V

### Vulnerability

Snyk가 식별한 보안 취약입니다. [취약점 수정](https://docs.snyk.io/fixing-and-prioritizing-issues/issue-management/remediate-your-vulnerabilities)를 참조하시오.

## W

### Webhook

프로그램이 다른 응용 프로그램에 실시간 정보를 제공하는 방법입니다. Snyk는 웹훅을 사용하여 코드의 변화를 확인합니다.
