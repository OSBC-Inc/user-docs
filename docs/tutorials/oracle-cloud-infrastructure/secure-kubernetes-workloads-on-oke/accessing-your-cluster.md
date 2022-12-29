# 클러스터에 액세스

OKE 클러스터를 프로비저닝하면 아래와 같이 **Developer Services** 및 **Kubernetes Clusters (OKE)**로 이동할 수 있습니다:

![](../../../.gitbook/assets/oci-console-01.png)

상호 작용하려는 클러스터를 찾고 아래와 같이 해당 이름을 클릭합니다:

![](../../../.gitbook/assets/oke-cluster-dash-01.png)

**Access Cluster** 버튼을 클릭하여 세부 정보를 표시합니다:

![](../../../.gitbook/assets/oke-cluster-dash-02.png)

이 실습에서는 **Local Access**를 선택하고 아래 명령을 적용하여 Kubernetes API와 상호 작용하도록 로컬 환경을 구성합니다:

![](../../../.gitbook/assets/oke-cluster-dash-03.png)

{% hint style="info" %}
[kubectl](https://kubernetes.io/docs/tasks/tools/)이 설치되어 있어야 합니다.
{% endhint %}

터미널에서 다음 명령을 실행하여 테스트할 수 있습니다:

```bash
kubectl get svc
```

모든 것이 작동하는 경우 클러스터 이름, IP 등과 같은 일부 데이터를 표시하는 응답이 표시되어야 합니다.
