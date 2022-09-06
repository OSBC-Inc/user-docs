---
description: Creating and setting up your AWS account
---

# AWS 계정

{% hint style="danger" %}
귀하는 귀하의 AWS 계정에서 이 워크샵을 실행하는 동안 사용된 AWS 서비스 비용은 **사용자에게 청구됩니다.** 계정에 새 IAM 역할을 생성하고 다른 IAM 권한의 범위를 지정할 수 있는 기능이 **있어야 합니다.**
{% endhint %}

{% hint style="info" %}
이미 AWS 계정이 있고 IAM 관리자 액세스 권한이 있는 경우 아래 **AWS 서비스 프로비저닝** 섹션으로 이동하십시오.
{% endhint %}

## 계정 만들기

### 1단계

Administrator에 액세스할 수 있는 권한이 있는 AWS 계정이 없는 경우 [지금 만드십시오.](http://docs.aws.amazon.com/connect/latest/adminguide/gettingstarted.html#sign-up-for-aws)

### 2단계

AWS 계정에 대한 관리자 액세스 권한이 있는 **IAM 사용자**로 나머지 워크샵 단계를 수행하고 있는지 확인하십시오. 그렇지 않다면 [워크샵에 사용할 새 IAM 사용자를 만드십시오.](https://console.aws.amazon.com/iam/home?region=us-east-1#/users$new)

### 3단계

사용자 세부 정보를 입력하십시오.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/iam-1-create-user.png)

### 4단계

**AdministratorAccess** IAM 정책을 연결합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/iam-2-attach-policy%20\(1\).png)

### 5단계

새 사용자를 만들려면 클릭하십시오.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/iam-3-create-user.png)

### 6단계

로그인 URL을 기록해 두고 다음을 저장합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/iam-4-save-url.png)

## AWS 서비스 프로비저닝

이번 워크샵에 필요한 AWS 서비스를 프로비저닝하기 위한 프로세스를 단순화하고 자동화했습니다. 이는 [ Amazon EKS AWS Quick Start용 Snyk 컨트롤러](https://github.com/aws-quickstart/quickstart-eks-snyk)를 통해 가능합니다. 아래의 **Launch Stack** 버튼을 클릭하면 AWS CloudFormation 콘솔로 리디렉션되어 다음 단계를 완료하라는 메시지가 표시됩니다.

* 스택을 생성하고, **Next**를 클릭합니다.
* 스택 세부 정보를 지정하고, **Next**를 클릭합니다.
* 스택 옵션을 구성하고, **Next**를 클릭합니다.
* **Capabilities** 아래의 맨 아래 섹션으로 스크롤하고 두 체크박스를 모두 확인한 후 **Create stack**을 클릭합니다.

준비가 되면 [여기를 클릭하여 배포하십시오](https://us-west-2.console.aws.amazon.com/cloudformation/home?region=us-west-2#/stacks/create/template?stackName=Amazon-EKS-with-Snyk\&templateURL=https://aws-quickstart.s3.us-west-2.amazonaws.com/quickstart-amazon-eks/templates/amazon-eks-master.template.yaml)!

{% hint style="warning" %}
설치에는 몇 분이 걸립니다. 다음 섹션을 계속 진행하십시오.
{% endhint %}
