# Kubernetes 보안

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snykk8s.png)

이 모듈에서는 [Dynatrace ActiveGate](https://www.dynatrace.com/support/help/setup-and-configuration/dynatrace-activegate/)와 [Snyk Monitor for Kubernetes Helm Chart](https://artifacthub.io/packages/helm/snyk/snyk-monitor)를 기존 Kubernetes 클러스터에 배포하는 방법에 대한 몇 가지 실습 예제를 제공합니다. 그런 다음 Kubernetes 프로젝트를 Snyk으로 가져오고 Dynatrace의 결과를 Snyk의 수정 조언과 연관시키는 방법에 대한 안내를 받게 됩니다.

{% hint style="danger" %}
이 기능은 모든 유료 요금제에서 사용할 수 있습니다. 자세한 내용은 [요금제](https://snyk.io/plans/)를 참조하세요.
{% endhint %}

## 전제 조건:

1. 기존 Dynatrace 환경 또는 [무료 평가판](https://www.dynatrace.com/trial/).
2. Snyk **Business or Enterprise** 계획. 자세한 내용은 [요금제](https://snyk.io/plans/)를 참조하십시오.
3. 실행 중인 Kubernetes 클러스터.
4. Snyk의 Goof [샘플 애플리케이션](https://github.com/snyk-partners/k8s-goof).

## 목표:

* Snyk의 Kubernetes Integration을 구성합니다.
* Goof 샘플 앱을 배포합니다.
* Dynatrace 애플리케이션 보안 모듈을 활성화하여 런타임 시 환경의 취약성을 감지합니다.
* Snyk 컨테이너 관련 Issue를 수정합니다.
