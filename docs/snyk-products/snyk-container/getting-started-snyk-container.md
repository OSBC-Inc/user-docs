# Snyk Container 시작하기

Snyk Container를 이용하여 컨테이너 이미지의 취약점을 수정하십시오.

{% hint style="info" %}
이 프로세스는 Snyk.io UI를 사용합니다. Snyk CLI를 이용하여 Snyk Container를 사용하는 경우 [컨테이너 보안을 위한 Snyk CLI](snyk-cli-for-container-security/)를 참조하십시오.
{% endhint %}

### 전제 조건

다음 사항이 존재하는지 확인하십시오.

* Snyk 계정 ([https://snyk.io/](https://snyk.io)로 이동하여 가입 - 자세한 내용은 [시작하기](../../getting-started/) 참조)
* Snyk과 함께 사용할 관련 컨테이너 레지스트리에 대한 액세스 확인. Snyk은 여러 레지스트리를 지원합니다. 자세한 내용은 [image scanning information library](image-scanning-library/)를 참조하십시오.

### 1단계: 컨테이너 레지스트리 통합 추가

1. Snyk.io에 로그인합니다.
2. **Integrations**을 선택합니다.
3. **Container registries** 항목을 선택하십시오.
4. Snyk과 통합할 레지스트리를 선택합니다.
5. 프롬프트에 따라 세부 정보를 입력한 다음 변경 사항을 저장하여 Snyk과 통합합니다.

![](../../.gitbook/assets/container-account-credentials.png)

### 2단계: 프로젝트 추가

Snyk으로 스캔을 시작하려면 컨테이너에 대한 프로젝트를 추가하십시오.

1. **Add Project**를 클릭하고 추가할 레지스트리를 선택합니다.
2. 가져올 컨테이너 저장소 및 태그를 선택한 다음 **Add selected repositories**를 클릭하여 프로젝트로 가져옵니다. 또한 Snyk이 저장소에서 취약점을 매일 검사하도록 설정합니다.
3. 진행률이 표시됩니다. 로그 결과를 확인하려면 **View log**를 클릭하십시오.

{% hint style="info" %}
프로젝트 추가 중 오류가 발생하면 [Importing projects](https://support.snyk.io/hc/en-us/sections/360000923478-Importing-projects)를 참조하십시오.
{% endhint %}

### 3단계: 취약점 보기

이제 가져온 프로젝트에 대한 취약점 결과를 볼 수 있습니다.

**Projects**를 선택한 다음 레지스트리 레코드에서 가져온 프로젝트 항목을 클릭하여 해당 프로젝트에 대한 취약점 정보를 확인할 수 있습니다.

![](<../../.gitbook/assets/mceclip2 (1) (1) (1) (3) (3) (4) (6) (1) (1) (1) (2).png>)

화면에서 확인된 취약점의 심각도에 대한 요약을 볼 수 있습니다.

발견된 취약점에 대한 세부 정보를 보려면 각 항목을 클릭하십시오.

![image5.png](../../.gitbook/assets/image5-1-.png)

자세한 내용은 [Snyk 앱에서 이미지 분석 및 수정](getting-around-the-snyk-container-ui/analysis-and-remediation-for-your-images-from-the-snyk-app.md)을 참조하십시오.

### 4단계: 수정 및 검토

1. Snyk의 권장 사항에 따라 발견된 Issue를 수정합니다.
2. 이미지 재구축을 진행합니다.
3. Snyk은 새로운 이미지를 push한 후 자동으로 다시 스캔합니다.
