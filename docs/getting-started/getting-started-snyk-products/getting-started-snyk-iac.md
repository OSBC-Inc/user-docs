# Snyk IaC (Infrastructure as Code) 시작하기

Snyk IaC를 이용하여 Terraform 및 Kubernetes(Helm 포함) 환경의 구성 파일에서 문제를 검사하여 수정하세요. 자세한 내용은 [Scan Kubernetes configuration files](../../products/snyk-infrastructure-as-code/scan-kubernetes-configuration-files/)와 [Scan Terraform files](../../products/snyk-infrastructure-as-code/scan-terraform-files/)를 참조하세요.

{% hint style="info" %}
이 문서에는 Snyk.io UI를 사용하는 프로세스에 대해 설명합니다. Snyk CLI를 이용하여 Snyk IaC를 사용하는 방법에 대한 자세한 내용은 [Snyk CLI for Infrastructure as Code](../../products/snyk-infrastructure-as-code/snyk-cli-for-infrastructure-as-code/)를 참조하세요.
{% endhint %}

## 전제 조건

다음 사항을 확인하세요.

* Snyk 계정 (go to [https://snyk.io/](https://snyk.io)로 이동하여 가입 - 자세한 내용은 [Create a Snyk account](https://docs.snyk.io/getting-started/getting-started-snyk-products) 참조).
* 작업할 Kubernetes 또는 Terraform 환경.
* 다른 Snyk 제품과 같이 Git 저장소를 통합합니다. 자세한 내용은 [Git repository (SCM) integrations](../../features/integrations/git-repository-scm-integrations/)를 참조하세요.

자세한 내용은 다음을 참조하세요.

* [Configure your integration to find security issues in your Kubernetes configuration files](https://docs.snyk.io/snyk-infrastructure-as-code/scan-kubernetes-configuration-files/configure-integration-for-security-issues-in-kubernetes-configuration-files)
* [Configure your integration to find security issues in your Terraform files](https://docs.snyk.io/snyk-infrastructure-as-code/scan-terraform-files/configure-your-integration-to-find-security-issues-in-your-terraform-filess).

## 1단계: 프로젝트 추가

Snyk이 테스트하고 모니터링할 저장소를 선택하여 Snyk으로 테스트할 프로젝트를 추가합니다.

1. Snyk.io에서 **Projects**를 선택합니다.
2. 프로젝트를 추가할 도구를 선택합니다(예: Github).
3. **Personal and Organization repositories**에서 사용할 저장소를 선택합니다.
4. **Add selected repositories**를 클릭하여 선택한 저장소의 프로젝트를 추가합니다.
5. 진행률이 표시됩니다. **View log**를 클릭하여 로그 결과를 확인할 수 있습니다(Kubernetes 및 Terraform 파일을 동시에 스캔할 수 있음).
6. 프로젝트 추가가 완료됩니다.

## 2단계: 구성 파일 문제 확인

추가한 프로젝트의 구성 파일에 대한 결과를 확인합니다.

**Projects**를 선택한 다음 추가한 프로젝트 항목을 클릭하여 발견된 심각도의 수를 포함한 스캔한 파일의 정보를 확인합니다.

![](../../.gitbook/assets/iac\_-\_issues\_list.png)

(Helm, Kubernetes 및 Terraform과 같은 프로젝트 유형으로 분류합니다.)

프로젝트를 클릭하면 구성 파일의 문제에 대한 세부 정보를 확인할 수 있습니다.

![](../../.gitbook/assets/iac\_-\_select\_config\_file.png)

{% hint style="info" %}
프로젝트 추가 중 오류가 발생하면 [Importing projects](https://support.snyk.io/hc/en-us/sections/360000923478-Importing-projects)를 참조하세요.
{% endhint %}

## 3단계: 구성 파일 확인 및 수정

Snyk IaC에서 생성한 권장사항에 따라서 진행합니다.

1. IaC 결과는 스캔 구성 파일에서 직접적으로 나타납니다.
2. 문제를 클릭하여 해당 문제에 대한 세부 정보와 Snyk IaC의 권장사항을 확인할 수 있습니다.
3. 권장사항에 따라서 구성 파일을 편집한 후 변경 사항에 대한 커밋을 진행합니다.
4. Snyk은 변경된 파일을 자동으로 스캔하고 이에 대한 변경 사항을 확인할 수 있습니다.

## 자세한 내용 확인

[Infrastructure as Code](https://docs.snyk.io/snyk-infrastructure-as-code)를 참조하세요.
