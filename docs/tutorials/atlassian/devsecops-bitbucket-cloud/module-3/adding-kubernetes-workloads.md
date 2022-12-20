# Kubernetes 워크로드 추가

## 배경

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/kubernetes-01.png)

Snyk 블로그 ["이미지 보안에서 워크로드 보안까지"](https://snyk.io/blog/from-image-security-to-workload-security/)에서는 Kubernetes의 구성 문제와 Kubernetes API가 클라우드 네이티브 시스템 구축을 위한 강력한 추상화를 제공하지만 기본적으로 안전하지 않다는 사실에 대해 논의합니다. 또한 이 문서는 종종 간과되는 몇 가지 일반적인 구성 속성에 대한 통찰력을 공유합니다.

| Security Context       | 설명                                                                                                                                |
| ---------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| CPU 및 메모리 제한           | 예상되는 CPU 및 메모리 제한을 제한하면 운영 및 보안상의 이점이 있습니다. 보안 측면에서 이는 서비스 거부 공격이 노드가 아닌 앱 및 잠재적으로 전체 클러스터에 미치는 영향을 제한하는 것입니다.                    |
| runAsNonRoot           | 기본적으로 컨테이너는 루트 사용자로 실행됩니다. 이 속성은 컨테이너 런타임에서 즉, 공격자가 컨테이너 컨텍스트에서 명령을 실행할 수 있는 경우 제한된 권한만 가지도록 방지합니다.                               |
| readOnlyRootFilesystem | 기본적으로 컨테이너에 대해 마운트된 파일 시스템은 쓰기 가능합니다. 즉, 컨테이너를 손상시키는 공격자는 디스크에도 쓸 수 있으므로 특정 공격이 더 쉬워집니다. 컨테이너가 상태 비저장이면 쓰기 가능한 파일 시스템이 필요하지 않습니다. |
| 기능                     | Linux 기능은 디스크 쓰기에서 네트워크 통신에 이르기까지 컨테이너에서 수행하는 프로세스를 낮은 수준에서 제어합니다. 모든 기능을 삭제하고 필요한 기능을 추가하는 것은 가능하지만 기능 목록을 이해해야 합니다.             |

다음 연습에서는 이러한 안전하지 않은 구성과 Snyk로 이를 식별하고 수정하는 방법을 보여줍니다.

### 파이프라인 활성화

저장소에서 파이프라인을 활성화하여 시작하겠습니다. Bitbucket 저장소로 이동하여 메뉴 표시줄에서 **Pipelines**를 선택합니다. 맨 아래로 스크롤하고 **Enable** 버튼을 클릭하여 파이프라인 실행을 시작합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/bitbucket-pipelines-enable.png)

### 워크로드 추가

Now, let's go to our Snyk app. Let's navigate to **Integrations** and select **Kubernetes**. Since we previously deployed the Snyk controller into our cluster, this should appear as **Connected to Kubernetes** and we should be able to click the button to **Add your Kubernetes workloads to Snyk**.

이제 Snyk 앱으로 이동하겠습니다. **Integrations**으로 이동하여 **Kubernetes**를 선택하겠습니다. 이전에 클러스터에 Snyk 컨트롤러를 배포했으므로 **Kubernetes에 연결**됨으로 나타나야 하며 버튼을 클릭하여 **Snyk에 Kubernetes 워크로드를 추가**할 수 있어야 합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-eks-integration-01.png)

다음으로 클러스터와 **goof** 앱을 선택합니다. 준비가 되면 **Add selected workloads**를 클릭합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-eks-integration-02.png)

스캔이 완료되면 다음과 같은 결과가 표시됩니다:

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-eks-integration-03%20\(1\).png)

그 결과는 우리를 놀라게 하지 않을 것입니다. 매니페스트를 검사하고 이전에 참조한 모범 사례와 비교하면 구성을 간과할 뿐만 아니라 `securityContext`가 전혀 없습니다. 다음 모듈에서 이에 대해 자세히 살펴보겠습니다.
