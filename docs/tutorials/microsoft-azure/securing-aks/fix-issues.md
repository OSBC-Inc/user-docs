# Issues 수정

이제 알다시피 Kubernetes는 기본적으로 안전하지 않습니다. 이 주제에 대한 심층 분석을 제공하는 것은 이러한 연습의 범위를 벗어나지만 [클러스터 보안](https://kubernetes.io/docs/tasks/administer-cluster/securing-a-cluster/)에 대한 자세한 문서는 쉽게 사용할 수 있습니다. 포드에 대한 [보안 컨텍스트](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/) 구성, [포드 보안](https://kubernetes.io/docs/concepts/policy/pod-security-policy/) 정책 및 컨테이너에 대한 [기능](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/#set-capabilities-for-a-container) 설정에 대한 추가 읽기가 권장됩니다.

그러나 당분간 보안 상태를 개선하기 위해 몇 가지 빠른 변경 사항을 도입할 예정입니다. Kubernetes 매니페스트에 몇 줄을 추가하여 이를 수행할 것입니다.

```yaml
securityContext:
  allowPrivilegeEscalation: false
  readOnlyRootFilesystem: true
  runAsNonRoot: true
  capabilities:
    drop:
      - all
```

편의를 위해 이러한 변경 사항이 포함된 샘플 파일이 이미 생성되어 있습니다. 이름은 [`azure-vote-secure.yaml`](https://github.com/snyk-partners/snyk-azure-resources/blob/master/templates/azure-vote-secure.yaml)이며 이 실습 저장소의 [`kube-manifests/`](https://github.com/snyk-partners/snyk-azure-resources/tree/master/kube-manifests) 디렉터리에서 찾을 수 있습니다.

그런 다음, 다음 명령을 사용하여 이 새 파일을 클러스터에 적용해야 합니다:

```bash
kubectl apply -f kube-manifests/azure-vote-secure.yaml
```

다음과 유사한 출력이 표시됩니다:

```
deployment.apps/azure-vote-back configured
service/azure-vote-back unchanged
deployment.apps/azure-vote-front configured
service/azure-vote-front unchanged
```

`vote-back` 및 `vote-front` 애플리케이션 모두에 대한 `deployment`는 구성된 것으로 표시되는 반면 각각에 대한 `service`는 변경되지 않은 것으로 표시됩니다. 이에 대한 `securityContext`를 정의했기 때문에 이는 예상됩니다.

프로젝트를 다시 한 번 확인하여 변경 사항이 문제를 해결했는지 확인합니다. 클러스터에서 실행 중인 `snyk-monitor`가 있으므로 Workload를 적극적으로 모니터링하고 있습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk\_scan\_05.png)

성공했습니다! 우리는 Kubernetes 구성에서 보안 문제를 식별하고 수정 사항을 포함하도록 매니페스트를 업데이트하고 이를 적용하여 문제를 해결할 수 있었습니다.
