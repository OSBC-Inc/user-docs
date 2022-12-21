# GKE Autopilot에서 Kubernetes Workload 보호

### GKE Autopilot이란 무엇입니까?

Autopilot은 클러스터 관리의 운영 비용을 줄이고 프로덕션을 위해 클러스터를 최적화하며 더 높은 워크로드 가용성을 제공하도록 설계된 GKE(Google Kubernetes Engine)의 새로운 작업 모드입니다. [여기](https://cloud.google.com/kubernetes-engine/docs/concepts/autopilot-overview)에서 Autopilot에 대해 자세히 알아볼 수 있습니다.

### 무엇을 배울 수 있습니까?

이 가이드에서는 Snyk를 사용하여 GKE Autopilot에서 실행되는 Kubernetes Workload를 빠르게 배포하고 스캔하여 오픈소스 종속성, 컨테이너 이미지, 애플리케이션 구성 오류의 취약점을 찾는 방법을 알아봅니다.

### 전제 조건

* [GCP 무료 평가판](https://console.cloud.google.com/freetrial) 계정.
* 설치가 완료된 [Cloud SDK](https://cloud.google.com/sdk/docs/install).
* [Snyk](https://snyk.co/udrgA) Business 또는 Enterprise 플랜.

{% hint style="danger" %}
이 기능은 모든 유료 요금제에서 사용할 수 있습니다. 자세한 내용은 [요금제](https://snyk.io/plans/)를 참조하세요.
{% endhint %}
