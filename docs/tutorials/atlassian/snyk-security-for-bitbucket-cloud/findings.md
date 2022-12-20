# 결과

매니페스트를 클릭하면 결과가 확장되고 발견된 항목에 대한 추가 정보가 제공됩니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-sec-17.png)

여기에서 [Snyk의 우선 순위 점수](https://snyk.io/blog/snyk-priority-score/)로 순위가 매겨진 모든 취약점 목록을 볼 수 있습니다. 당사의 우선 순위 점수 알고리즘은 다양한 데이터 포인트(요인)를 처리하여 0에서 1000 사이의 점수를 생성합니다. 우리는 0-100부터 시작하여 기업이 프로젝트 내에서 우선 순위를 정하는 것이 아니라 모든 프로젝트에 우선 순위를 지정하고 있음을 빠르게 깨달았습니다. . 세분성은 심각도만 사용하거나 심지어 CVSS를 사용할 때 직면하는 문제를 피하는 데 핵심입니다. 모든 것이 최우선입니다! 우리는 다양한 요소의 가중치를 계산하여 점수가 균등하게 분산되도록 하는 동시에 가장 큰 위험을 초래하는 요소가 가장 높은 점수를 얻도록 했습니다.

이 보기에서 취약성에 대한 컨텍스트 정보와 클릭하면 **Snyk**으로 이동하여 **수정 조언**을 제공하는 링크도 표시됩니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-sec-18.png)

Snyk 앱에서 취약성을 수정하기 위한 권장 사항을 검토하고 **Fix these vulnerabilities** 버튼을 클릭하여 저장소에 대한 **pull request**를 자동으로 생성할 수 있습니다.

마찬가지로 저장소의 모든 **Dockerfile**에 대해 **기본 이미지** 권장 사항 및 **Open a fix PR** 기능으로 잠재적인 보안 Issues를 완화할 수 있는 방법에 대한 통찰력을 얻을 수 있습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-sec-19.png)

Snyk와 Bitbucket Cloud의 통합에 대해 자세히 알아보려면 [설명서 페이지](https://support.snyk.io/hc/en-us/articles/360004032097-Bitbucket-Cloud-integration)를 읽어보십시오.
