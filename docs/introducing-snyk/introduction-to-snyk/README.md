# Snyk 소개

취약점에 대한 Snyk 테스트와 [코드](../../products/snyk-code/), [오픈 소스 디펜던시](../../products/snyk-open-source/), [컨테이너 이미지](../../products/snyk-container/), [IaC(Infrastructure as Code) 구성](../../products/snyk-infrastructure-as-code/), 컨텍스트, 우선순위 지정 및 수정사항을 제공합니다.

## 지원되는 언어 및 연동

Snyk은 JavaScript, Java (Gradle, Maven), .NET, Python, Golang, Swift, Objective-C (CocoaPods), Scala, Ruby, PHP  Bazel등 다양한 언어를 지원합니다. [자세한 내용](../../products/snyk-open-source/language-and-package-manager-support/)

Snyk은 보안과 관련하여 개발자 우선 접근 방식을 적용하여 IDE, 리포지토리, CI/CD, 런타임, 레지스트리 및 문제 관리 도구와 같은 다양한 도구를 [연동](../../features/integrations/)할 수 있습니다.

## 보안 및 취약점 데이터

[보안 인텔리전스 데이터베이스](https://snyk.io/snyk-intelligence-security/)인 Snyk Intel Vulnerability Database는 오픈 소스, 개발자의 커뮤니티 기여, 독점 연구 및 기계학습을 적용하여 보안을 위협하는 특성에 지속적으로 학습하여 전담 연구 팀에 의해 유지 관리됩니다.

## Snyk CLI

Snyk CLI를 사용하여 로컬 시스템에서 스캔 및 모니터링을 진행하고 이를 파이프라인에 통합할 수 있습니다. Snyk CLI를 사용하여 애플리케이션, 컨테이너 및 인프라 구성에 대한 보안 취약점을 스캔할 수 있습니다. npm, Homebrew, Scoop을 이용하거나 수동으로 설치할 수 있습니다.

[Snyk CLI 시작하기](../../features/snyk-cli/getting-started-with-the-cli/).

## Snyk API

Snyk의 확장성과 API를 통해 개발자는 Snyk의 보안 자동화를 특정 워크플로우에 맞게 조정할 수 있어 일관된 플랫폼 거버넌스를 보장할 수 있습니다. [Snyk API 문서](https://support.snyk.io/hc/en-us/articles/360000914857-Does-Snyk-have-an-API-)에서 자세하게 확인이 가능합니다. [Twilio 및 Spotify](https://snyk.io/blog/snyk-watcher-keep-snyk-in-sync/)에서 Snyk API를 사용하는방법을 확인하세요.

## Snyk 제품 및 플랫폼

* [Snyk Open Source](https://docs.snyk.io/snyk-open-source): 개발자가 오픈 소스 취약덤을 쉽게 찾고 자동으로 수정할 수 있도록 합니다. Snyk Open Source에는 오픈 소스 라이선스 사용을 관리하는데 도움이 되는 [Snyk 라이선스 규정 준수](../../products/snyk-open-source/)가 포함되어 있습니다.
* [Snyk Code](https://snyk.io/product/snyk-code/): 개발 과정에서 실시간으로 애플리케이션 코드의 취약점을 찾아 수정합니다.
* [Snyk Container](https://docs.snyk.io/snyk-container): 컨테이너 이미지 및 Kubernetes 애플리케이션의 취약점을 찾아 수정합니다.
* [Snyk Infrastructure as Code (IaC)](https://docs.snyk.io/snyk-infrastructure-as-code): Terraform 및 Kubernetes 코드에서 안전하지 않은 구성을 찾아 수정합니다.
* [Snyk Intel Vulnerability Database](https://snyk.io/product/vulnerability-database/): 포괄적이고 실행 가능한 오픈 소스 및 컨테이너 취약점 데이터.

## Snyk 시작하기

Snyk을 시작하려면 [시작하기](../../tutorials/getting-started/) 문서를 참조하세요.

* [Snyk Open Source 시작하기](../../getting-started/getting-started-snyk-products/getting-started-snyk-open-source.md).
* [Snyk 라이선스 관리 시작하기](../../getting-started/getting-started-snyk-products/getting-started-snyk-licensing-compliance.md).
* [Snyk Code 시작하기](../../getting-started/getting-started-snyk-products/getting-started-with-snyk-code.md).
* [Snyk Container 시작하기](../../getting-started/getting-started-snyk-products/getting-started-snyk-container.md).
* [Snyk IaC 시작하기](../../getting-started/getting-started-snyk-products/getting-started-snyk-iac.md).

## 온보딩 가이드

회사에서 Snyk을 구현하고 사용하는 방법을 안내합니다.

* [시작하기](./#get-started-with-snyk) - Snyk을 준비하고 팀에서 배포하는 방법
* [그룹 관리자](https://snyk.gitbook.io/group-set-up/) - 그룹 수준에서 설정을 구성하는 방법
* [조직 관리자](https://snyk.gitbook.io/org-set-up/) - 조직 수준에서 설정을 구성하는 방법
* [개발자](https://snyk.gitbook.io/dev-training/) - Snyk Web App, CLI, IDE 및 소스 코드 관리자에게 직접 Snyk을 사용하는 방법
