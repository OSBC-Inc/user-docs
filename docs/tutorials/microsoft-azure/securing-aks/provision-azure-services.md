# Azure 서비스 프로비저닝

## 배경

Azure에 대한 다양한 Snyk Integration 지점을 이해하기 위해 몇 가지 지원 리소스를 배포하고 구성할 것입니다. 이 연습의 목표는 Snyk이 Workload를 보호하는 방법을 보여주는 것입니다. 학습 환경에서 사용하기 위한 기본 패턴을 제공합니다. Azure에 대해 자세히 알아보고 자세히 알아보려면 Microsoft의 [자습 교육 모듈](https://docs.microsoft.com/en-us/learn/browse/?products=azure)을 참조하는 것이 좋습니다.

## AKS(Azure Kubernetes Service) 배포

다음 예제는 CLI를 사용하여 AKS를 배포하기 위한 [Azure Quickstart](https://docs.microsoft.com/en-us/azure/aks/kubernetes-walkthrough)를 기반으로 합니다. 클러스터와 샘플 다중 컨테이너 애플리케이션을 배포합니다. 애플리케이션에는 웹 프런트 엔드와 Redis 인스턴스가 모두 포함됩니다.

### 리소스 그룹 만들기

배포하고 관리할 리소스를 논리적으로 구성하기 위해 [Azure 리소스 그룹](https://docs.microsoft.com/en-us/learn/modules/control-and-organize-with-azure-resource-manager/2-principles-of-resource-groups)을 만드는 것으로 시작합니다. 여기서는 리소스가 Azure에서 실행될 위치도 정의합니다. 이 경우에는 eastus 위치에 배포합니다. 터미널에서 다음 명령을 실행합니다:

```bash
az group create --name mySnykAKSResourceGroup --location eastus
```

성공적으로 완료되면 다음과 유사한 출력이 표시됩니다:

```javascript
{
  "id": "/subscriptions/<guid>/resourceGroups/mySnykAKSResourceGroup",
  "location": "eastus",
  "managedBy": null,
  "name": "mySnykAKSResourceGroup",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null,
  "type": "Microsoft.Resources/resourceGroups"
}
```

아래 그림과 같이 Azure Portal에서 리소스 그룹 생성의 유효성을 검사할 수도 있습니다:

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/azure\_resource\_groups\_01.png)

### AKS Cluster 만들기

다음으로 최근에 만든 `mySnykAKSResourceGroup`에 `mySnykAKSCluster`라는 Cluster를 만들겠습니다. Cluster에는 하나의 노드가 있고 모니터링이 활성화됩니다.

```bash
az aks create --resource-group mySnykAKSResourceGroup --name mySnykAKSCluster --node-count 1 --enable-addons monitoring --generate-ssh-keys
```

완료하는 데 몇 분 정도 걸릴 수 있습니다. 터미널에 다음 출력이 표시됩니다:

```
Finished service principal creation[##########################]  100.0000%
- Running...
AAD role propagation done[[##########################]  100.0000%
```

배포가 완료되면 CLI는 클러스터에 대한 세부 정보가 포함된 긴 JSON 응답을 반환합니다. Azure Portal 내에서 이를 볼 수도 있습니다.

_**Figure 1**_

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/azure\_resource\_groups\_02.png)

_**Figure 2**_

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/azure\_resource\_groups\_03.png)

_**Figure 3**_

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/azure\_resource\_groups\_04.png)

### Cluster에 연결

AKS 클러스터를 관리하기 위해 [kubectl](https://kubernetes.io/docs/user-guide/kubectl/)을 사용합니다. Azure CLI를 사용하고 있으므로 다음 명령을 사용하여 kubectl을 설치해야 합니다:

```bash
az aks install-cli
```

다음으로 자격 증명을 다운로드하고 이를 사용하도록 CLI를 구성하여 AKS에 연결하도록 kubectl을 구성해야 합니다.

```bash
az aks get-credentials --resource-group mySnykAKSResourceGroup --name mySnykAKSCluster
```

성공하면 다음과 유사한 출력이 표시됩니다:

```
Merged "mySnykAKSCluster" as current context in $HOME/.kube/config
```

이제 Cluster에 대한 연결을 확인할 준비가 되었습니다.

```bash
kubectl get nodes
```

노드가 준비되면 다음과 유사한 예시 출력이 표시되어야 합니다:

```
NAME                                STATUS   ROLES   AGE   VERSION
aks-nodepool1-27048785-vmss000000   Ready    agent   5m    v1.15.10
```
