# CLI를 사용하여 Kubernetes 파일 테스트 진행

Snyk Infrastructure as Code를 사용하여 CLI에서 직접 구성 파일을 테스트할 수 있습니다.

Kubernetes에서 Snyk Infrastructure as Code는 다음 항목을 지원합니다.

* Deployments, Pods 및 Services.
* CronJobs, Jobs, StatefulSet, ReplicaSet, DaemonSet, 및 ReplicationController.

CLI는 다음과 같이 사용할 수 있습니다.

## 지정된 파일에 대한 issue 테스트 진행

```
snyk iac test
```

예를 들어, CLI에서 다음과 같이 입력합니다.

```
snyk iac test deploy.yaml
```

다음과 같이 파일 이름을 추가하여 여러 파일을 지정할 수 있습니다.

```
snyk iac test file-1.yaml file-2.yaml
```

## CLI를 사용하여 Helm Charts 스캔 진행

렌더링된 Kuberenetes 매니페스트 파일로 템플릿을 변환한 다음 Snyk IaC CLI를 사용하여 Helm Charts를 스캔합니다.

```
helm template ./iac-helm > helm.yaml
snyk iac test helm.yaml
```

Helm Charts 이름을 `iac-helm`으로 변경합니다.

## CLI를 사용하여 Kustomize 템플릿 스캔 진행

Kuberenetes 매니페스트 파일을 작성한 다음 Snyk IaC CLI를 사용하여 Kustomize 템플릿을 스캔합니다.

```
kustomize build > kubernetes.yaml
snyk iac test kubernetes.yaml
```

Kuberenetes 템플릿에 따라 빌드 파라미터 뒤에 이름을 제공해야 할 수 있습니다.
