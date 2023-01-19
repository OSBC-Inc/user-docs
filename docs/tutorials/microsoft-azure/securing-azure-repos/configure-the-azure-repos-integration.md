# Azure Repos Integration 구성

## Integration 활성화

[Integration 문서](https://support.snyk.io/hc/en-us/articles/360004002198-Azure-Repos-integration)에 익숙해지는 것부터 시작하겠습니다. 그런 다음 [Snyk](https://snyk.io/) 웹 콘솔에서 `Integrations`으로 이동합니다. `Azure Repos`를 검색하고 선택합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk\_integrations\_09.png)

구성 메뉴에서 다음 세 단계를 수행해야 합니다:

1. `organization` 입력
2. 개인 액세스 토큰 생성
3. 해당 토큰을 복사하여 붙여넣고 `save`를 클릭하십시오.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk\_integrations\_10.png)

### 개인 액세스 토큰 생성

위 다이어그램에 표시된 `Create a personal access token` 단추를 클릭하면 Azure DevOps 조직으로 리디렉션됩니다. 다음 네 단계를 수행해야 합니다:

1. 토큰 이름(예: `snyk`)을 입력하세요.
2. 범위에 대해 `Custom defined`을 선택합니다.
3. 코드 `Read & write` 선택
4. `Create`를 클릭합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/azure\_tokens\_01.png)

토큰을 복사하여 Azure Repos용 Snyk integrations 페이지에 붙여넣어야 합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/azure\_tokens\_02.png)

이제 스캔을 위해 Azure Repos 저장소를 추가할 준비가 되었습니다!
