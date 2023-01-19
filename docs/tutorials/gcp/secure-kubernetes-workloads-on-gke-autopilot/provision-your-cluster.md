# 클러스터 프로비저닝

[GCP 콘솔](https://console.cloud.google.com/kubernetes)로 이동하고 메뉴 옵션에서 **Kubernetes Engine**을 선택한 다음 **Clusters**를 선택합니다.

![](../../../.gitbook/assets/gcp-dash-01.png)

상단 메뉴에서 **Create**를 선택하고 GKE Autopilot Cluster의 **Configure**을 선택합니다. 이 자습서의 목적을 위해 모든 기본값을 수락할 수 있습니다.

![](../../../.gitbook/assets/gcp-dash-02.png)

Cluster가 준비되면 상단 메뉴에서 **Connect**를 클릭하고 명령을 복사하여 터미널 창에 붙여넣습니다.

![](../../../.gitbook/assets/gcp-dash-03.png)

Cluster 생성 시 선택한 이름이 접두사로 붙은 노드 목록이 표시되는 간단한 `kubectl get nodes` 명령을 실행하여 연결을 확인할 수 있습니다.
