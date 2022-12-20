# 시작하기

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-codepipeline-graphic-2.png)

[AWS CodePipeline](https://aws.amazon.com/codepipeline/)은 빠르고 안정적인 애플리케이션 및 인프라 업데이트를 위해 릴리스 파이프라인을 자동화하는 데 도움이 되는 완전관리형 [지속적 전달](https://aws.amazon.com/devops/continuous-delivery/) 서비스입니다. CodePipeline은 정의한 릴리스 모델을 기반으로 코드 변경이 있을 때마다 릴리스 프로세스의 빌드, 테스트 및 배포 단계를 자동화합니다. 이를 통해 기능과 업데이트를 빠르고 안정적으로 제공할 수 있습니다.

## 목적:

AWS CodePipeline에서 Snyk을 성공적으로 활성화하여 배포 전에 소스 코드를 스캔합니다.

## 전제 조건:

1. 리소스를 프로비저닝할 수 있는 적절한 액세스 권한이 있는 AWS 계정.
2. 소스 단계 및 배포 단계로 구성된 기존 파이프라인.

{% hint style="info" %}
AWS CodePipeline을 처음 사용하는 경우 다음 리소스를 검토하는 것이 좋습니다:

[CodePipeline을 시작하려면 어떻게 해야 합니까?](https://docs.aws.amazon.com/codepipeline/latest/userguide/welcome-get-started.html)\
[CodePipeline 듀토리얼](https://docs.aws.amazon.com/codepipeline/latest/userguide/tutorials.html)\
**추천:** [듀토리얼: 간단한 파이프라인 생성(CodeCommit 저장소)](https://docs.aws.amazon.com/codepipeline/latest/userguide/tutorials-simple-codecommit.html)
{% endhint %}
