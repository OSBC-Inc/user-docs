# Kubernetes Integration 구성

## Integration 활성화

Snyk 웹 콘솔에서 `Integrations`로 이동합니다. `Kubernetes`를 검색하고 선택합니다. `Connect`를 클릭하고 `Integration` ID를 클립보드에 복사합니다. `Integration` ID는 `abcd1234-abcd-1234-abcd-1234abcd1234`와 유사한 형식의 UUID입니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk\_integrations\_01.png)

`Integration` ID에 대한 환경 변수를 생성해 보겠습니다.

```bash
IntegrationId=<value>
```

## Snyk 컨트롤러 설치

### Helm chart

터미널에서 다음 명령을 실행하여 helm이 설치되어 있는지 확인합니다:

```bash
brew update && brew install helm
```

그런 다음 다음 명령을 사용하여 Snyk Charts 저장소를 Helm에 추가합니다.

```bash
helm repo add snyk-charts https://snyk.github.io/kubernetes-monitor/
```

성공하면 다음과 유사한 출력이 표시됩니다:

```
"snyk-charts" has been added to your repositories
```

### 네임스페이스

일단 추가되면 Snyk 컨트롤러에 대한 고유한 네임스페이스를 생성해야 합니다. 다음 명령을 실행합니다:

```bash
kubectl create namespace snyk-monitor
```

성공하면 다음과 유사한 출력이 표시됩니다:

```
namespace/snyk-monitor created
```

### 암호

Snyk 모니터는 Snyk `Integration` ID와 `dockercfg` 파일을 사용하여 실행됩니다. 프라이빗 레지스트리를 사용하지 않는 경우 이전 단계의 Snyk `Integration` ID를 포함하는 `snyk-monitor`라는 Kubernetes 암호을 생성하고 다음 명령을 실행합니다.

```bash
kubectl create secret generic snyk-monitor -n snyk-monitor \
        --from-literal=dockercfg.json={} \
        --from-literal=integrationId=$IntegrationId
```

성공하면 다음과 유사한 출력이 표시됩니다:

```
secret/snyk-monitor created
```

### 배포

이제 AKS 클러스터에 Snyk Helm chart를 설치합니다:

```bash
helm upgrade --install snyk-monitor snyk-charts/snyk-monitor \
             --namespace snyk-monitor \
             --set clusterName="mySnykAKSCluster"
```

성공하면 다음과 유사한 출력이 표시됩니다:

```
Release "snyk-monitor" does not exist. Installing it now.
NAME: snyk-monitor
LAST DEPLOYED: Tue Apr 28 16:34:04 2020
NAMESPACE: snyk-monitor
STATUS: deployed
REVISION: 1
TEST SUITE: None
```

### 테스트

다음 명령을 사용하여 pod가 실행 중인지 확인할 수도 있습니다:

```bash
kubectl get pods --namespace snyk-monitor
```

다음 예제 출력에서와 같이 `STATUS` 디스플레이 `Running`을 볼 수 있습니다.

```
NAME                            READY   STATUS    RESTARTS   AGE
snyk-monitor-544ff7ccd9-qkwj8   1/1     Running   0          4m47s
```

Snyk Monitor에는 아웃바운드 인터넷 액세스가 필요합니다.
