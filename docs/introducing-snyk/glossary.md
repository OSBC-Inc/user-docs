# 용어 사전

## A

### Advisor

[Snyk Advisor](https://support.snyk.io/hc/en-us/articles/360017682058-Snyk-Glossary#SnykAdvisor)를 참조하십시오.

## B

### Base image

컨테이너 이미지를 구성하는 데 사용되는 상위 이미지이며, 일반적으로 Dockerfile의 FROM 지시문에 정의됩니다. base image는 다른 base image에서 구성할 수 있습니다.

### Broker

[Snyk Broker](../features/integrations/snyk-broker/)를 참조하십시오.

### Build System

소스 코드를 가져와 배포 가능한 애플리케이션(예: 컨테이너)을 빌드하는 시스템입니다.

## C

### CI / CD

지속적 통합(CI), 지속적 배포(CD)가 함께 SDLC 모델을 구성하며 개발자가 작고 빈번한 변경 사항의 개발 및 배포를 자동화하도록 안내합니다. 이렇게 하면 모든 팀 구성원이 최신 소스 코드에 액세스할 수 있으며 개발 중에 커밋된 코드의 호환성을 보장할 수 있습니다.

### CLI

Command Line Interface의 약자로, [Snyk CLI](../features/snyk-cli/)를 참조하십시오.

### Cloud Native Application Security

CI/CD 파이프라인 전체에 보안을 구현하고, 마이크로서비스에 내장된 보안을 자동화하고, 반복을 극대화하여 취약점 유입을 줄입니다. Snyk은 포괄적인 [CNAS platform](https://snyk.io/product/cloud-native-application-security/)을 제공하고 있습니다.

### Container

컨테이너를 사용하면 애플리케이션과 해당 디펜던시를 함께 패키징하여 단일 실행 가능한 단위로 배포할 수 있습니다. 컨테이너는 운영체제 커널이 제공하는 추상화이며, 시스템에서 실행 중인 다른 프로세스로부터 프로세스를 분리할 수 있습니다. 자세한 내용은 [Snyk Container](../snyk-products/snyk-container/)를 참조하십시오.

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

동적 응용 프로그램 보안 테스트(Dynamic Application Security Testing)를 말합니다. 사이트 또는 서비스를 가리킬 수 있는 애플리케이션입니다. 그런 다음 일반적으로 사이트 또는 서비스를 성능 분석한 다음 출력 및 동작을 검사하여 보안 취약점을 파악합니다. [SAST](glossary.md#sast)를 참조하십시오.

### Dependency

응용 프로그램에서 다른 패키지를 사용하면 이 다른 패키지가 사용자 소프트웨어에 종속됩니다.

* 직접 의존성은 사용자가 자신의 프로젝트에 포함하는 패키지입니다.
* 간접 의존성(deep, chained 또는 transitive dependency라고도 함)은 직접 의존성 중 하나에 사용되는 패키지입니다.

### Dependency tree

Dependency path라고도 하며, 소프트웨어 애플리케이션의 종속성을 보여주는 계층적 그래프입니다. 그래프에는 직접 및 간접 디펜던시 모두 포함되며, 많은 수준의 디펜던시가 포함될 수 있습니다.

### DevOps

시스템 개발 수명 주기를 단축하기 위해 소프트웨어 개발과 IT 운영을 결합하는 일련의 문학적 철학, 관행 및 도구입니다.

### DevSecOps

새로운 민첩한 IT 및 DevOps 개발에 최대한 원활하고 투명하게 보안을 통합합니다.

### Dockerfile

Docker를 사용하여 컨테이너 이미지를 빌드하는 데 사용되는 텍스트 파일 형식입니다. Dockerfile에는 상위 기본 이미지 지정을 포함하여 최종 이미지를 생성하는 데 필요한 모든 명령이 포함되어 있습니다.

## E

### Exploit

취약점이 어떻게 악용될 수 있는지 보여주는 것입니다. exploit이 널리 게시되면 일반적으로 ‘exploit in the wild’라고 합니다.

### Exploit Maturity

취약점에 대한 공격이 얼마나 실현 가능한지, 취약점이 널리 게시되었는지, 공격자에게 얼마나 유용한지 측정합니다. [Evaluating and prioritizing vulnerabilities](../features/fixing-and-prioritizing-issues/issue-management/evaluating-and-prioritizing-vulnerabilities.md)을 참조하십시오.

## F

### Fixable / Partially fixable

패치, 업그레이드 또는 핀을 적용하여 Snyk에서 취약점 수정 여부를 확인합니다. [Fixed in version vs. fixable attributes in vulnerabilities](https://support.snyk.io/hc/en-us/articles/4405034808209)를 참조하십시오.

### Fix PR

Snyk은 사용자에게 취약점에 대한 자동 수정이 포함된 pull request를 제공할 수 있습니다.

## G

### Git

소프트웨어 개발 중에 소스 코드의 변경 사항을 추적하기 위한 분산 버전 관리 시스템입니다.

## I

### IAC

Infrastructure as Code의 약자로,[ Snyk Infrastructure as Code](../snyk-products/snyk-infrastructure-as-code/)를 참조하십시오.

### IAST

Interactive Application Security Testing의 약자로, 이 접근 방식은 애플리케이션을 실행하는 동안 취약점을 테스트합니다. [**DAST**](glossary.md#dast) 및 [**SAST**](glossary.md#sast)를 참조하십시오.

### IDE

통합 개발 환경(Integrated Development Environment)의 약자입니다. 일반적으로 소스 코드 편집기, 빌드 자동화 도구 및 디버거와 함께 소프트웨어 개발을 위한 기능을 제공하는 애플리케이션입니다.

### Image

애플리케이션을 실행하는 데 필요한 소프트웨어 집합을 포함하는 컨테이너의 저장된 인스턴스입니다.

### Image layer

컨테이너 이미지는 일반적으로 여러 개의 서로 다른 파일 시스템 계층으로 구성되어 있으며, 런타임에 단일 파일 시스템으로 결합합니다.

### Integrations

Snyk에서 작동하는 타사 제품, 애플리케이션 및 플랫폼을 말합니다. (예: GitHub와 같은 SCM 시스템)

### Issue

Snyk에서 식별 및 나열한 라이선스 문제 또는 취약점입니다.

## L

### Library

패키지의 특정 유형입니다.

## M

### Manifest

패키지의 파일들에 대한 메타데이터를 포함하는 파일입니다.

### Monitor

**snyk monitor**는 프로젝트를 테스트하고 결과를 Snyk에 업로드하는 snyk의 명령어입니다.

## O

### OCI

Open Container Initiative의 약자로, 컨테이너 표준에 대한 협업을 용이하게 하고 공급 업체 솔루션 간에 상호 운용성을 보장하기 위해 설립된 독립적인 기구입니다.

### Organization

Snyk의 조직은 프로젝트를 수집하고 구성하는 방법입니다. 그런 다음 구성원이 특정 프로젝트에 액세스할 수 있습니다.

## P

### Package

패키지 매니저가 사용하는 파일 그룹 및 해당 파일에 대한 추가 메타데이터입니다.

### Package manager

패키지를 자동화하고 관리하는 도구 집합으로, 일반적으로 언어에 따라 다른 Package manager를 사용합니다. (예: npm)

### Package registry

고객이 패키지와 코드를 한 곳에서 호스팅할 수 있는 소프트웨어 패키지 호스팅 서비스입니다.

### Pinnable

수정 유형 중 하나이며, 취약한 버전을 가져오는 직접 의존성을 피하기 위해 간접 의존성의 특정 버전을 정의하고 “pin”합니다.

### PR

Pull Request의 약자로, 사용자가 소스 코드의 변경 사항을 반영하고 동일한 branch에 있는 다른 사용자와 협업할 수 있습니다.

### Priority Score

Snyk는 Issue(취약점 및 라이선스)를 점수화하여 각각의 Issue 해결의 우선순위를 정하는 데 도움이 됩니다. 점수는 CVSS 점수를 포함한 여러 요소를 기반으로 하며 0(낮음)에서 1000(높음) 사이의 범위를 가집니다. [Snyk 우선순위 점수](../features/fixing-and-prioritizing-issues/starting-to-fix-vulnerabilities/snyk-priority-score.md)를 참조하십시오.

### Project

Snyk이 스캔하는 외부 항목으로, 해당 스캔을 실행하는 방법을 정의하는 구성입니다. Snyk 대시보드의 프로젝트 메뉴에 나타납니다. [Snyk Target 및 Projects 소개](../getting-started/introduction-to-snyk-projects/)를 참조하십시오.

## R

### Reachability

실행 중 공격 가능한 취약한 경로의 코드가 애플리케이션에 포함되어 있는지 여부입니다. [Reachable vulnerabilities](../features/fixing-and-prioritizing-issues/prioritizing-issues/reachable-vulnerabilities.md)를 참조하십시오.

### Registry

[Container Registry](glossary.md#container-registry) 또는 [Package Registry](glossary.md#package-registry)를 참조하십시오.

### Repository

애플리케이션 배포에 필요한 모든 요소를 포함하는 저장소 영역을 말합니다.

## S

### SARIF

정적 분석 결과 상호 교환 형식입니다. 정적 분석 도구의 출력을 위한 표준 JSON 기반 형식입니다.

### SAST

정적 애플리케이션 보안 테스트(Static Application Security Testing)를 말합니다. 독점 소프트웨어의 소스 코드를 검토하고 취약점의 원인을 식별하여 소프트웨어를 보호하는 방법입니다. 또한 [DAST](glossary.md#dast)를 참조하십시오.

### SBOM

Software Bill Of Materials의 약자로, 소프트웨어의 구성 요소 목록입니다.

### SCA

Software Composition Analysis의 약자로, 알려진 보안 취약점 및 일반적인 라이선스 문제를 포함하여 애플리케이션에서 사용 중인 오픈소스 및 타사 구성 요소를 식별하는 데 사용되는 기술입니다.

{% hint style="info" %}
정적 코드 분석(프로그램 실행 전에 소스 코드를 검사하여 디버깅하는 방법)과 혼동하지 마십시오.
{% endhint %}

### SCM

Source Code Management의 약자로, code repo / repository / version control system이라고도 합니다. 개발자가 소스 코드를 저장하고 코드의 변경 사항을 추적하기 위해 사용하는 방법입니다. SCM은 여러 기여자의 업데이트를 병합할 때 발생하는 충돌을 해결하는 데 도움이 됩니다. (예: GitHub)

### SDLC

Software Development Life Cycle의 약자로, 소프트웨어 개발 수명 주기를 말합니다. 개발 팀이 뒤따르는 프로세스로, 소프트웨어 개발 및 유지 관리 방법을 설명합니다.

### Serverless

사용한 만큼 지불하는 백엔드 컴퓨팅 서비스를 제공하는 방법으로, 공급자가 제공하는 기능으로 애플리케이션을 완전히 구성할 수 있습니다. serverless provider의 예로는 AWS Lambda와 Azure Functions가 있습니다.

### Severity

심각도 수준은 취약점 또는 라이선스 문제에 적용되어 애플리케이션에서 해당 항목의 위험을 나타냅니다. [심각도 수준](snyks-core-concepts/severity-levels.md)을 참조하십시오.

### Snapshot

프로젝트의 테스트 기록 내에 있는 개별 보고서입니다. 디펜던시 트리 및 테스트 수행 당시 취약점 목록을 포함합니다.

### Snyk

CNAS(Cloud Native Application Security) 솔루션을 제공하는 플랫폼으로 개발자는 코드 및 오픈소스에서 컨테이너 및 클라우드 인프라에 이르기까지 전체 애플리케이션에 대한 보안을 유지하고 구축할 수 있습니다. [What is Snyk?](https://snyk.io/what-is-snyk/)을 참조하십시오.

Synk은 또한 Snyk 플랫폼을 제공하는 회사입니다.

### Snyk Advisor

오픈소스 생태계에서 소프트웨어 패키지를 비교할 수 있는 무료 웹 애플리케이션입니다. 커뮤니티 및 보안 데이터를 단일 통합 뷰에 결합하여 특정 패키지의 전반적인 상태에 대한 통찰력을 갖게 합니다. [Snyk Advisor](https://snyk.io/advisor/)를 참조하십시오.

### Snyk API

개발자가 Snyk과 프로그래밍 방식으로 통합할 수 있도록 지원하는 Snyk 도구입니다. [Snyk API documentation](https://support.snyk.io/hc/en-us/categories/360000665657-Snyk-API)을 참조하십시오.

### Snyk Broker

Agent/Proxy 역할을 하는 클라이언트/서버 시스템으로, Snyk이 개인 고객 환경(Jira, 소스코드 저장소 또는 컨테이너 레지스트리)을 스캔할 수 있습니다. 메시지를 중계하고 사용자가 통과할 수 있는 메시지를 필터링할 수 있습니다. 예를 들어, 사용자가 일부 GitHub API만 Snyk에 노출할 수 있도록 허용한다. Snyk [Broker documentation](../features/integrations/snyk-broker/)을 참조하십시오.

### Snyk CLI

Snyk 플랫폼 도구입니다. Snyk CLI를 사용하면 개발자가 CLI를 사용하여 디펜던시의 알려진 취약점을 찾아 수정할 수 있습니다. [Snyk CLI documentation](../features/snyk-cli/)을 참조하십시오.

### Snyk Code

Snyk의 제품 중 하나입니다. 개발자가 독점 애플리케이션 코드의 취약점을 찾아 수정할 수 있는 SAST 제품입니다. [Snyk Code documentation](../snyk-products/snyk-code/)을 참조하십시오.

### Snyk Container

Snyk의 제품 중 하나입니다. 개발자가 컨테이너 이미지 및 Kubernetes 애플리케이션에서 취약점을 찾아 수정할 수 있습니다. [Snyk Container documentation](../snyk-products/snyk-container/)을 참조하십시오.

### Snyk Infrastructure as Code

Snyk의 제품 중 하나입니다. 개발자가 Kubernetes, Helm 및 Terraform 구성 파일의 취약점을 찾아 수정할 수 있습니다. [Snyk IaC documentation](../tutorials/springone-workshop/snyk-iac-for-developers/)을 참조하십시오.

### Snyk Open Source

Snyk의 제품 중 하나입니다. 개발자가 오픈소스 취약점을 찾아 수정할 수 있습니다. [Snyk Open Source documentation](../snyk-products/snyk-open-source/)을 참조하십시오.

### Snyk plugin

Snyk CLI에서 특정 언어/빌드 시스템을 스캔하는 데 사용하는 라이브러리입니다.

### Snyk Security Intelligence

Snyk의 클라우드 네이티브 애플리케이션 보안 플랫폼을 지원하는 구성 요소입니다.\
**Snyk Intel Vulnerability DB** 통합: Snyk의 취약점 데이터베이스를 통합하여 자세한 정보를 제공하고 알려진 취약점에 대한 조언을 제공합니다. [Vulnerability DB](https://security.snyk.io)를 참조하십시오.

### Social Trends

Snyk는 Twitter에서 활발하게 논의되고 있는 이슈에 대해 트렌드 배너를 보여줍니다. [Prioritize by Social Trends](../features/fixing-and-prioritizing-issues/prioritizing-issues/prioritize-by-social-trends.md) 문서를 참조하십시오.

### SPDX

Software Package Data Exchange의 약자로, 소프트웨어가 배포되는 소프트웨어 라이선스에 대한 정보를 문서화하는 데 사용되는 파일 형식입니다.

## U

### Upgradable / Patchable

수정 유형 중 하나이며, 패키지 버전을 업그레이드하거나 패치를 적용하여 문제를 해결할 수 있습니다.

## V

### Vulnerability

Snyk가 식별한 보안 취약점입니다. [취약점 수정](../snyk-products/snyk-open-source/open-source-basics/fixing-vulnerabilities.md)을 참조하십시오.

## W

### Webhook

프로그램이 다른 애플리케이션에 실시간 정보를 제공하는 방법입니다. Snyk은 웹훅을 사용하여 코드의 변경 사항을 확인합니다.
