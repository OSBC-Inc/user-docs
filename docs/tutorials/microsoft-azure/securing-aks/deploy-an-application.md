# 애플리케이션 배포

## Kubernetes 매니패스트

[Kubernetes 매니페스트](https://docs.microsoft.com/en-us/azure/aks/concepts-clusters-workloads#deployments-and-yaml-manifests) 파일을 사용하여 샘플 애플리케이션을 배포합니다. 저장소에서 편의를 위해 [`azure-vote.yaml`](https://github.com/snyk-partners/snyk-azure-resources/blob/master/templates/azure-vote.yaml)이라는 샘플 파일이 제공됩니다. 매니페스트에는 두 개의 Kubernetes 배포가 포함되어 있습니다. 하나는 샘플 Azure Vote Python 애플리케이션용이고 다른 하나는 [Redis](https://redislabs.com/) 인스턴스용입니다. 두 개의 Kubernetes [services](https://docs.microsoft.com/en-us/azure/aks/concepts-network#services)도 생성됩니다. 하나는 Redis 인스턴스용 내부 서비스이고 다른 하나는 인터넷에서 애플리케이션에 액세스할 수 있도록 하는 외부 서비스입니다.

저장소를 복제하고 로컬 디렉터리에서 작업 중인 경우 다음 명령을 실행하여 `YAML` 매니페스트에서 애플리케이션을 배포합니다.

```bash
kubectl apply -f kube-manifests/azure-vote.yaml
```

성공하면 다음과 유사한 출력이 표시됩니다:

```
deployment "azure-vote-back" created
service "azure-vote-back" created
deployment "azure-vote-front" created
service "azure-vote-front" created
```

## 애플리케이션 테스트

`--watch` 인수를 사용하여 CLI에서 [kubectl get 서비스](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)를 호출하여 애플리케이션 배포를 모니터링하고 `LoadBalancer`의 `EXTERNAL-IP`를 얻습니다.

Run the following command:

```bash
kubectl get service azure-vote-front --watch
```

애플리케이션이 배포되는 동안 다음과 유사한 출력이 표시될 수 있습니다:

```
NAME               TYPE           CLUSTER-IP   EXTERNAL-IP   PORT(S)        AGE
azure-vote-front   LoadBalancer   10.0.37.27   <pending>     80:30572/TCP   6s
```

`EXTERNAL-IP`는 `pending` 상태를 표시합니다. 유효한 공용 IP 주소가 표시될 때까지 기다린 다음 이 값을 복사하여 웹 브라우저에 붙여넣습니다.

브라우저는 다음을 확인하고 표시해야 합니다:

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/azure\_voting\_app.png)
