# 인증 관리

Snyk은 개인 계정 인증을 위해 또는 서비스 계정을 통합하기 위한 자격 증명 대신 타사 개발자 도구와의 통합을 가능하게 하는 API 토큰을 제공합니다.

{% hint style="info" %}
인증 목적을 위해 ID 제공자는 **저장소에 대한 액세스를 요구하지 않고** 이메일 주소만 요구합니다.
{% endhint %}

Snyk을 사용하면 다음 ID 제공자 중 하나를 인증에 사용할 수 있습니다:

* GitHub
* Bitbucket
* Google
* Azure
* Single Sign-On (SSO) - [setting-up-sso-for-authentication](../setting-up-sso-for-authentication/ "mention") 참조
* DockerID

{% hint style="info" %}
**기능 가용성**

Single sign-on은 엔터프라이즈 및 비즈니스 플랜에서 사용할 수 있습니다. 자세한 내용은 [요금제](https://snyk.io/plans/)를 참조하세요.
{% endhint %}

{% hint style="info" %}
Snyk 계정을 처음 생성할 때 등록한 공급자와 다른 공급자로 로그인하면 별도의 새 Snyk 계정이 생성됩니다.
{% endhint %}
