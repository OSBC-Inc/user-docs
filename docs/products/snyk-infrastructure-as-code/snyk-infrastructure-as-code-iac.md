# Snyk Infrastructure as Code (IaC) 시작하기

Snyk IaC를 사용하여 Terraform 또는 Kubernetes(Helm 포함) 환경의 구성 파일에서 issue를 탐색, 검사 및 수정합니다. 자세한 내용은 [Scan Kubernetes configuration files](broken-reference) 및 [Scan Terraform files](broken-reference)를 참조하세요.

{% hint style="info" %}
이 문서는 Snyk.io UI를 사용하는 프로세스에 대해 설명합니다. Snyk CLI에서 IaC를 사용하는 방법에 대한 자세한 내용은 [해당 문서](snyk-cli-for-infrastructure-as-code/)를 참조하세요.
{% endhint %}

## 전제 조건

다음 사항을 확인하세요

* Snyk 계정 ([https://snyk.io/](https://snyk.io) 로 이동하여 등록합니다. 자세한 내용은 [Create a Snyk account](https://docs.snyk.io/getting-started/getting-started-snyk-products) 참조).
* 기존 Kubernetes 또는 Terraform 환경에서 작업할 수 있습니다.
* 다른 Snyk 제품과 마찬가지로 Git 저장소를 통합합니다. 자세한 내용은 [Git 저장소(SCM) 통합](../../features/integrations/git-repository-scm-integrations/)을 참조하십시오.

## 1 단계: 프로젝트 가져오기

Snyk에서 테스트하고 모니터링할 저장소를 선택하여 Snyk으로 테스트할 프로젝트를 가져옵니다.

1. Snyk.io에서 **Projects**를 선택합니다.
2. 프로젝트를 추가할 도구(예: GitHub)를 선택합니다.
3. **Personal and Organization repositories**에서 사용할 저장소를 선택합니다.
4. 선택한 저장소를 프로젝트로 가져오려면 **Add selected repositories**를 클릭합니다.
5. 진행률 표시줄이 나타납니다. 가져오기 로그 결과를 보려면 **View log**를 클릭하십시오(Kubernetes 및 Terraform 파일을 동시에 검색할 수 있음).
6. 프로젝트 가져오기를 완료했습니다.

## Stage 2: View configuration file issues



Select **Projects**, then click on the imported project entry, to see information for scanned configuration files, including the number of high, medium and low severity issues found. For example:View results for configuration files in imported projects.View results for configuration files in imported projects.

![](../../.gitbook/assets/getting-started-snyk-iac-1.png)

(Issues are sorted into project types: Helm, Kubernetes and Terraform.)

Click on a project to see more information and details of the issues in a configuration file:

![](../../.gitbook/assets/getting-started-snyk-iac-2.png)

{% hint style="info" %}
If you encounter any errors during import, see [Importing projects](https://support.snyk.io/hc/en-us/sections/360000923478-Importing-projects) FAQs.
{% endhint %}

## Stage 3: View and fix config files

Act on the recommendations produced by Snyk IaC.

1.
2.
3.
4.

## For more information

See [Infrastructure as Code](https://docs.snyk.io/snyk-infrastructure-as-code).
