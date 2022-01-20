# 용어 사전

## A

### Advisor

[Snyk Advisor](https://support.snyk.io/hc/en-us/articles/360017682058-Snyk-Glossary#SnykAdvisor)를 참조하십시오.

## B

### Base image

컨테이너 이미지를 구성하는 데 사용되는 상위 이미지이며, 일반적으로 도커 파일의 FROM 지시문에 정의됩니다. Base images는 다른 base images에서 구성할 수 있습니다.

### Broker

[Snyk Broker](https://docs.snyk.io/integrations/snyk-broker)를 참조하십시오.

### Build System

소스 코드를 가져와 배포 가능한 애플리케이션(예: 컨테이너)을 구축하는 시스템입니다.

## C

### CI / CD

지속적 통합(CI), 지속적 배포(CD)가 함께 SDLC 모델을 구성하며 개발자가 작고 빈번한 변경 사항의 개발 및 배포를 자동화하도록 안내합니다. 이렇게 하면 모든 팀 구성원이 최신 소스 코드에 액세스할 수 있으며 개발 중에 커밋된 코드의 호환성을 보장할 수 있습니다.

### CLI

Command Line Interface. [Snyk CLI](glossary.md#snyk-cli)를 참조하십시오.

### Cloud Native Application Security ~~(\*수정 필요)~~&#x20;

CI/CD 파이프라인 전체에 보안을 구현하고, 마이크로 서비스에 내장된 보안을 자동화하고, 반복을 극대화하여 취약점 유입을 줄입니다. Snyk는 포괄적인 [CNAS platform](https://snyk.io/product/cloud-native-application-security/)을 제공합니다.

### Container

Containers allow you to package applications and their dependencies together, to be deployed as a single runnable unit. A container is an abstraction provided by the operating system kernel, that allows a process to be isolated from other processes running on the system. [Snyk Container](https://support.snyk.io/hc/en-us/articles/360017682058-Snyk-Glossary#SnykContainer)를 참조하십시오.

### Container engine

For users, an application which takes a container image and turns it into a running container. Container engines typically interface with container registries, and run containers. Examples of container engines include Docker, CRI-O or LXC.

### Container image

One or more files which, when instantiated by a container engine or runtime, provide a running container. Images are the packaging and distribution format for containers.

### Container registry

컨테이너 이미지를 저장하고 검색할 수 있는 메커니즘을 제공하는 서버입니다.

### CVE

Common Vulnerabilities and Exposures의 약자이며 잘 알려진 취약성에 대해 널리 사용되는 식별자입니다.

### CVSS

Common Vulnerability Scoring System의 약자이며 0점에서 10점 사이의 점수를 사용하여 취약성의 심각도를 평가하는 업계 표준입니다. Snyk는 CVSS를 사용합니다.

### CWE

Common Weakness Enumeration의 약자이며 an online glossary that categorizes software and hardware weaknesses into different types. 예: **CWE-20: Input Validation**.

## D

### DAST

동적 응용 프로그램 보안 테스트(Dynamic Application Security Testing)를 말합니다. An application that you can point at a site or service; it then typically profiles the site or service, then examines the output and behaviour to uncover security vulnerabilities. 또한 [SAST](glossary.md#sast)를 참조하십시오.

### Dependency

응용 프로그램에서 다른 패키지를 사용하면 이 다른 패키지가 사용자 소프트웨어에 종속됩니다.

* direct dependency는 사용자가 자신의 프로젝트에 포함하는 패키지입니다.
* indirect dependency(deep, chained 또는transitive dependency라고도 함)는 직접 종속성 중 하나에 사용되는 패키지입니다.

### Dependency tree~~(수정 필요?=직접종속성, 간접종속성이란 말 원래쓰는건지?)~~

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

A measure of whether a vulnerability can be fixed by Snyk, by applying a patch, upgrade, or pin.  [Fixed in version vs. fixable attributes in vulnerabilities](https://support.snyk.io/hc/en-us/articles/4405034808209)을 참조하십시오.

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

### Library~~(수정필요)?~~&#x20;

패키지의 특정 유형입니다.

## M

### Manifest

패키지의 파일들에 대한 메타데이터가 들어 있는 파일입니다.

### Monitor

**snyk monitor**는 프로젝트를 테스트하고 결과를 Snyk에 업로드하는 snyk의 명령어입니다.

## O

### OCI

Open Container Initiative의 약자이며 An independent body set up to facilitate collaboration around standards for containers, to ensure they are interoperable between vendor solutions.

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

Snyk scores issues (vulnerabilities and licenses), to help prioritze treatment of each one. Scores are based on multiple factors including as the CVSS score, and range from 0 (low) to 1000 (high). [Snyk Priority Score](https://docs.snyk.io/fixing-and-prioritizing-issues/starting-to-fix-vulnerabilities/snyk-priority-score) 참조하십시오.

### Project

An external item that Snyk scans, with configuration to define how to run that scan. Snyk 대시보드의 프로젝트 메뉴에 나타납니다. [프로젝트 소개](https://docs.snyk.io/getting-started/introduction-to-snyk-projects) 참조하십시오.

## R

### Reachability

실행 중 공격 가능한 취약한 경로의 코드가 응용 프로그램에 포함되어 있는지 여부입니다. [Reachable vulnerabilities](https://support.snyk.io/hc/en-us/articles/360010554837-Reachable-Vulnerabilities-) 참조하십시오.

### Registry

[Container registry](https://support.snyk.io/hc/en-us/articles/360017682058-Snyk-Glossary#ContainerRegistry) 또 [Package registry](https://support.snyk.io/hc/en-us/articles/360017682058-Snyk-Glossary#PackageRegistry)를 참조하십시오.

### Repository

응용 프로그램 배포에 필요한 모든 요소를 포함하는 저장소 영역을 말합니다.

## S

### SARIF

정적 분석 결과 상호 교환 형식입니다. 정적 분석 도구의 출력을 위한 표준 JSON 기반 형식입니다.

### SAST

정적 응용 프로그램 보안 테스트(Static Application Security Testing). A method to secure software by reviewing the source code of your proprietary software, and identifying sources of vulnerabilities. 또한 [DAST](glossary.md#ast) 참조하십시오.

### SBOM

Software Bill Of Materials. A list of components in a piece of software.

### SCA

Software Composition Analysis. Technology used to identify open-source and third-party components in use in an application, including their known security vulnerabilities, and typically adversarial license restrictions.

{% hint style="info" %}
Not to be confused with static code analysis (a method of debugging by examining source code before a program is run).
{% endhint %}

### SCM

Source Code Management. Also known as a code repo / repository / version control system. The method used by developers to store their source code, and track changes to code. SCM helps resolve conflicts when merging updates from multiple contributors. GitHub is an example of a common SCM system.

### SDLC

Software Development Life Cycle. A process followed by a development team, describing how to develop and, maintain software.

### Serverless

A method to provide pay-as-you-use backend computing services, allowing applications to be constructed entirely from functions provided by the supplier. Examples of serverless providers include AWS Lambda and Azure Functions.

### Severity

A severity level is applied to a vulnerability or a license issue, to indicate the risk for that item in an application. See [Severity levels](https://docs.snyk.io/introducing-snyk/snyks-core-concepts/severity-levels).

### Snapshot

An individual report within a project’s test history. Includes a tree of dependancies, and a list of vulnerabilities that was accurate at the time the test was conducted.

### Snyk

A platform providing Cloud Native Application Security (CNAS) solutions, allowing developers to own and build security for the whole application, from code and open source to containers and cloud infrastructure. See [What is Snyk?](https://snyk.io/what-is-snyk/).

Snyk is also the company providing the Snyk platform.

### Snyk Advisor

A free web application which allows you to compare software packages across open source ecosystems. It provides insights into the overall health of a particular package by combining community and security data into a single unified view. See [Snyk Advisor](https://snyk.io/advisor/).

### Snyk API

A Snyk tool, Enables developers to programatically integrate with Snyk. See [Snyk API documentation](https://support.snyk.io/hc/en-us/categories/360000665657-Snyk-API).

### Snyk Broker

A client/server system that serves as an agent / proxy, allowing Snyk to scan private customer environments (Jira, code repositories or container registries). It relays messages and allows users to filter which messages are allowed through; for example, allowing users to expose only some Github APIs to Snyk. See [Snyk Broker documentation](https://docs.snyk.io/integrations/snyk-broker).

### Snyk CLI

A Snyk platform tool. Snyk CLI enables developers to find and fix known vulnerabilities in dependencies, using a command line interface. See [Snyk CLI documentation](https://docs.snyk.io/snyk-cli).

### Snyk Code

A Snyk product. A SAST product enabling developers to find and fix vulnerabilities in your proprietary application code. See [Snyk Code documentation](https://docs.snyk.io/snyk-code).

### Snyk Container

A Snyk product. Enables developers to find and fix vulnerabilities in container images and Kubernetes applications. See [Snyk Container documentation](https://docs.snyk.io/snyk-container).

### Snyk Infrastructure as Code

A Snyk product. Enables developers to find and fix vulnerabilities in your Kubernetes, Helm and Terraform configuration files. See [Snyk IaC documentation](https://docs.snyk.io/snyk-infrastructure-as-code).

### Snyk Open Source

A Snyk product. Enables developers to find and fix open source vulnerabilities. See [Snyk Open Source documentation](https://docs.snyk.io/snyk-open-source).

### Snyk plugin

A library used by the Snyk CLI to scan a certain language/build system.

### Snyk Security Intelligence

A component powering Snyk’s cloud native application security platform.\
Incorporates **Snyk Intel Vulnerability DB**: Snyk’s database of vulnerabilities, providing detailed information and fix advice for known vulnerabilities. See [Vulnerability DB](https://snyk.io/vuln).

### Social Trends

Snyk shows a Trending banner on issues that are being actively discussed in Twitter. See the [Prioritizing Social Trends](https://docs.snyk.io/fixing-and-prioritizing-issues/prioritizing-issues/prioritize-by-social-trends) article.

### SPDX

Software Package Data Exchange. A file format used to document information on the software licenses under which a piece of computer software is distributed.

## U

### Upgradable / Patchable

A fix type: a problem can be fixed by upgrading a version of a package, or by applying a patch.

## V

### Vulnerability

A security vulnerability, identified by Snyk. See [Fixing vulnerabilities](https://docs.snyk.io/fixing-and-prioritizing-issues/issue-management/remediate-your-vulnerabilities).

## W

### Webhook

A way for an app to provide other applications with real-time information. Snyk uses webhooks to check changes in code.
