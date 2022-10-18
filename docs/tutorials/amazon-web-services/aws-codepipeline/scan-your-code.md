# 코드 스캔

Snyk은 파이프라인이 트리거될 때마다 코드를 스캔합니다. 이것은 구성된 저장소의 모든 커밋에 대해 수행되지만 릴리스와 함께 수동으로 트리거할 수도 있습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-codepipeline-15.png)

**Release change** 버튼을 클릭하여 파이프라인을 트리거합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-codepipeline-16.png)

Snyk가 잠재적인 취약점을 찾기 위해 아티팩트를 소비하는 **Scan** 단계가 실행되는 것을 볼 수 있습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-codepipeline-17.png)

**Scan** 단계 내에서 두 개의 클릭 가능한 링크를 볼 수 있습니다. 이는 통합 구성 및 결과 보고서에 해당합니다. 위의 링크를 클릭하면 이 통합을 활성화하기 위한 전체 프로세스를 거치지 않고도 구성된 각 파이프라인에 대한 통합을 재구성할 수 있습니다.

마찬가지로, 단계가 완료되면 **Details** 링크를 클릭하여 결과 보고서를 검토할 수 있습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-codepipeline-18.png)

AWS CodePipeline 콘솔 내에서 자세한 결과 보고서를 사용할 수 있습니다. 이 보고서는 알려진 취약점의 총 수, 종속성 경로 및 이러한 취약점이 어떻게 도입되었는지에 대한 자세한 정보를 제공합니다.

그게 전부 입니! AWS CodePipeline에 대한 Snyk의 통합을 활성화했으며 보안 태세를 개선하기 위한 첫 번째 단계를 밟을 준비가 되었습니다!

Snyk 및 [AWS와의 파트너십](https://snyk.io/partners/aws/)에 대해 자세히 알아보려면 파트너 페이지를 방문하십시오.
