# Section 2: IaC Scan 결과 검토

## Step 1: GitHub에서 IaC Scan 결과 검토 <a href="#step-1-review-the-iac-scan-results-in-github" id="step-1-review-the-iac-scan-results-in-github"></a>

컨테이너 Workflow와 마찬가지로 Snyk IaC Action은 스캔 결과를 GitHub Security Code Scanning에 업로드하여 GitHub UI 내에서 잘못된 구성 위험을 볼 수 있습니다. 결과를 보려면 Security -> Code Scanning Alerts -> Snyk Infrastructure as Code로 이동하십시오.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-iac-codescanningresults.png)

이를 통해 배포 매니페스트에 존재하는 위험을 빠르게 초기에 엿볼 수 있습니다. 각 문제를 클릭하면 문제가 소개된 코드 줄, 문제에 대한 설명, 문제가 처음 나타난 Commit이 제공됩니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-iac-issuedetail.png)

## Step 2: Snyk UI에서 IaC Scan 결과 검토 <a href="#step-2-review-iac-scan-results-in-the-snyk-ui" id="step-2-review-iac-scan-results-in-the-snyk-ui"></a>

배포 매니페스트를 Snyk에 추가하여 발견된 문제에 대한 정보를 보고 조치를 취하는 데 도움을 줄 수 있습니다.‌

### 배포 YAML을 Snyk으로 가져오기

Snyk UI에서 이전에 생성한 프로젝트에 `goof-deployment.yaml` 및 `goof-service.yaml` 파일을 추가합니다. 프로젝트 항목에서 + 기호를 클릭하고 파일 경로를 제공합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-iac-addfiletoproject.png)

파일을 가져오면 프로젝트 목록에 파일이 나타납니다. 문제가 하나뿐이므로 서비스 정의를 먼저 살펴보겠습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-iac-selectservice.png)

### 구성 문제 검토 및 제안 수정

Project issues view에는 Issue, 그 영향 및 해결 방법이 표시됩니다. Snyk은 또한 변경 사항을 도입할 수 있는 코드 줄을 강조 표시합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-iac-viewissuedetails.png)

{% hint style="info" %}
Tip: Snyk IaC를 사용하면 확인하는 규칙에 대한 [자체 심각도 점수를 설정](https://support.snyk.io/hc/en-us/articles/360006402818#UUID-c1919782-6bfa-b84b-a638-3913cee39fc5)할 수 있습니다.
{% endhint %}

다음 Section에서는 이러한 문제를 해결하고 이러한 변경 사항을 PROD Branch에 병합할 수 있도록 Snyk Gate의 차단을 해제하기 위한 조치를 취할 것입니다. 준비가 되면 Section 3으로 진행하십시오!
