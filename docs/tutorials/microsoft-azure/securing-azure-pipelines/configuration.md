# Configuration

Azure DevOps용 **Snyk Security Scan** 확장이 설치되면 몇 가지 간단한 단계를 수행하여 Snyk 계정과 통신할 수 있도록 구성해야 합니다. 이를 위해 **Snyk Service Account**(추천)를 생성하거나 프리 티어 요금제를 사용 중인 경우 **Snyk** **Organization ID**를 사용합니다.

{% hint style="info" %}
[설명서 페이지](https://support.snyk.io/hc/en-us/articles/360004037597-Service-accounts)를 방문하여 Snyk Service Accounts에 대해 자세히 알아볼 수 있습니다.
{% endhint %}

아래와 같이 [Snyk](https://app.snyk.io/)에 로그인하고 오른쪽 상단 탐색 모음에서 기어 아이콘을 클릭하여 토큰을 얻을 수 있습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/azure-devops-11.png)

**Settings** 메뉴에서 **General** 탭을 선택한 다음 조직 ID를 사용하는 경우 복사 버튼을 **클릭**하거나 유료 요금제를 사용하는 경우 **Manage service accounts**(권장)를 클릭합니다.

이제 Azure DevOps 브라우저 탭으로 돌아가 구성을 완료합니다. Azure Pipelines **Project Settings**로 이동하고 아래와 같이 **Service Extensions**을 선택하여 토큰을 추가하거나 변경할 수 있습니다:

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/azure-devops-05.png)

여기에서 **Service URL**을 구성하고 **Snyk API Token**을 입력하고 연결 이름을 지정할 수 있습니다. 아래 이미지를 예로 참조하십시오:

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/azure-devops-06.png)

완료되면 **Save**를 클릭합니다. 이제, 다음 Section으로 넘어갑니다!
