# Snyk API 토큰 취소 및 재생성

{% hint style="info" %}
API 토큰이 취소되면 해당 키를 사용하는 모든 통합이 즉시 작동을 중지합니다. 조심해서 진행하십시오!
{% endhint %}

API 토큰이 유출된 것으로 의심될 경우 이를 취소하고 대신 사용할 새 토큰을 생성하는 것이 좋습니다.

Snyk 사용자 API 토큰을 취소하려면 [app.snyk.io/account](https://app.snyk.io/account)에서 Snyk 웹 UI의 User Account Settings로 이동하십시오.

![](<../../.gitbook/assets/image (11).png>)

API 토큰을 해지하려면 **Revoke & Regenerate** 버튼을 클릭하십시오. 대신 새로운 토큰이 생성됩니다. 이제 새로 생성된 API 토큰을 가져와 이전 키를 사용한 통합을 업데이트할 수 있습니다.
