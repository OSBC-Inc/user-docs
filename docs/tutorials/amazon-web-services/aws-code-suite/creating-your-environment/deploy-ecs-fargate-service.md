# ECS Fargate 서비스 배포

## Fargate 서비스 배포

다음 명령 세트에서는 CloudFormation을 사용하여 Unicorn Store 애플리케이션이 인터넷 트래픽을 처리할 수 있도록 하는 서비스를 배포할 것입니다. CloudFormation 템플릿은 ECS 클러스터, 서비스, 작업 정의, 작업 및 Application Load Balancer를 설정합니다.

```bash
cd ~/environment/modernization-workshop/modules/30_workshop_app
aws cloudformation create-stack --stack-name WorkshopECS --template-body file://ecs-fargate.yaml --capabilities CAPABILITY_NAMED_IAM
until [[ `aws cloudformation describe-stacks --stack-name "WorkshopECS" --query "Stacks[0].[StackStatus]" --output text` == "CREATE_COMPLETE" ]]; do  echo "The stack is NOT in a state of CREATE_COMPLETE at `date`";   sleep 30; done && echo "The Stack is built at `date` - Please proceed"
```

{% hint style="info" %}
이 단계는 약 3분이 소요되며 성공하면 아래와 같은 메시지가 표시됩니다.
{% endhint %}

```
The stack is NOT in a state of CREATE_COMPLETE at Sun Aug  4 05:34:25 UTC 2019
The stack is NOT in a state of CREATE_COMPLETE at Sun Aug  4 05:34:55 UTC 2019
The stack is NOT in a state of CREATE_COMPLETE at Sun Aug  4 05:35:26 UTC 2019
The stack is NOT in a state of CREATE_COMPLETE at Sun Aug  4 05:35:57 UTC 2019
The stack is NOT in a state of CREATE_COMPLETE at Sun Aug  4 05:36:27 UTC 2019
The stack is NOT in a state of CREATE_COMPLETE at Sun Aug  4 05:36:58 UTC 2019
The Stack is built at Sun Aug  4 05:37:28 UTC 2019 - Please proceed
```

테스트하려면 다음 쿼리를 실행하고 출력에서 얻은 URL을 웹 브라우저의 주소 표시줄에 복사합니다. 아래 이미지와 비슷한 내용이 표시되어야 합니다.

```bash
aws elbv2 describe-load-balancers --names="Modernization-Workshop-LB" --query="LoadBalancers[0].DNSName" --output=text
```
