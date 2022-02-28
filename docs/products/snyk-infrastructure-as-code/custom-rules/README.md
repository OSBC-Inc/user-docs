# Custom rules 제작

{% hint style="info" %}
이 기능은 현재 베타 버전입니다. 어떤 피드백이라도 주시면 감사하겠습니다.
{% endhint %}

Snyk IaC는 AWS, Azure, GCP, Kubernetes를 포함하는 포괄적인 보안 규칙 목록을 포함하고 있습니다. 이러한 규칙은 보안 연구, 모범 사례, 공인된 표준 및 벤치마크를 기반으로 합니다. Snyk의 보안 엔지니어링 팀에 의해 적극적으로 유지 관리되고 있으며 새로운 규칙들이 정기적으로 출시됩니다.

이러한 규칙은 첫 번째 스캔 시 대부분의 요구 사항을 충족시키지만 태그 지정 표준과 같은 시스템에 대한 추가 보안 규칙을 적용해야 할 수도 있습니다.

#### 추가적인 Snyk IaC 사용자 지정 규칙 생성

IaC SDK는 보안 팀이 개발자에게 피드백을 제공하는 [Snyk CLI](../snyk-cli-for-infrastructure-as-code/)에서 실행할 고유한 규칙을 정의하는 데 도움이 됩니다.

이 SDK를 사용하면 Snyk IaC에 사용자 정의 규칙을 추가하여 표준 제공 규칙에 따라 실행할 수 있으며, 개발 팀에 포괄적인 보안 피드백을 한 곳에서 제공할 수 있습니다.

Snyk IaC(Infrastructure as Code) SDK를 시작하기 위한 초기 지침:

* [SDK 설치하기](install-the-sdk.md)
* [SDK 시작하기](getting-started-with-the-sdk/)
* [Snyk CLI를 사용하여 사용자 정의 규칙을 실행하는 법](use-IaC-custom-rules-with-CLI/)
* [파이프라인 내에 사용자 정의 규칙을 통합하는 법](integrating-iac-custom-rules-within-a-pipeline.md)
* [SDK reference](sdk-reference.md)

![Snyk　CLI로 파일을 스캔하고 배포하는 데 사용하는 고유한 사용자 지정 규칙을 작성하는 종단 간 흐름](<../../../.gitbook/assets/image (77) (1) (1).png>)

#### Snyk 플랫폼 정책 및 Snyk IaC 사용자 지정 규칙

{% hint style="info" %}
요약:

* Snyk 플랫폼 정책: 이슈 관리
* Snyk IaC 사용자 지정 규칙: 이슈 생성
{% endhint %}

Snyk 플랫폼을 사용하면 [policies](../../../features/fixing-and-prioritizing-issues/policies/)을 직접 만들고 스캔 중 Snyk이 식별한 이슈의 우선 순위 지정 및 분류 방법을 관리할 수 있습니다. 예를 들어 이슈에 특정 속성이 있는 경우 이슈의 우선 순위를 medium에서 high로 변경하거나 특정 기준을 충족하는 경우 이슈를 대량 무시하도록 정책을 정의할 수 있습니다.

Snyk IaC 사용자 정의 규칙 기능을 사용하면 시행하려는 잘못된 구성 검사에 대한 규칙을 직접 정의할 수 있습니다. 구성 파일에서 사용자 지정 규칙이 실패하면 이슈가 발생합니다.

\\
