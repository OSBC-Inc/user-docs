# 1단계: 서비스 계정 IaC 템플릿 다운로드 (웹 UI)

Snyk Cloud 환경을 만들기 전에 Snyk에게 Google 프로젝트의 리소스 구성을 스캔할 수 있는 권한을 부여하는 엄격한 범위의 Google 서비스 계정을 선언하는 코드형 인프라(IaC) 템플릿을 다운로드해야 합니다.

또한 템플릿은 Google Cloud 프로젝트를 위한 [Google 서비스 APIs](https://cloud.google.com/service-usage/docs/enabled-service)를 가능하게 합니다. 이를 통해 Snyk Cloud는 프로젝트의 리소스를 스캔하는 데에 필요한 API를 활용할 수 있습니다.

You will use this IaC template to provision the role in [Step 2: Create the Google service account](step-2-create-the-google-service-account-api.md).

## Download the IaC template

1. In the [Snyk Web UI](https://app.snyk.io/), navigate to **Integrations > Cloud platforms**.
2. Select **Google Cloud**.
3. On the **Add Google Cloud Environment** modal, select the **Terraform** button to download a `snyk-permissions-google.tf` file:

<figure><img src="../../../../.gitbook/assets/image (59).png" alt=""><figcaption><p>The Snyk Cloud Add Google Cloud Environment modal</p></figcaption></figure>

You can now proceed to [Step 2: Create the Google service account.](step-2-create-the-google-service-account-api.md)

{% hint style="info" %}
You can also add a cloud environment from **Organization Settings (cog icon) > Cloud environments**. See [View Snyk Cloud Environments](../../view-snyk-cloud-environments.md#add-an-environment).
{% endhint %}
