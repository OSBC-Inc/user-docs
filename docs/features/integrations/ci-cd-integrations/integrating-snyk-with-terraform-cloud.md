# Terraform Cloud 통합

## Terraform Cloud 개요

[Terraform Cloud](https://www.terraform.io/cloud) (TFC)는 HashiCorp가 제공하는 SaaS 유료 플랫폼으로, Terraform을 사용하는 팀에게 프로덕션 준비 상태 관리 및 지속적인 제공을 제공합니다. Terraform을 통해 클라우드 인프라를 관리하는 팀은 다음과 같은 이점을 얻을 수 있습니다.

* 바로 사용할 수 있는 버전 관리 기능을 통해 클라우드에서 Terraform 상태를 관리할 수 있습니다.
* 팀이 인프라에서 협업하고 인프라 변경 사항을 검토 및 승인할 수 있는 중앙 집중식 장소를 확보합니다.
* Terraform Cloud에서 CI/CD 파이프라인과 유사한 방식으로 클라우드 공급자에 대한 원격 운영을 자동으로 관리하여 Terraform을 사용하여 클라우드 인프라에 변경 사항을 적용합니다.

{% hint style="info" %}
이 기능은 Hashicorp **Business tier** plan\*\*.\*\*의 사용자에게 제공됩니다. 더 낮은 Hashicorp plan에 있는 경우 [**Terraform Cloud Beta Sign Up form**](http://hashi.co/tfc-beta)의 개인 베타 기능 플래그에 액세스하려면 등록해야 합니다.
{% endhint %}

## **Snyk integration**과 **Terraform Cloud**의 통합 개요

Terraform Cloud는 Run Check라고 불리는 새로운 기능을 도입했습니다. TFC의 “Run”은 TFC의 실행 단위를 나타냅니다. TFC는 최종적으로 검토, 승인 및 적용될 Terraform plan을 생성합니다.

Run Check 베타 기능을 사용하면 외부 통합이 “Run” 이벤트에 연결하고 이벤트와 상호 작용하여 이 실행이 성공할지 실패할지 결정하는 상태를 제공할 수 있습니다.

Snyk [introduced support in May 2021](https://snyk.io/blog/prevent-cloud-misconfigurations-hashicorp-terraform-snyk-iac/)에 Terraform 사용자가 모든 주요 클라우드 공급자를 위한 Snyk 보안 정책과 비교하여 Terraform 계획 json 출력을 스캔할 수 있는 지원을 도입했습니다.

The Snyk integration connects the “Run” workflow of Terraform Cloud with Snyk Terraform plan scanning, meaning that for each “Run” generated, Snyk scans the Terraform plan artifact for misconfigurations.

If you are a user of Terraform Cloud, you can sign up with Snyk to set the integration and connect it with your workspaces in Terraform Cloud. Then you'll be able track, manage, and resolve security misconfigurations as part of your software development lifecycle with Terraform Cloud.

## **How to set up and use the integration between Snyk and Terraform Cloud**

{% hint style="warning" %}
You must be an administrator on the Snyk organization to configure the Terraform Cloud integration.
{% endhint %}

Navigate to the dedicated Terraform Cloud integration settings page, under the **Integrations** page in the Snyk Web UI, then follow these steps:

### Set up Terraform plan scanning

1. Copy the provided URL and HMAC Key from the integration setting page in Snyk.
2. Navigate to [Terraform Cloud](https://app.terraform.io) and go into the organization global settings.
3. Go to the Run Tasks settings, for example,\
   `https://app.terraform.io/app/{YOUR_TFC_ORG}/settings/tasks`
4. Create a new Run Task for Snyk with the URL and HMAC key values.\
   The HMAC key is mandatory for the Snyk integration to work, even though it is identified as optional on Terraform Cloud.
5. To connect this Run Task to your workspace in Terraform Cloud, navigate to the Run Tasks settings of a specific workspace and add the newly created run task for Snyk. For example:\
   `https://app.terraform.io/app/{YOUR_TFC_ORG}/workspaces/{YOUR_WORKSPACE}/settings/tasks`
6. Choose the enforcement level (Advisory or Mandatory) and click Create.

Once your integration is set up Snyk scans Terraform plans for each run triggered in your workspace.

### View Terraform plan scanning results

1. For each run triggered in the Terraform Cloud workspace, the result of the Snyk Terraform plan scanning appears under the \`Run tasks\` step, which triggers after the Plan stage finishes.
2. The scan results in either a \`passed\` or a \`failed\` status. If Snyk finds issues in your Terraform plan file, the scan results in a failure.
3. Click on the Details link of the run task results in Terraform Cloud to view further details in Snyk.
   1. You can also find the results under the Projects tab in Snyk by searching for terraform-plan.json which will be under a Target named by `{YOUR_TFC_ORG_NAME}/{YOUR_TFC_WORKSPACE_NAME}`
   2. You can also use the filter in the left pane to show only Terraform Cloud projects
4. A single project in Snyk (`terraform-plan.json`) is created per workspace which uses the Snyk integration. Every project page shows the latest scanning results.
5. To see historical scan results, navigate into the History tab under the relevant project and choose the historic snapshot you wish to view.

### Customize Terraform plan scanning

Snyk Terraform Cloud integration provides the following levels of customization:

* Severity Threshold: Set the minimum level of severity for failure. This can be set on the integration page in Snyk.
* Custom Severities: Set custom severities for issues which overwrite the defaults (for example, [SNYK-CC-TF-63](https://snyk.io/security-rules/SNYK-CC-TF-63)).
* Enforcement Level: Determine whether a failure blocks the apply or not. This setting is controlled via Terraform Cloud. For example, the `Advisory` level does not block the apply even if Snyk finds issues within the minimum severity threshold.

### Notes and limitations

* Snyk receives an event from Terraform Cloud for each "plan" stage finished within the latest run in Terraform Cloud.
* The only way to trigger a scan is through Terraform Cloud by triggering a new "Run".
* You cannot trigger a re-scan of the Terraform plan file through the Snyk UI.
* If you customize the Snyk integration (for example, change severity threshold or customise policy severities), you must trigger a new run in Terraform Cloud for the changes to take effect in Snyk.
