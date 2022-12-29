# 스캔 결과 해석

`Projects` 페이지에는 추가된 모든 프로젝트의 인벤토리와 결과에 대한 높은 수준의 요약이 포함됩니다. 특정 프로젝트를 확장하여 발견되었을 수 있는 취약성에 대해 자세히 알아보고 이를 수정하는 방법 또는 최적화에 대한 지침을 얻을 수 있습니다. 몇 가지 예를 살펴보겠습니다.

아래 그림은 이전 섹션에서 가져온 두 가지 Workload를 보여줍니다. 이는 결과에 Kubernetes 구성 및 컨테이너 이미지 스캔 결과라는 두 가지 핵심 영역이 포함되어 있음을 보여주기 위해 확장되었습니다. 각각을 클릭하면 추가 정보가 표시됩니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk\_scan\_01.png)

각 Workload를 클릭하여 Kubernetes 구성을 검토하는 것으로 시작하겠습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk\_scan\_02.png)

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk\_scan\_03.png)

위의 결과는 몇 가지 흥미로운 결과를 제공합니다. 이 보기에서 `Vulnerabilities` 요약, `Dependencies` 수 및 `Security configuration`을 볼 수 있습니다. 이 결과가 의미하는 바를 자세히 살펴보고 해석해 봅시다.

Kubernetes 클러스터에 적용한 `azure-vote.yaml` 매니페스트를 살펴보면 `cpu` 및 `memory` 제한과 같은 일부 매개 변수를 정의했음을 알 수 있습니다. 결과적으로 스캔 중에 플래그가 지정되지 않았습니다.

```yaml
resources:
  requests:
    cpu: 100m
    memory: 128Mi
  limits:
    cpu: 250m
    memory: 256Mi
```

그러나 매니페스트는 `readOnlyRootFilesystem`, `runAsNonRoot`, `allowPrivilegeEscalation` 및 `capabilities`와 같은 `securityContext` 매개 변수를 설정하지 않았습니다. 결과적으로 `FAIL` 플래그가 있는 결과에서 이를 확인할 수 있습니다.

* Run as non-root: Workload의 컨테이너에 `container.securityContext.runAsNonRoot`가 `false`로 설정되어 있는지 여부.
* Read-only root file system: Workload의 컨테이너에 `container.securityContext.readOnlyFilesystem`이 `false`로 설정되어 있는지 여부.
* Drop capabilities: 모든 기능이 삭제되고 `CAP_SYS_ADMIN`이 추가되지 않는지 여부.

다음으로 컨테이너 이미지 결과를 자세히 살펴보겠습니다:

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk\_scan\_04.png)

여기에서 `Dockerfile`이 누락되었다는 알림이 즉시 표시됩니다. 배포가 공용 레지스트리에서 [이미지](https://kubernetes.io/docs/concepts/containers/images/)를 가져오는 매니페스트 파일로 구성되었기 때문에 이것이 사실임을 알고 있습니다. `vote-back` 및 `vote-front` 애플리케이션의 경우 각각 `redis` 및 `microsoft/azure-vote-front:v1`에서 이미지를 가져옵니다.

여기서 가장 좋은 방법은 Git 저장소에 Dockerfile을 포함하고 개인 레지스트리에서 이미지를 가져오는 것입니다. 이렇게 하면 기본 이미지의 문제를 해결할 수 있고 [Azure Repos](https://support.snyk.io/hc/en-us/articles/360004002198-Azure-Repos-integration) 및 [ACR(Azure Container Registry)](https://support.snyk.io/hc/en-us/articles/360003946957-Container-security-with-ACR-integrate-and-test)에 대한 Snyk의 통합을 통해 기본 이미지를 스캔 및 모니터링할 수 있습니다.

차후 실습에서 이에 대해 자세히 알아볼 것입니다.
