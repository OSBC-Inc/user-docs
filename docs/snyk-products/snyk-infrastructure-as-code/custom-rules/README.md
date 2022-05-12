# Custom Rule 만들기

Snyk IaC는 AWS, Azure, GCP, Kubernetes를 포함하는 포괄적인 보안 규칙 목록을 포함하고 있습니다. 이러한 규칙은 보안 연구, 모범 사례, 공인된 표준 및 벤치마크를 기반으로 합니다. Snyk의 보안 엔지니어링 팀에 의해 적극적으로 유지 관리되고 있으며 새로운 규칙들이 정기적으로 릴리즈됩니다.

이러한 규칙은 첫 번째 스캔 시 대부분의 요구 사항을 충족하는 것을 목표로 하지만 태그 지정 표준과 같은 시스템에 대한 추가 보안 규칙을 적용해야 할 수도 있습니다.

#### 추가적인 Snyk IaC custom rule 생성

IaC SDK는 보안 팀이 자체 규칙을 정의하여 [Snyk CLI](../snyk-cli-for-infrastructure-as-code/) 개발자에게 피드백을 제공합니다.

이 SDK를 사용하면 Snyk IaC에 custom rule을 추가하고 표준 제공 규칙과 함께 실행하여 한 곳에서 개발 팀에 포괄적인 보안 피드백을 제공할 수 있도록 합니다.

Snyk IaC(Infrastructure as Code) SDK를 시작하기 위한 초기 지침은 다음과 같습니다.

* [SDK 설치하기](install-the-sdk.md)
* [SDK 시작하기](getting-started-with-the-sdk/)
* [Snyk CLI를 사용하여 custom rule을 실행하는 법](use-iac-custom-rules-with-cli/)
* [파이프라인 내에 custom rule을 통합하는 법](integrating-iac-custom-rules-within-a-pipeline.md)
* [SDK reference](sdk-reference.md)

![Snyk CLI로 파일을 스캔하고 배포하는 데 사용하는 고유한 custom rule을 작성하는 흐름](<../../../.gitbook/assets/image (77) (1) (1).png>)

#### Snyk 플랫폼 정책 및 Snyk IaC custom rule

{% hint style="info" %}
요약:

* Snyk 플랫폼 정책: Issue 관리
* Snyk IaC custom rule: Issue 생성
{% endhint %}

Snyk 플랫폼을 사용하면 [정책](broken-reference)을 직접 만들고 스캔 중 Snyk이 식별한 Issue의 우선순위 지정 및 분류 방법을 관리할 수 있습니다. 예를 들어 Issue에 특정 속성이 있는 경우 Issue의 우선순위를 medium에서 high로 변경하거나 특정 기준을 충족하는 경우 Issue를 대량 무시하도록 정책을 정의할 수 있습니다.

Snyk IaC custom rule 기능을 사용하면 시행하려는 잘못된 구성 검사에 대한 규칙을 직접 정의할 수 있습니다. 구성 파일에서 custom rule이 실패하면 Issue가 발생합니다.
