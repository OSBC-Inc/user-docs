# Snyk Container 시작하기

Snyk Container를 이용하여 컨테이너 이미지의 취약점을 수정하세요. 자세한 내용은 [Container security overview](https://support.snyk.io/hc/en-us/articles/360003946897-Container-security-overview) 와 [Snyk Container](https://solutions.snyk.io/snyk-academy/container)를 참조하세요.

{% hint style="info" %}
이 프로세스는 Snyk.io UI에서 진행합니다. Snyk CLI를 이용하여 Snyk Container를 사용하는 경우 [Snyk CLI for container security](../../products/snyk-container/snyk-cli-for-container-security/)를 참조하세요.
{% endhint %}

### 전제 조건

다음 사항을 확인하세요.

* Snyk과 함께 사용할 관련 컨테이너 레지스트리에 대한 액세스 확인. Snyk은 Amazon Elastic Container Registry ([ECR](https://docs.snyk.io/snyk-container/image-scanning-library/ecr-image-scanning)), Google Container Registry ([GCR](https://docs.snyk.io/snyk-container/image-scanning-library/gcr-image-scanning)), Microsoft Azure Container Registry ([ACR](https://docs.snyk.io/snyk-container/image-scanning-library/acr-image-scanning)), [JFrog Artifactory](https://docs.snyk.io/snyk-container/image-scanning-library/jfrog-artifactory-image-scanning)를 지원합니다. 또는 [Kubernetes](https://docs.snyk.io/snyk-container/image-scanning-library/kubernetes-workload-and-image-scanning)에 액세스할 수 있습니다.
* Snyk 계정 ([https://snyk.io/](https://snyk.io)로 이동하여 가입 - 자세한 내용은 [Create a Snyk account](https://docs.snyk.io/getting-started/getting-started-snyk-products) 참조).

## 1단계: 컨테이너 레지스트리 통합 추가

Snyk과 레지스트리를 연결하려면 컨테이너 레지스트리 통합을 선택하세요.

1. Snyk.io에 로그인합니다.
2. **Integrations**을 선택합니다.
3. **Container registries** 항목을 선택하세요.
4. Snyk과 통합할 레지스트리를 선택합니다.
5. 계정 자격 증명 및 세부 정보를 입력하여 변경 사항을 저장 후 Snyk과 통합을 진행합니다.

![](../../.gitbook/assets/container-account-credentials.png)

## 2단계: 프로젝트 추가

Snyk으로 스캔을 시작하려면 컨테이너에 대한 프로젝트를 추가하세요.

1. **Add Project**를 클릭하고 추가 할 레지스트리를 선택합니다.
2. 컨테이너 저장소 및 태그를 선택한 다음 **Add selected repositories**를 클릭하여 프로젝트에 추가합니다. 이 경우 Snyk이 저장소에서 취약점을 매일 검사하도록 합니다.
3. 진행률이 표시됩니다. 로그 결과를 확인하려면 **View log**를 클릭하세요.

{% hint style="info" %}
프로젝트 추가 중 오류가 발생하면 [Importing projects](https://support.snyk.io/hc/en-us/sections/360000923478-Importing-projects)를 참조하세요.
{% endhint %}

## 3단계: 취약점 확인

추가한 프로젝트에 대한 취약점을 확인할 수 있습니다.

**Projects**를 선택한 다음 레지스트리 레코드에서 추가한 프로젝트 항목을 클릭하여 해당 프로젝트에 대한 취약점 정보를 확인할 수 있습니다.

![](<../../.gitbook/assets/mceclip2 (1) (1) (1) (3) (3) (4) (6) (1) (24).png>)

화면에서 확인된 취약점의 심각도에 대한 요약을 확인합니다.

발견된 취약점에 대한 세부 정보를 각 항목에서 확인할 수 있습니다.

![image5.png](../../.gitbook/assets/image5-1-.png)

자세한 내용은 [Analysis and fixes for your images from the Snyk app](https://docs.snyk.io/snyk-container/getting-around-the-snyk-container-ui/analysis-and-remediation-for-your-images-from-the-snyk-app)을 참조하세요.

## 4단계: 수정 및 검토

1. Snyk의 권장 사항에 따라 발견된 문제를 수정합니다.
2. 이미지 재구축을 진행합니다.
3. Snyk은 새로운 이미지를 push한 후 스캔을 자동으로 진행합니다.

## 자세한 내용 확인

[Snyk Container](https://docs.snyk.io/snyk-container)를 참조하세요.
