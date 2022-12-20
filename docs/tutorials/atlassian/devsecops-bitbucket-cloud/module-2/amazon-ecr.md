# Amazon ECR

Amazon ECR과 Snyk 간의 통합을 활성화하기 위해 Snyk을  활용합니다: A[WS 클라우드의 개발자 우선 보안](https://github.com/aws-quickstart/quickstart-snyk-security) **AWS Quick Start**.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/quickstart-snyk-security-ecr.png)

{% hint style="success" %}
Snyk의 Amazon ECR(Elastic Container Registry) 통합은 하나의 Amazon ECR 레지스트리와 하나의 Snyk 조직 간에 활성화됩니다. 여러 레지스트리와 통합하려면 각 레지스트리에 대해 고유한 Snyk 조직을 만듭니다.
{% endhint %}

## Snyk API 토큰 받기

From the Snyk console, navigate to **Settings** and under the **General** menu `Copy` your **Organization ID**.

Snyk 콘솔에서 **Settings**로 이동하고 **General** 메뉴에서 **Organization ID**를 `Copy`하십시오.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-api-token.png)

## 통합 활성화

Snyk의 Amazon ECR 통합을 클릭 한 번으로 배포할 수 있도록 교차 계정 액세스를 설정하는 옵션이 있습니다. 이 옵션은 공식 AWS Quick Start로 제공되며 수동 구성이 필요하지 않습니다. 아래의 **Launch Stack** 버튼을 클릭하면 다음 단계를 완료하라는 메시지가 표시되는 AWS CloudFormation 콘솔로 리디렉션됩니다:

* 스택 생성, **Next** 클릭
* 스택 세부 정보를 지정하고 **Next**를 클릭합니다.
* 스택 옵션을 구성하고 **Next**를 클릭합니다.
* **Capabilities** 아래의 맨 아래 섹션으로 스크롤하고 상자를 선택하고 **Create stack**을 클릭합니다.

준비가 되면 [여기를 클릭하여 배포하십시오](https://us-west-2.console.aws.amazon.com/cloudformation/home?region=us-west-2#/stacks/create/template?stackName=Snyk-Security-ECR\&templateURL=https://aws-quickstart.s3.amazonaws.com/quickstart-snyk-security/templates/snyk-ecr.yaml)!

{% hint style="warning" %}
설치를 완료하는 데 약 1분 정도 걸립니다.
{% endhint %}

### 출력 수집

완료되면 AWS CloudFormation 템플릿은 **Outputs** 탭에서 두 가지 필수 값을 제공합니다. 이 값을 복사합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-ecr-integration-01.png)

### 통합 메뉴에 액세스

Snyk 앱에서 **Integrations** 메뉴로 이동한 다음 **ECR**을 클릭합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-ecr-integration-02.png)

### 값 입력

이전에 CloudFormation 콘솔의 **Outputs** 탭에서 복사한 두 값을 해당 필드에 붙여넣은 다음 **Save**를 클릭합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-ecr-integration-03.png)

### 이미지 추가

성공적으로 연결되면 확인 메시지와 **Add your ECR images to Snyk** 버튼을 받게 됩니다. 버튼을 클릭합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-ecr-integration-04.png)

### 저장소 스캔

통합이 활성화되었을 때 선택한 AWS 리전과 연결된 모든 저장소를 찾아볼 수 있습니다. 원하는 리포지토리를 선택한 다음 **Add selected repositories** 버튼을 클릭합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-ecr-integration-05.png)

다음 섹션으로 넘어가겠습니다.
