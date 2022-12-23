# Section 2: IaC Scan 결과 검토

## Step 1: GitHub에서 IaC Scan 결과 검토 <a href="#step-1-review-the-iac-scan-results-in-github" id="step-1-review-the-iac-scan-results-in-github"></a>

컨테이너 Workflow와 마찬가지로 Snyk IaC Action은 스캔 결과를 GitHub Security Code Scanning에 업로드하여 GitHub UI 내에서 잘못된 구성 위험을 볼 수 있습니다. 결과를 보려면 Security -> Code Scanning Alerts -> Snyk Infrastructure as Code로 이동하십시오.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-iac-codescanningresults.png)

이를 통해 배포 매니페스트에 존재하는 위험을 빠르게 초기에 엿볼 수 있습니다. 각 문제를 클릭하면 문제가 소개된 코드 줄, 문제에 대한 설명, 문제가 처음 나타난 Commit이 제공됩니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-iac-issuedetail.png)

## Step 2: Snyk UI에서 IaC Scan 결과 검토 <a href="#step-2-review-iac-scan-results-in-the-snyk-ui" id="step-2-review-iac-scan-results-in-the-snyk-ui"></a>

배포 매니페스트를 Snyk에 추가하여 발견된 문제에 대한 정보를 보고 조치를 취하는 데 도움을 줄 수 있습니다.‌

### Import the deployment YAML into Snyk <a href="#import-the-deployment-yaml-into-snyk" id="import-the-deployment-yaml-into-snyk"></a>

In the Snyk UI, add the `goof-deployment.yaml` and `goof-service.yaml` files into the Project we created before. Click the + sign on the Project entry, and provide the path to the files.​

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-iac-addfiletoproject.png)

Once they import, the files appear in the Project list. Let's explore our service definition first, since it only has a single issue.​

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-iac-selectservice.png)

### Review configuration issues and fix suggestions <a href="#review-configuration-issues-and-fix-suggestions" id="review-configuration-issues-and-fix-suggestions"></a>

The Project issues view shows the issue, its impact, and how it can be resolved. Snyk also highlights the line of code where the change can be introduced.​

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-iac-viewissuedetails.png)

{% hint style="info" %}
Tip: Snyk IaC allows you to [set your own Severity scores](https://support.snyk.io/hc/en-us/articles/360006402818#UUID-c1919782-6bfa-b84b-a638-3913cee39fc5) for the rules it checks against.
{% endhint %}

In the next section, we'll take action to fix these issues and unblock our Snyk Gate to we can merge these changes into our PROD branch. Proceed to Section 3 when ready!
