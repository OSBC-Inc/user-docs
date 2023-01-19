# Module 3

## Red Hat OpenShift 컨테이너 플랫폼

이 단계를 완료하려면 실행 중인 OpenShift 4 클러스터가 있어야 합니다. **시작하기**에서 이 실습의 전제 조건을 나열했으며 작업할 클러스터가 아직 없는 경우 [Red Hat의 OpenShift 시작하기 가이드](https://www.openshift.com/try)에 있는 단계를 따라야 합니다.

{% hint style="warning" %}
계속하기 전에 [OpenShift Container Platform CLI(command-line interface)](https://docs.openshift.com/container-platform/4.2/cli\_reference/openshift\_cli/getting-started-cli.html)를 설치해야 합니다.
{% endhint %}

### Kubernetes Workload 보안

#### 클러스터에 인증

CLI를 설치했으면 클러스터 인증부터 시작하겠습니다:

```bash
oc login
```

#### 애플리케이션 배포

다음으로 `oc new-project` 명령을 사용하여 [프로젝트를 생성](https://docs.openshift.com/container-platform/4.2/cli\_reference/openshift\_cli/getting-started-cli.html#creating-a-project)합니다.

```bash
oc new-project demo
```

다음으로 `oc new-app` 명령을 사용하여 [새 앱을 만듭니다](https://docs.openshift.com/container-platform/4.2/cli\_reference/openshift\_cli/getting-started-cli.html#creating-a-new-app). 여기서는 `mongo` 컨테이너 이미지를 사용하여 백엔드를 생성하고 `--name` 매개변수를 전달하여 앱 이름을 `goof-mongo`로 지정합니다:

```bash
oc new-app mongo --name goof-mongo
```

다음으로, 배포 구성에 대해 `oc logs` 명령을 실행하는 상태 bu를 선택적으로 볼 수 있습니다.

```bash
oc logs -f dc/goof-mongo
```

`oc get svc` 명령을 실행하여 생성된 서비스의 상태를 _선택적_으로 볼 수도 있습니다:

```bash
oc get svc goof-mongo
```

이제 프런트엔드 애플리케이션을 배포할 준비가 되었습니다. 여기에서 몇 가지 작업을 수행합니다:

1. 이전에 quay 저장소에 Push한 컨테이너 이미지를 가져옵니다.
2. 프런트엔드가 백엔드와 통신할 수 있도록 `COMPONENT_BACKEND_HOST` 및 `COMPONENT_BACKEND_PORT`를 설정합니다.

```bash
oc new-app quay.io/<QUAY_USER>/goof \
--name goof -e COMPONENT_BACKEND_HOST=goof-mongo \
-e COMPONENT_BACKEND_PORT=27017
```

또한 프런트엔드 배포 구성에 대해 `oc set env` 명령을 실행하여 프런트엔드 앱에 대한 환경 변수를 설정해야 합니다.

```bash
oc set env dc/goof DOCKER=1
```

백엔드에서 수행한 것과 유사하게 선택적으로 `oc get svc`를 실행하여 프런트엔드 서비스의 상태를 확인할 수 있습니다.

```bash
oc get svc goof
```

이제 프런트엔드가 배포되었으므로 웹 브라우저에서 앱에 액세스할 수 있도록 이를 노출해야 합니다. 이를 위해 프런트엔드 서비스에 대해 `oc expose` 명령을 실행합니다.

```bash
oc expose svc/goof
```

마지막으로 `oc get route`를 실행하여 브라우저에 복사하여 붙여넣을 URL을 가져옵니다.

```bash
oc get routes
```

OpenShift 콘솔에 로그인하고 프로젝트의 **Deployment Configs**을 검토하면 이러한 명령의 결과를 볼 수 있습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/openshift-deployment-config.png)

#### OpenShift 4 및 OperatorHub와 함께 Snyk 컨트롤러 설치

**시작하기**에서 클러스터에 Snyk 컨트롤러를 설치해야 한다고 언급했습니다. 아직 수행하지 않았다면 지금이 [가이드](https://support.snyk.io/hc/en-us/articles/360006548317-Install-the-Snyk-controller-with-OpenShift-4-and-OperatorHub)에 설명된 단계를 수행할 적기입니다.

#### Kubernetes Workload 모니터링

Snyk 계정에 로그인하면 [보안 검색을 위해 Kubernetes Workload를 추가](https://support.snyk.io/hc/en-us/articles/360003947117-Adding-Kubernetes-workloads-for-security-scanning)할 수 있습니다. 이 예에서는 최근에 배포된 **goof** 애플리케이션을 모니터링할 것입니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/kubernetes-integration-01.png)

**Add selected workloads**를 클릭하면 Kubernetes 애플리케이션을 포함하여 가져온 모든 프로젝트의 높은 수준의 개요를 볼 수 있는 **Projects** 페이지로 돌아갑니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/kubernetes-integration-02.png)

`demo/replicationcontroller/goof-1` 프로젝트를 클릭하면 애플리케이션 보안 구성과 관련된 추가 세부 정보가 표시됩니다. 이 예에서는 여러 가지 문제가 발견되었음을 알 수 있습니다.

이제 알다시피 Kubernetes는 기본적으로 안전하지 않습니다. 이 주제에 대한 심층 분석을 제공하는 것은 이러한 연습의 범위를 벗어나지만 [클러스터 보안](https://kubernetes.io/docs/tasks/administer-cluster/securing-a-cluster/)에 대한 자세한 문서는 쉽게 사용할 수 있습니다. 포드에 대한 [보안 컨텍스트](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/) 구성, [포드 보안](https://kubernetes.io/docs/concepts/policy/pod-security-policy/) 정책 및 컨테이너에 대한 [기능](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/#set-capabilities-for-a-container) 설정에 대한 추가 읽기가 권장됩니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/kubernetes-integration-03.png)
