# 3단계: Snyk Cloud 환경 생성 및 스캔 (웹 UI)

{% hint style="info" %}
**요약**\
Snyk Cloud IAM 역할을 생성했습니다. 이제 Snyk Cloud 환경을 만들고 스캔할 차례입니다.
{% endhint %}

Snyk Cloud 환경을 생성하고 스캔하려면 역할의 ARN(Amazon Resource Name)을 제공해야 합니다. 그 다음 환경 온보딩을 완료할 수 있습니다.

## 역할 ARN 찾기

역할 ARN은 Terraform 또는 CloudFormation 탬플릿 속 [역할의 이름을 변경한 경우](../snyk-cloud-for-aws-api/step-1-download-iam-role-iac-template.md#optional-change-iam-role-name)를 제외하곤 다음 형식을 따라야 합니다.

```
arn:aws:iam::YOUR-ACCOUNT-ID:role/snyk-cloud-role
```

AWS(Amazon Web Services) 계정 ID를 모르거나 Terraform 또는 CloudFormation 속 IAM 역할의 이름을 변경한 경우, [AWS CLI](step-3-create-and-scan-a-snyk-cloud-environment-web-ui.md#aws-cli) 또는 [AWS Management Console](step-3-create-and-scan-a-snyk-cloud-environment-web-ui.md#aws-management-console)를 이용하여 역할 ARN을 찾을 수 있습니다.

### AWS CLI

AWS CLI를 이용하여 Snyk Cloud IAM 역할의 ARN을 찾으려면 역할 세부 정보를 검색해 `snyk-cloud-role` 를 변경한 역할 이름으로 바꾸십시오:

```
aws iam get-role \
  --role-name snyk-cloud-role \
  --query 'Role.Arn' --output text
```

다음과 같은 출력이 표시됩니다:

```
arn:aws:iam::123412341234:role/snyk-cloud-role
```

### AWS Management Console

1. [AWS Management Console](https://console.aws.amazon.com) 로그인하십시오.
2. [Identity and Access Management](https://console.aws.amazon.com/iamv2/home#/home) 이동하십시오.
3. 왼쪽 사이드바에서 **Roles**를 선택합니다.
4. **Roles** 페이지에서 `snyk-cloud-role` (또는 변경한 경우엔 역할 이름 대체)을 검색하십시오.

<figure><img src="../../../../.gitbook/assets/image (26).png" alt=""><figcaption><p>Search for the name of your role in the AWS Management Console</p></figcaption></figure>

5\. 역할을 선택하십시오.

6\. 역할 세부 정보 페이지의 **Summary** 섹션에서 ARN을 찾아 복사합니다.

<figure><img src="../../../../.gitbook/assets/image (28).png" alt=""><figcaption><p>Copy the role ARN in the AWS Management Console</p></figcaption></figure>

## 환경 생성 및 스캔

1. IAM 역할 템플릿을 다운로드한 Snyk 웹 UI **Add AWS Environment** 모달에서 **IAM 역할 ARN** 필드에 역할 ARN을 입력하십시오.
2. 선택적으로 환경 이름을 입력합니다. 그렇지 않은 경우 Snyk은 AWS 계정 별칭을 사용합니다.
3. **Approve and begin scan**을 선택하십시오.
4. "AWS environment successfully added." 라는 확인 메시지가 표시됩니다. **Add another environment**를 선택하여 **Add AWS Environment** 모달로 돌아가 새 계정을 온보딩하거나, 완료되었다면 **Go to settings**를 선택하십시오.

<figure><img src="../../../../.gitbook/assets/image (70).png" alt=""><figcaption><p>Success message after adding an AWS environment in the Snyk Web UI</p></figcaption></figure>

### 다음 단계

이제 Snyk 웹 UI에서 구성 오류 문제를 볼 수 있습니다. 자세한 내용은 [Snyk Cloud 이슈](../../snyk-cloud-issues/) 참조하십시오.
