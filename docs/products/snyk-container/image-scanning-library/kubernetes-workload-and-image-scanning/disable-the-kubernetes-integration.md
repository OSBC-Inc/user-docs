# Disable the Kubernetes integration

Kubernetes 통합을 사용하지 않도록 설정하려면 먼저 클러스터에서 컨트롤러를 제거하세요. Helm을 사용하여 통합 비활성화를 진행할 수 있으며, Helm을 사용하지 않을 경우 snyk-monitor 네임스페이스를 제거하면 됩니다. Helm을 사용하여 릴리스 이름을 결정해야 합니다.

`$ helm ls --short`

`snyk-monitor`

이 경우 릴리스를 삭제할 수 있습니다.

`$ helm delete snyk-monitor`

컨트롤러를 제거한 후 Snyk의 통합 설정에서 연결 해제 버튼을 누르면 새 워크로드를 가져오고 동기화하는 데 사용하는 자격 증명이 무효화됩니다.

![](../../../../.gitbook/assets/uuid-0873a309-1aa2-20c0-ecf0-068df973ae5d-en.png)
