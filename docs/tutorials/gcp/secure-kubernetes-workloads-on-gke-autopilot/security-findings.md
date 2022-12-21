# 보안 결과

이제 OKE 클러스터에서 일부 워크로드를 실행하고 Snyk를 배포했으므로 다음과 같은 확인사항을 얻기 위해 이를 분석할 수 있습니다.

* 오픈 소스 라이브러리의 Issue.
* 기본 이미지 업그레이드 권장 사항.
* 애플리케이션 구성 오류.

[Snyk Container](https://snyk.io/product/container-vulnerability-management/)와 함께 사용할 수 있는 안전한 환경을 실행하는 데 중요한 기타 기능도 있습니다.

### Workload 스캔

[Snyk](https://snyk.co/udrgA)에 로그인하고 **Kubernetes** 섹션을 클릭할 **Integrations** 메뉴로 이동합니다. 클러스터와 원하는 네임스페이스(이 경우 둘 다 **goof**로 이름 지정됨)를 선택한 다음 아래와 같이 **Add selected workloads** 버튼을 클릭합니다.

![](../../../.gitbook/assets/snyk-k8s-01.png)

Kubernetes Workload 추가에 대한 자세한 지침은 [설명서 페이지](https://docs.snyk.io/products/snyk-container/image-scanning-library/kubernetes-workload-and-image-scanning/adding-kubernetes-workloads-for-security-scanning)에서 확인할 수 있습니다.

### 프로젝트 상태

선택하면 아래와 같이 프로젝트별로 그룹화된 결과 요약을 찾을 수 있는 기본 프로젝트 페이지로 리디렉션됩니다:

![](../../../.gitbook/assets/snyk-dash-01.png)

이 보기에서 각 범주를 드릴다운하고 조사 결과를 검토할 수 있습니다. Cluster의 잘못된 구성부터 시작하겠습니다.

![](../../../.gitbook/assets/snyk-dash-02.png)

여기에서 애플리케이션이 정의되지 않았거나 잘못 정의된 다양한 설정으로 배포된 것을 볼 수 있습니다. 예를 들어 Workload의 컨테이너에 `container.securityContext.runAsNonRoot`가 `false`로 설정되어 있는지 또는 설정 해제되어 있는지 여부입니다. 이는 배포용 Kubernetes 매니페스트 파일을 업데이트하여 해결할 수 있으며 많은 [Snyk SCM(Source Code Management)](https://docs.snyk.io/features/integrations/git-repository-scm-integrations) Integration 중 하나로 사전에 해결할 수 있습니다.

다음으로 컨테이너 이미지를 살펴보겠습니다.

![](../../../.gitbook/assets/snyk-dash-03.png)

여기에서 애플리케이션과 호환되는 이미지를 고려하고 보안 태세를 개선하기 위해 취약점 수를 줄이는 기본 이미지 업그레이드 권장 사항이 제공됩니다.

마지막으로 오픈 소스 종속성과 발견된 취약점을 살펴보겠습니다.

![](../../../.gitbook/assets/snyk-dash-04.png)

이 보기에서 우리는 [Snyk's Priority Score](https://snyk.io/blog/snyk-priority-score/)와 함께 발견된 취약점에 대한 자세한 컨텍스트 데이터를 얻습니다. 이는 오픈 소스를 안전하게 사용하는 데 있어 가장 큰 문제 중 하나인 먼저 해결해야 할 취약점을 획기적으로 단순화하는 데 도움이 됩니다.
