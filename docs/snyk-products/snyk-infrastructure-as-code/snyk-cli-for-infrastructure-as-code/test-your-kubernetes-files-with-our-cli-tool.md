# CLI를 사용하여 Kubernetes 파일 테스트

Snyk Infrastructure as Code를 사용하여 CLI에서 직접 구성 파일을 테스트할 수 있습니다.

Kubernetes에서 Snyk Infrastructure as Code는 다음 항목을 지원합니다.

* Deployments, Pods 및 Services.
* CronJobs, Jobs, StatefulSet, ReplicaSet, DaemonSet, 및 ReplicationController.

다음 Snyk CLI 명령을 사용하여 지정된 파일의 Issue를 테스트합니다.

```
snyk iac test
```

예를 들어, CLI에서 다음과 같이 입력합니다.

```
snyk iac test deploy.yaml
```

다음과 같이 파일 이름을 추가하여 여러 파일을 지정할 수도 있습니다.

```
snyk iac test file-1.yaml file-2.yaml
```

Snyk CLI를 사용하여 Helm Charts를 스캔하는 단계는 [Snyk CLI로 Helm Cha](test-your-helm-charts-with-our-cli-tool.md)rts 테스트를 참조하십시오.

Snyk CLI를 사용하여 Kustomize 템플릿을 스캔하는 단계는 [Snyk CLI로 Kustomize 파일 테스트](test-your-kustomize-files-with-our-cli-tool.md)를 참조하십시오.
