# Snyk Controller

Amazon EKS용 Snyk 컨트롤러를 사용하면 실행 중인 EKS 워크로드를 가져와 테스트하고 해당 워크로드의 보안을 약화시킬 수 있는 관련 이미지 및 구성의 취약성을 식별할 수 있습니다. 가져온 후 Snyk는 해당 워크로드를 계속 모니터링하여 새 이미지가 배포되고 워크로드 구성이 변경될 때 추가 보안 문제를 식별합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-controller-architecture.png)

워크숍 초반에 Amazon EKS 클러스터에 Snyk 컨트롤러를 배포했습니다. 이 배포에서는 사용자 환경에서 다음을 설정합니다:

* Snyk용 Kubernetes 네임스페이스
* Skyk 통합 ID 및 docker 구성 json을 포함하는 Kubernetes 암호입니다.
* Snyk 모니터 포드

클러스터에 배포되면 이제 Snyk로 모니터링할 추가 Kubernetes 워크로드를 쉽게 추가할 수 있습니다.

{% hint style="success" %}
[Helm 차트](https://hub.helm.sh/charts/snyk/snyk-monitor)는 Snyk 모니터에서도 사용할 수 있습니다.
{% endhint %}
