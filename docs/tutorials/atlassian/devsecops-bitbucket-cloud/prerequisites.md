# 전제 조건

{% hint style="danger" %}
AWS 계정에서 이 워크숍을 실행하는 동안 사용되는 AWS 서비스 비용은 귀하의 **책임**입니다. 계정에는 새 IAM 역할을 생성하고 다른 IAM 권한의 범위를 지정할 수 있는 기능이 **있어야 합니다.**
{% endhint %}

{% hint style="info" %}
이미 AWS 계정이 있고 IAM 관리자 액세스 권한이 있는 경우 아래의 **AWS 서비스 프로비저닝** 섹션으로 이동하십시오.
{% endhint %}

## 계정 만들기

### Step 1

관리자 액세스 권한이 있는 AWS 계정이 아직 없는 경우: [지금 생성하십시오](http://docs.aws.amazon.com/connect/latest/adminguide/gettingstarted.html#sign-up-for-aws).

### Step 2

AWS 계정이 있으면 AWS 계정에 대한 관리자 액세스 권한이 있는 IAM 사용자로서 워크숍의 나머지 단계를 수행하고 있는지 확인하십시오: [워크샵에 사용할 새 IAM 사용자 생성](https://console.aws.amazon.com/iam/home?region=us-east-1#/users$new)

### Step 3

사용자 세부 정보를 입력합니다:

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/iam-1-create-user.png)

### Step 4

AdministratorAccess IAM 정책을 연결합니다:

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/iam-2-attach-policy%20\(1\).png)

### Step 5

새 사용자를 생성하려면 클릭하십시오:

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/iam-3-create-user.png)

### Step 6

로그인 URL을 기록하고 다음을 저장합니다:

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/iam-4-save-url.png)

## AWS 서비스 프로비저닝

이 워크샵에 필요한 필수 AWS 서비스를 프로비저닝하는 프로세스를 간소화하고 자동화했습니다. 이는 [Amazon EKS AWS Quick Start용 Snyk 컨트롤러](https://github.com/aws-quickstart/quickstart-eks-snyk)를 통해 가능합니다. 아래의 **Launch Stack** 버튼을 클릭하면 다음 단계를 완료하라는 메시지가 표시되는 AWS CloudFormation 콘솔로 리디렉션됩니다.

* 스택 생성, **Next** 클릭
* Specify stack details, click **Next**
* 스택 세부 정보를 지정하고 **Next**를 클릭합니다.
* **Capabilities** 아래의 맨 아래 섹션으로 스크롤하고 두 상자를 모두 선택하고 **Create stack**을 클릭합니다.

준비가 되면 [여기](https://us-west-2.console.aws.amazon.com/cloudformation/home?region=us-west-2#/stacks/create/template?stackName=Amazon-EKS-with-Snyk\&templateURL=https://aws-quickstart.s3.us-west-2.amazonaws.com/quickstart-amazon-eks/templates/amazon-eks-master.template.yaml)를 클릭하여 배포하십시오!

{% hint style="warning" %}
설치에는 몇 분 정도 걸립니다. 다음 섹션을 계속 진행하십시오.
{% endhint %}
