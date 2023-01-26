# 2단계: Snyk IAM 역할 생성



{% hint style="info" %}
**요약**\
Snyk Cloud에 대한 IAM(Identity & Management) 역할을 선언하는 Terraform 또는 AWS(Amazon Web Services) CloudFormation 템플릿을 다운로드했습니다. 이제 인프라를 프로비저닝해야 합니다.
{% endhint %}

Snyk IAM 역할을 생성하는 프로세스는 AWS 계정 온보딩에 [Snyk 웹 UI](step-1-download-iam-role-iac-template-web-ui.md) 또는 [Snyk API](../snyk-cloud-for-aws-api/step-1-download-iam-role-iac-template.md) 중 무엇을 사용하던 동일합니다.

프로비저닝할 IAM 역할은 다음과 같은 정책과 연결되어 있습니다:

* AWS 관리형 [SecurityAudit](https://docs.aws.amazon.com/IAM/latest/UserGuide/access\_policies\_job-functions.html#jf\_security-auditor) 읽기 전용 정책
* SecurityAudit 에서 다루지 않는 필수 읽기 권한을 부여하는 추가 인라인 정책

이 역할에는 [외부 ID](https://docs.aws.amazon.com/IAM/latest/UserGuide/id\_roles\_create\_for-user\_externalid.html)를 지정하는 신탁 정책도 있습니다. Snyk은 다른 당사자가 역할 ARN(Amazon Resource Name)을 가지고 있더라도 ID 없이 역할을 맡는 것을 방지하기 위해 조직에 대한 고유 ID를 생성합니다.

## Terraform 또는 CloudFormation으로 IAM 역할 생성

Snyk에서 다운받은 탬플릿의 유형에 따라 다음 도구 중 하나를 이용하여 IAM 역할을 생성할 수 있습니다:

* **Terraform:** [Terraform CLI](step-2-create-the-snyk-iam-role.md#terraform)
* **AWS CloudFormation:** [AWS CLI](step-2-create-the-snyk-iam-role.md#aws-cli) 또는 [AWS Management Console](step-2-create-the-snyk-iam-role.md#aws-management-console)

### Terraform

{% hint style="info" %}
[Terraform CLI](https://www.terraform.io/downloads)를 사용하기 전에, [AWS 자격 증명을 사용하도록 구성](https://registry.terraform.io/providers/hashicorp/aws/latest/docs#authentication-and-configuration)해야 합니다.
{% endhint %}

1. 터미널에서 Snyk IAM 역할 Terraform 파일(Snyk 웹 UI에서 다운로드된 경우 `snyk-permissions-aws.tf`로 명명됨)이 포함된 디렉터리로 이동합니다.
2. Terraform CLI를 사용하여 Terraform 프로젝트를 초기화하십시출력이:

```
terraform init
```

3\. Terraform 계획을 검토하고 적용하십시오:

```
terraform apply
```

4\. Terraform이 작업을 수행할지 물을 때 `yes`를 입력하십시오.

5\. 그런 다음 Terraform이 IAM 역할을 생성합니다. 완료되면 다음의 출력이 표시됩니다:

```
Apply complete! Resources: 1 added, 0 changed, 0 destroyed.
```

### AWS CLI

{% hint style="info" %}
[AWS CLI](https://aws.amazon.com/cli/)를 사용하기 전에   [AWS 자격 증명을 사용하도록 구성](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-quickstart.html)해야 합니다., .
{% endhint %}

1. 터미널에서 Snyk IAM 역할 CloudFormation 파일(Snyk 웹 UI에서 다운로드된 경우 `snyk-permissions-aws.yml`로 명명됨)이 포함된 디렉터리로 이동합니다.
2. AWS CLI를 사용하여 CloudFormation 스택을 시작해 `snyk-cloud-role` 를 IAM 역할의 이름(변경한 경우)으로 바꾸고, `snyk-permissions-aws.yml` 를 파일 이름으로 바꾸십시오:

```
aws cloudformation create-stack \
  --stack-name snyk-cloud-role \
  --capabilities CAPABILITY_NAMED_IAM \
  --template-body file://snyk-permissions-aws.yml
```

3\. 그런 다음 AWS는 IAM 역할을 생성합니다. 이 작업은 약 1분 정도 소요됩니다. 완료되었는지 확인하려면 스택 상태를 가져와 `snyk-cloud-role` 를 IAM 역할 이름으로 바꾸십시오.

```
aws cloudformation describe-stacks \
  --stack-name snyk-cloud-role \
  --query 'Stacks[0].StackStatus'
```

`"CREATE_COMPLETE"`라고 출력이표시되면 AWS가 역할 생성을 완료한 것입니다.

### AWS Management Console

1. [AWS Management Console](https://console.aws.amazon.com)[ ](https://console.aws.amazon.com) 로그인하십시오.
2. [CloudFormation](https://console.aws.amazon.com/cloudformation) 으로이동하십시오.
3. **Create stack** 버튼을:선택하십시오:

<figure><img src="../../../../.gitbook/assets/image (4).png" alt=""><figcaption><p>Select the Create stack button in the AWS Management Console</p></figcaption></figure>

4\. 드롭다운 메뉴에서 **With new resources (standard)**를 선택하십시오.

5\. **Create stack** 페이지의 **Specify template** 섹션에서, **Upload a template file**를 선택하십시오.

6\. 표시되는 **Choose file** 버튼을 선택하고 Snyk IAM 역할이 포함된CloudFormation 파일을 선택하십시오.

7\. **Next**를 선택하십시오.

8\. **Specify stack details** 페이지의 **Stack name** 섹션에서, `snyk-cloud-role`과 같은 스택 이름을 입력합니다.

9\. **Next**를 선택하십시오.

10\. **Configure stack options** 페이지에서 원하는 경우 태그를 입력하고 나머지 기본값을 유지합니다.

11\. **Next**를 선택하십시오.

12\. **Review** 페이지 하단의 **Capabilities** 섹션에서, **I acknowledge that AWS CloudFormation might create IAM resources with custom names** 상자를 선택하십시오.

13\. **Create stack**를 선택하십시오.

14\. AWS 가 스택을 시작하고 스택 세부 정보가 있는 페이지가 표시됩니다. **Refresh** 버튼을 선택하여 상태를 새로고침할 수 있습니다:

<figure><img src="../../../../.gitbook/assets/image (3).png" alt=""><figcaption><p>Select the Refresh button to refresh the stack status in the AWS Management Console</p></figcaption></figure>

**Status** 열에 `CREATE_COMPLETE`가 표시되면 AWS 가 IAM 역할 생성을 완료한 것입니다.

## 다음 단계

다음 단계는 Snyk Cloud 환경을 생성하고 스캔하는 것입니다. [3단계: Snyk Cloud 환경 생성 및 스캔 (웹 UI)](step-3-create-and-scan-a-snyk-cloud-environment-web-ui.md)을 참조하십시오.
