# Snyk 배포

`snyk-monitor`를 클러스터에 배포하여 Kubernetes 워크로드를 스캔할 수 있습니다. 이것은 공식 [helm chart](https://artifacthub.io/packages/helm/snyk/snyk-monitor)로 게시되며 해당 배포 옵션을 기반으로 이러한 단계를 수행할 것입니다. Snyk의 Kubernetes 통합에 대해 자세히 알아보려면 [설명서 페이지](https://docs.snyk.io/products/snyk-container/image-scanning-library/kubernetes-workload-and-image-scanning/kubernetes-integration-overview)를 방문하십시오. 편의를 위해 여기에서 높은 수준의 단계를 다룰 것입니다.

#### Step 1

네임스페이스를 생성합니다:

```bash
kubectl create namespace snyk-monitor
```

#### Step 2

암호 생성합니다:

```bash
kubectl create secret generic snyk-monitor -n snyk-monitor --from-literal=dockercfg.json={} --from-literal=integrationId=abcd1234-abcd-1234-abcd-1234abcd1234
```

{% hint style="info" %}
[Snyk Integrations 페이지](https://app.snyk.io/org/YOUR-ORGANIZATION-NAME/manage/integrations/kubernetes)에서 **Integration** ID를 찾아 복사합니다.
{% endhint %}

#### Step 3

Helm 저장소를 추가합니다:

```bash
helm repo add snyk-charts https://snyk.github.io/kubernetes-monitor/ --force-update
```

#### Step 4

{% hint style="info" %}
"my-cluster"를 클러스터 이름으로 바꿉니다. 또한 GKE Autopilot과의 호환성을 위해 몇 가지 설정을 전달하고 있습니다.
{% endhint %}

차트를 설치합니다:

```bash
helm upgrade --install snyk-monitor snyk-charts/snyk-monitor \
  --namespace snyk-monitor \
  --set pvc.enabled=true \
  --set pvc.create=true \
  --set pvc.name="snyk-monitor-pvc" \
  --set clusterName="my-cluster" \
  --set nodeAffinity.disableBetaArchNodeSelector=true \
  --set requests.memory="512Mi" \
  --set requests."ephemeral-storage"="50Gi" \
  --set limits."ephemeral-storage"="50Gi"
```

이제 앱이 준비될 때까지 기다렸다가 다음 명령을 실행하여 상태를 확인할 수 있습니다:

```bash
kubectl get pods -n snyk-monitor
```

이전 예와 마찬가지로 준비 상태가 표시됩니다.
