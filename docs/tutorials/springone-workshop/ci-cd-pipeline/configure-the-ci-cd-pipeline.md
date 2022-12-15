# Secret 추가

## Secret 추가

1. 브라우저를 사용하여 Github SPC 리포지토리를 열고 보라색 원을 따라 Secret을 추가합니다. (이미지 1)
2. Docker 허브 및 Snyk API 토큰에 대한 Secret을 추가합니다.

{% hint style="info" %}
Docker Hub Secret은 Docker Hub에서 사용할 수 있습니다. profile-> account settings->security에서. 필요한 경우 새 토큰을 만듭니다.
{% endhint %}

Snyk API 토큰은 무료 계정을 사용할 때 개인 토큰입니다. 토큰을 검색하는 방법에 대한 자세한 내용은 [Sync CLI 인증](../developer-environment-and-snyk/snyk-authenticate-using-cli.md#authenticate-with-your-token)을 참조하십시오.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/add\_secrets.png)

Secret을 생성하면 다음과 같이 표시됩니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/screen-shot-2020-08-22-at-11.37.20-am.png)
