# Snyk 인증

## CLI 인증

이 실습에서는 아래에 자세히 설명된 지침에 따라 **토큰으로 인증**하십시오. 브라우저를 통한 **계정 인증**이 대안으로 제공됩니다.

### 계정으로 CLI 인증

Snyk CLI 도구로 작업할 때 Snyk은 먼저 인증이 필요합니다.

인증하려면 아래와 같이 진행하십시오.

1.  CLI에서 `snyk auth`를 실행합니다.

    브라우저 탭이 열리고 계정에서 사용할 CLI를 인증하도록 리디렉션됩니다.
2.  Authenticate을 클릭합니다.

    인증이 종료되고 터미널로 돌아가 작업을 계속할 수 있습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/auth\_image\_1.gif)

### 토큰으로 인증

1. [your Snyk account](https://app.snyk.io/account)를 방문하십시오.
2. **General Account Settings**로 이동하여 token을 복사합니다.
3. token 필드에서 **click to show**를 클릭한 다음 API token을 복사합니다.
4. CLI에서 `snyk config set api=XXXXXXXX`를 실행합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/auth\_image\_2.png)

{% hint style="info" %}
maven 플러그인 중에 개인 API token을 사용합니다.
{% endhint %}
