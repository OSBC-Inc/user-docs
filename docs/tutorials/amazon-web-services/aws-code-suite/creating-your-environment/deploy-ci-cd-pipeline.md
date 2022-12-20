# CI/CD 파이프라인 배포

## CI/CD란 무엇입니까?

CI(Continuous integration) 및 CD(Continuous Delivery)는 애플리케이션 개발 팀이 기능을 더 자주, 안정적으로 제공할 수 있도록 하는 문화, 일련의 운영 원칙 및 사례 모음을 구현합니다.

지속적인 통합은 개발 팀이 작은 변경 사항을 구현하고 가능한 한 자주 버전 제어 저장소에 코드를 체크인하도록 하는 코딩 철학이자 일련의 관행입니다. 대부분의 최신 애플리케이션은 다양한 플랫폼과 도구에서 코드를 개발해야 하기 때문에 팀은 변경 사항을 통합하고 검증하는 메커니즘이 필요합니다.

CI의 목표는 애플리케이션을 구축하고 테스트하는 일관되고 자동화된 방법을 확립하는 것입니다. 통합 프로세스가 일관되면 팀은 코드 변경을 더 자주 커밋할 가능성이 높아져 피드백 루프를 통해 더 나은 협업과 소프트웨어 품질로 이어집니다.

지속적 전달은 지속적 통합이 끝나는 곳에서 시작됩니다. CD는 선택한 인프라 환경에 대한 애플리케이션 제공을 자동화합니다. 대부분의 팀은 개발 및 테스트 환경과 같은 프로덕션 이외의 여러 환경에서 작업하며 CD는 코드 변경 사항을 자동으로 푸시하는 방법이 있는지 확인합니다. 최신 응용 프로그램의 CD 자동화는 "코드로서의 인프라" 및 불변성과 같은 원칙을 준수하면서 필요한 배포 작업을 수행합니다.

지속적인 통합 및 전달은 사용자에게 양질의 애플리케이션과 코드를 전달하는 것이 목표이기 때문에 지속적인 테스트가 필요합니다. 지속적인 테스트는 종종 CI/CD 파이프라인에서 실행되는 일련의 자동화된 회귀, 성능, 보안 및 기타 테스트로 구현됩니다.

발달한 CI/CD 관행에는 응용 프로그램 변경 사항이 CI/CD 파이프라인을 통해 실행되고 전달 빌드가 프로덕션 환경에 직접 배포되는 연속 배포를 구현하는 옵션이 있습니다.

## 이 워크샵에서 배포 중인 CI/CD 파이프라인

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/aws-pipeline.png)

1. 개발 및 로컬 테스트: 개발자는 Cloud9 IDE 환경에서 코딩 작업을 수행합니다. 작업이 완료되면 개발자는 자신의 변경 사항을 로컬 git 저장소에 commit하고 변경 사항을 테스트합니다.
2. 원격 마스터 브랜치로 푸시: 개발자가 소프트웨어 변경 사항에 만족하면 개발자는 해당 변경 사항을 원격 마스터 브랜치로 푸시합니다. 이 워크샵에서 이것은 AWS CodeCommit Repo입니다.
3. AWS CodePipeline - 커밋 이벤트: CodePipeline은 새로운 커밋이 있는지 AWS CodeCommit을 모니터링합니다. 새 커밋(코드 변경)이 감지되면 CodeBuild 작업이 트리거됩니다.
4. AWS CodePipeline - 빌드: CodeBuild 내에서 일련의 보안 테스트가 계측되어 코드 변경이 애플리케이션에 보안 위험을 추가하지 않는지 검증합니다. 보안 문제가 감지되면 CodePipeline 프로세스의 이 단계가 종료되고 파이프라인 프로세스가 실패 상태를 보고합니다. 보안 문제가 감지되지 않으면 애플리케이션을 빌드하고 패키징하여 빌드 프로세스가 계속됩니다.
5. AWS CodePipeline - Postbuilld: 추가 테스트를 실행하고 해당 테스트를 통과하면 컨테이너가 Amazon ECR로 푸시됩니다.
6. AWS CodePipeline - 배포: 빌드 프로세스가 성공하면 Codepipeline은 새 이미지가 있다는 Elastic Container Service를 업데이트합니다. 새 이미지가 배포되고 모니터링됩니다. 모든 상태 확인을 통과하면 새 배포가 기본 서비스가 되고 이전 배포가 정상적으로 종료됩니다.
7. 모니터링: ECS 및 Application Load Balancer는 컨테이너와 애플리케이션의 상태를 지속적으로 모니터링하고 항상 실행되는 정상 컨테이너 작업의 최소 수를 유지하기 위해 필요한 조정을 수행합니다.

## CI/CD 파이프라인 배포

파이프라인을 배포하려면 Cloud9의 터미널에서 다음 명령을 실행합니다.

```bash
cd ~/environment/modernization-workshop/modules/30_workshop_app
aws cloudformation create-stack --stack-name WorkshopPipeline --template-body file://pipeline.yaml --capabilities CAPABILITY_NAMED_IAM
until [[ `aws cloudformation describe-stacks --stack-name "WorkshopPipeline" --query "Stacks[0].[StackStatus]" --output text` == "CREATE_COMPLETE" ]]; do  echo "The stack is NOT in a state of CREATE_COMPLETE at `date`";   sleep 30; done && echo "The Stack is built at `date` - Please proceed"
```

{% hint style="info" %}
이 단계는 약 1분 정도 소요되며 성공하면 아래와 같은 메시지가 표시됩니다.
{% endhint %}

```
The stack is NOT in a state of CREATE_COMPLETE at Sun Aug  4 05:46:27 UTC 2019
The stack is NOT in a state of CREATE_COMPLETE at Sun Aug  4 05:46:58 UTC 2019
The Stack is built at Sun Aug  4 05:47:29 UTC 2019 - Please proceed
```

이 시점에서 완전히 작동하는 CI/CD CodePipeline이 있어야 합니다. AWS 콘솔에서 CodePipeline으로 이동하여 **WorkshopPipeline-Pipeline**이라는 이름으로 시작하는 파이프라인을 클릭하면 아래와 유사한 화면이 표시됩니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/pipeline-view.png)
