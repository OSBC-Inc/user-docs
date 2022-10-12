# 파이프라인 편집

예제 파이프라인은 Snyk가 가장 좋아하는 취약한 데모 앱인 [Goof](https://github.com/snyk/goof)의 복제본으로 시작합니다. 이 애플리케이션은 [AWS CodeCommit](https://aws.amazon.com/codecommit/) 저장소에 복제되었지만 CodePipeline에서 지원하는 모든 [소스 제어](https://aws.amazon.com/devops/source-control/) 통합을 [소스 작업 통합](https://docs.aws.amazon.com/codepipeline/latest/userguide/integrations-action-type.html#integrations-source)으로 사용할 수 있습니다.

이 예제에서는 애플리케이션을 [AWS Elastic Beanstalk](https://aws.amazon.com/elasticbeanstalk/)에 배포하기로 선택했지만 CodePipeline에서 지원하는 지원되는 [배포 작업 통합](https://docs.aws.amazon.com/codepipeline/latest/userguide/integrations-action-type.html#integrations-deploy) 중 하나를 선택할 수 있습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-codepipeline-01.png)

AWS CodePipeline 콘솔에서 원하는 파이프라인을 선택하고 위 이미지와 같이 편집 버튼을 클릭합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-codepipeline-02.png)

그런 다음 **Source** 단계 직후에 **Add stage** 버튼을 클릭합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-codepipeline-03.png)

스테이지 이름을 입력하세요. 이름은 무엇을 입력해도 상관없지만, 이 예에서는 이름을 **Scan**으로 지정하고 버튼을 클릭하여 확인하겠습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-codepipeline-04.png)

이제 **Scan** 단계에서 **Add action group**를 클릭합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-codepipeline-05.png)

그러면 아래로 스크롤하여 **Snyk**을 선택하거나 간단히 검색할 수 있는 풀다운 메뉴가 있는 대화 상자가 나타납니다. **Snyk**을 선택합시다!

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-codepipeline-06.png)

또한 **Input artifacts**와 **Output artifacts**를 지정해야 합니다. 이는 각각 **SourceArtifact** 및 **Results**입니다. SourceArtifact는 **Source** 단계에서 구성한 모든 것을 참조하며 출력 결과물의 이름은 원하는 대로 지정할 수 있습니다.

준비가 되면 **Connect to Snyk** 버튼을 클릭합니다.
