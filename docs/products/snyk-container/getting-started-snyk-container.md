# Snyk Container 시작하기

컨테이너 이미지의 취약성을 찾고 수정하는 데 도움이 되는 Snyk Container를 시작합니다. 자세한 내용은 [Container security overview](https://support.snyk.io/hc/en-us/articles/360003946897-Container-security-overview) 및 [Snyk Container](https://solutions.snyk.io/snyk-academy/container)를 참조하십시오.

{% hint style="info" %}
이 프로세스에서는 Snyk.io UI를 사용합니다. Snyk CLI (Command-Line Interface) 도구를 사용하는 Snyk Container에 대한 자세한 내용은 [snyk-cli-for-container-security](snyk-cli-for-container-security/ "mention")를 참조하십시오.
{% endhint %}

### 전제 조건

다음 사항이 있는지 확인하십시오.

* Snyk과 함께 사용할 관련 컨테이너 레지스트리에 대한 액세스. Snyk은 Amazon Elastic Container Registry ([ECR](https://docs.snyk.io/snyk-container/image-scanning-library/ecr-image-scanning)), Google Container Registry ([GCR](https://docs.snyk.io/snyk-container/image-scanning-library/gcr-image-scanning)), Microsoft Azure Container Registry ([ACR](https://docs.snyk.io/snyk-container/image-scanning-library/acr-image-scanning)) 및 [JFrog Artifactory](https://docs.snyk.io/snyk-container/image-scanning-library/jfrog-artifactory-image-scanning)등의 레지스트리를 지원합니다. 또는 통합으로 선택한 경우 [Kubernetes](https://docs.snyk.io/snyk-container/image-scanning-library/kubernetes-workload-and-image-scanning)에 액세스할 수 있습니다.
* Snyk 계정([https://snyk.io/](https://snyk.io)로 이동하여 가입 - 자세한 내용은 [Create a Snyk account](https://docs.snyk.io/getting-started/getting-started-snyk-products) 참조).

## 1단계: 컨테이너 레지스트리 통합하기

컨테이너 레지스트리 통합을 선택하여 레지스트리를 Snyk과 연결합니다.

1. Snyk.io에 로그인
2. **Integrations**를 선택합니다.
3. **Container registries** 항목을 선택합니다.
4. Snyk과 통합할 항목을 클릭합니다.
5. 프롬프트가 나타나면 계정 자격 증명 및 기타 세부 정보를 입력한 다음 변경 사항을 저장하여 이 항목을 Snyk과 통합합니다.

![](../../.gitbook/assets/container-account-credentials.png)

## 2단계: 프로젝트 추가

선택한 컨테이너에 대한 프로젝트를 추가하여 Snyk으로 스캔을 시작합니다.

1. **Add Project**를 클릭하고 추가할 통합 레지스트리 항목을 선택합니다.
2. 가져올 컨테이너 저장소 및 태그를 선택한 다음 **Add selected repositories**를 클릭하여 프로젝트로 가져옵니다. 또한 가져오기는 저장소에 대해 Snyk이 저장소에서 취약점을 매일 검사하도록 설정합니다.
3. 진행률 표시줄이 나타납니다: **View log**를 클릭하여 로그 결과를 확인할 수 있습니다.

{% hint style="info" %}
가져오는 동안 오류가 발생하는 경우 [Importing projects](https://support.snyk.io/hc/en-us/sections/360000923478-Importing-projects) 정보를 참조하십시오.
{% endhint %}

## 3단계: 취약점 보기

이제 가져온 프로젝트에 대한 취약점 결과를 볼 수 있습니다.

**Projects**를 선택한 다음 레지스트리 레코드 아래에서 가져온 프로젝트 항목을 클릭하여 해당 프로젝트에 대한 취약점 정보를 확인하십시오.

![](<../../.gitbook/assets/mceclip2 (1) (1) (1) (3) (3) (4) (6) (1) (24).png>)

탐지된 취약점의 심각도에 대한 요약을 볼 수 있습니다.

발견된 취약점의 세부정보를 확인하려면 항목을 클릭하십시오.

![image5.png](../../.gitbook/assets/image5-1-.png)

자세한 내용은 [Snyk 앱에서 이미지 분석 및 수정](getting-around-the-snyk-container-ui/analysis-and-remediation-for-your-images-from-the-snyk-app.md)을 참조하십시오.

## 4단계: 수정 및 검토

1. Snyk 권장 사항에 따라 발견된 문제를 해결합니다.
2. 이미지를 재구축하십시오.
3. 새 이미지를 푸시한 후 Snyk이 자동으로 다시 스캔합니다.

## 자세한 내용은

[Snyk Container](./)를 참조하십시오.
