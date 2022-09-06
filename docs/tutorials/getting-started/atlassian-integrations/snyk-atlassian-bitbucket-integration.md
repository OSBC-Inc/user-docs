# Snyk - Atlassian Bitbucket 통합

## Snyk API 토큰 얻기

Snyk 콘솔에서 **Settings**로 이동하고 **General** 메뉴에서 **Organization ID** `Copy`를 선택합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-api-token.png)

토큰을 복사한 후에는 Bitbucket Cloud UI로 돌아가서 `SNYK_TOKEN`으 **저장소 변수**를 정의해야 합니다.

## Bitbucket 통합하기

Snyk 콘솔에서 **Integrations** 이동하고 **Bitbucket Cloud**를 선택합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-integrations-menu.png)

**Bitbucket Cloud** 통합 페이지에서 **Username** 필드에 **Bitbucket username** 을 입력하고 **App password** 필드에 이전 단계의 **Bitbucket app password**를 입력합니다. 그런 다음 `Save`를 클릭합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-bitbucket-integration-01.png)

Snyk 및 Bitbucket 계정을 성공적으로 연결하면 확인 메시지와 **Bitbucket Cloud 저장소를 Snyk에 추가**할 수 있는 기능이 표시됩니다. 계속하려면 버튼을 클릭하십시오.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-bitbucket-integration-02.png)

Snyk으로 가져올 저장소를 찾습니다. 체크박스를 클릭하여 선택한 다음 **Add selected repository** 버튼을 클릭하여 프로젝트를 가져옵니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-bitbucket-add-repo.png)

다음 섹션으로 넘어가십시오.
