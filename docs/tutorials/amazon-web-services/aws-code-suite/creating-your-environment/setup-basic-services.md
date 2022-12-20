# 기본 서비스 설정

## 소개

지금까지 우리는 환경을 설정하기 위해 다양한 단계를 거쳤습니다. 문제 없이 모듈을 진행할 수 있도록 도구 및 기타 필요한 단계를 설치합니다. 이제 Unicorn Store 애플리케이션을 지원할 인프라 배포를 시작할 준비가 되었습니다.

#### 기본 서비스 CloudFormation 스택

AWS CodeCommit 및 Amazon ECR 서비스와 같은 몇 가지 기본 서비스를 설정하겠습니다.

{% hint style="info" %}
이 단계는 약 2분이 소요됩니다.
{% endhint %}

다음을 복사하여 Cloud9의 터미널에 붙여넣어 CloudFormation 스택을 시작합니다.

```bash
cd ~/environment/modernization-workshop/modules/30_workshop_app
aws cloudformation create-stack --stack-name WorkshopServices --template-body file://services.yaml --capabilities CAPABILITY_NAMED_IAM
until [[ `aws cloudformation describe-stacks --stack-name "WorkshopServices" --query "Stacks[0].[StackStatus]" --output text` == "CREATE_COMPLETE" ]]; do  echo "The stack is NOT in a state of CREATE_COMPLETE at `date`";   sleep 30; done && echo "The Stack is built at `date` - Please proceed"
```

출력은 아래 창과 같아야 합니다.

```
The stack is NOT in a state of CREATE_COMPLETE at Sun Sep  8 05:53:33 UTC 2019
The Stack is built at Sun Sep  8 05:54:04 UTC 2019 - Please proceed
```
