# SCM(Git) 및 CI/CD 통합 구축 소개

Snyk의 가장 많이 사용되는 통합은 SCM(Git) 또는 CI/CD 파이프라인입니다.

![](../.gitbook/assets/scm-ci-cid.png)

또한 Snyk SCM 통합을 통해 모든 fix PR에서 자동으로 다시 검색하고 새로 도입된 취약성을 차단할 수 있습니다.

두 가지 모두 동일한 비즈니스 목표를 달성할 수 있다면, 둘 중 하나를 선택해야 하는 이유는 무엇일까요?&#x20;

\- 워크플로우 및 프로세스에 따라 모든 조직에 한정되지만 아래와 같이 고려해야 할 사항들을 제공할 수 있습니다. ~~**(\*수정 필요)**~~

### SCM 통합 고려 사항

* 보다 쉽게 설정 및 유지 관리 가
* webhooks 덕분에 fix PR을 차단할 수 있는 기능
* SDLC의 초기부터 사용
* 개발자에게 보다 친화적
* Snyk의 fix PR(SCA 및 도커 파일)
* CI/CD 파이프라인에서 리소스를 사용하지 않음

### CI/CD 통합 고려 사항

* Some package managers require local context and are better run within your environment (notably Scala, Gradle and Go modules)
* More granular options to block
* 강력한 gatekeeper
* container scan의 모범 사례
* Complex repo structure such as large Monorepo, where a CI/CD integration would allow more custom imports
