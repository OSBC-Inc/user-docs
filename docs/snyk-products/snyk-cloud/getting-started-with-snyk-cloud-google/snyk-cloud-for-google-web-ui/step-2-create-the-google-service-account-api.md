# 2단계: Google 서비스 계정 생성 (웹 UI)

{% hint style="info" %}
**요약**

Snyk용 [Google 서비스 계정](https://cloud.google.com/iam/docs/service-accounts) 을 선언하는 Terraform 템플릿을 다운로드했습니다. 이제 인프라를 프로비저닝해야 합니다.
{% endhint %}

The process to create the Google service account is the same whether you're using the [Snyk Web UI](./) or [Snyk API](../snyk-cloud-for-google-api/) to onboard your Google project.

To scan a Google Cloud project, Snyk Cloud takes the permissions of a tightly-scoped Google service account that allows Snyk to scan the configuration of your project resources.

The service account you create is granted the following read-only Identity & Access Management (IAM) roles:

* [Security Reviewer](https://cloud.google.com/iam/docs/understanding-roles#iam.securityReviewer)
* [Viewer](https://cloud.google.com/iam/docs/understanding-roles)

Snyk Cloud's service account is granted the [Service Account Token Creator](https://cloud.google.com/iam/docs/understanding-roles#iam.serviceAccountTokenCreator) IAM role to enable it to generate short-lived credentials for your service account.

Additionally, Snyk Cloud has a mechanism in place to lock a service account to the Organization that onboards it. This is a security feature to ensure that nobody can guess a service account name and onboard it into a separate Organization to see those resources.

## Set Google Cloud project ID

Snyk Cloud scans the Google Cloud project specified by the `project_id` [variable](https://www.terraform.io/language/values/variables) in the Terraform template. You must set the variable's value using one of the following methods:

* **Set the `project_id` variable directly in the Terraform template.** On line 4 of the template, change the default value of the `project_id` variable to your project ID:

```
default = "your-project-id"
```

* **Terraform을 적용할 때 `project_id` 변수 설정.** 아래 [Apply the Terraform](step-2-create-the-google-service-account-api.md#apply-the-terraform)  Terraform을 적용하여 Google 서비스 계정을 생성합니다. 이 때 Terraform의 [-var](https://www.terraform.io/language/values/variables#variables-on-the-command-line) 옵션을 사용하여`project_id` 변수를 프로젝트 ID로 설정할 수 있습니다:

```
terraform apply -var="project_id=your-project-id"
```

* **`GOOGLE_PROJECT` 환경 변수 사용.** Terraform [문서](https://registry.terraform.io/providers/hashicorp/google/latest/docs/guides/provider\_reference#full-reference) 참고하십시오.

## Apply the Terraform

{% hint style="info" %}
Before you use the [Terraform CLI](https://www.terraform.io/downloads), ensure you [configure it to use your Google Cloud credentials](https://registry.terraform.io/providers/hashicorp/google/latest/docs/guides/getting\_started).
{% endhint %}

To provision the Google service account using Terraform:

1. In your terminal, navigate to the directory containing your `.tf` file (named `snyk-permissions-google.tf` if downloaded from the Web UI).
2. Using the Terraform CLI, initialize the Terraform project:

```
terraform init
```

3\. Review and apply the Terraform plan:

```
terraform apply
```

4\. Enter `yes` when Terraform asks if you want to perform the actions.

Terraform then creates the Google service account. When it is finished, you'll see the following output:

```
Apply complete! Resources: 22 added, 0 changed, 0 destroyed.

Outputs:

service_account_email = "snyk-cloud-mt-us-abcd1234@my-project.iam.gserviceaccount.com"
```

Copy the service account email for use in the next step.

## What's next?

The next step is to create and scan the Snyk Cloud Environment. See [Step 3: Create and scan a Snyk Cloud Environment for Google (Web UI)](step-3-create-and-scan-a-snyk-cloud-environment-for-google-web-ui.md).
