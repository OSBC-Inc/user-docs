# Custom rules 제작

Snyk IaC에는 AWS, Azure, GCP 및 Kubernetes를 포함하는 포괄적인 보안 규칙 목록이 포함되어 있습니다. 이러한 규칙은 보안 연구, 모범 사례, 공인된 표준 및 벤치마크를 기반으로 합니다. 이러한 규칙은 Snyk의 보안 엔지니어링 팀이 적극적으로 유지하며 새로운 규칙이 정기적으로 출시됩니다.

이러한 규칙은 첫 번째 검색 시 대부분의 요구를 충족시키지만 태그 지정 표준과 같은 시스템에 대한 추가 보안 규칙을 적용해야 할 수도 있습니다.

#### 추가 Snyk IaC 사용자 지정 규칙 제작

IaC SDK는 보안 팀이 자체 규칙을 정의할 수 있도록 지원하며, [Snyk CLI](../snyk-cli-for-infrastructure-as-code/)에서 이 규칙을 실행하여 개발자에게 피드백을 제공합니다.

SDK를 사용하여 Snyk IaC에 사용자 정의 규칙을 추가하여 표준 규칙과 함께 실행할 수 있으며, 개발 팀에 포괄적인 보안 피드백을 한 곳에서 제공할 수 있습니다.

Snyk IaC(Infrastructure as Code) SDK를 시작하기 위한 초기 지침은 다음과 같습니다.

* [Install the SDK](install-the-sdk.md)
* [Getting started with the SDK](getting-started-with-the-sdk/)
* [How to run custom rules with the Snyk CLI](use-IaC-custom-rules-with-CLI/)
* [How to integrate custom rules within a pipeline](integrating-iac-custom-rules-within-a-pipeline.md)
* [SDK reference](sdk-reference.md)

![End to end flow of writing your own custom rules to distributing and using them to scan files with the Snyk CLI](<../../../.gitbook/assets/image (77) (1) (1).png>)

#### Snyk 플랫폼 정책 및 Snyk IaC 사용자 지정 규칙

{% hint style="info" %}
요약

* Snyk 플랫폼 정책: 이슈 관리
* Snyk IaC 사용자 지정 규칙: 이슈 생성
{% endhint %}

Snyk 플랫폼을 사용하면 [정책](../../../features/fixing-and-prioritizing-issues/policies/)을 직접 만들고 검색 중 Snyk가 식별한 문제의 우선 순위 지정 및 분류 방법을 관리할 수 있습니다. 예를 들어 이슈에 특정 특성이 있는 경우 이슈의 우선 순위를 보통에서 높음으로 변경하거나 특정 기준을 충족하는 경우 이슈를 대량 무시하도록 정책을 정의할 수 있습니다.

Snyk IaC 사용자 정의 규칙 기능을 사용하면 시행하려는 잘못된 구성 검사에 대한 규칙을 직접 정의할 수 있습니다. 구성 파일에서 사용자 지정 규칙이 실패하면 문제가 발생합니다.
