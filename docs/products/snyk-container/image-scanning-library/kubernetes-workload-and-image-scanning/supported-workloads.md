# 워크로드 지원

Snyk 컨트롤러는 클러스터에서 다음 워크로드를 감지할 수 있습니다.

* Deployment
* ReplicaSet
* ReplicationController
* DaemonSet
* StatefulSet
* Job
* CronJob
* DeploymentConfig (OpenShift)
* Pod, when these Pods have no parent or owner references

컨트롤러는개별 포드부터 최상위 워크로드에 도달할 때까지 소유자의 참조 체인을 추적하여 이러한 워크로드를 탐지합니다. 예를들어, Pod가 주어지면 컨트롤러는 ReplicaSet이 소유하고있고 ReplicaSet은 다른 소유자가 없으며, 따라서 탐지된 워크로드는 Deploysetment입니다.

사용자 지정 리소스가 워크로드를 소유하는 경우 snyk-monitor는 현재 진행할 수 없으며 현재 워크로드를 컨트롤러가 처리할 수 있는 최상위 워크로드라고 가정해야 합니다.

{% hint style="danger" %}
중요한 데이터는 암호, 인증 토큰 및 SSH 키와 같은 컨테이너의 환경 변수로 일반 텍스트로 **저장하지 않는 것이 좋습니다**. 또는 중요한 데이터를 **숨기고** **볼륨으로 마운트**한 다음 해당 데이터의 정보에 액세스할 수 있습니다.
{% endhint %}
