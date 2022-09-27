# 인증을 위한 SSO(Single Sign-On) 설정

{% hint style="info" %}
**기능 가용성**\
이 기능은 Business 및 Enterprise 고객이 사용할 수 있습니다. 자세한 내용은 [요금제](https://snyk.io/plans/)를 참조하세요.
{% endhint %}

### 소개

회사의 기존 ID 관리 시스템을 활용하고 직원이 회사 ID를 사용하여 Snyk에 로그인하도록 할 수 있습니다. 이렇게 하면 사용자에게 Snyk을 더 쉽게 프로비저닝할 수 있습니다. 또한 그룹 및 조직 멤버십, 역할 기반 액세스 등을 위한 더 깊은 통합을 허용합니다.

Snyk can integrate with any SAML-based and OpenID Connect (OIDC)-based SSO, as well as ADFS. You can also use your Enterprise Identity Provider for SSO, including [Azure AD](https://docs.microsoft.com/en-us/azure/active-directory/fundamentals/active-directory-whatis) and [Google G Suite](https://community.snowflake.com/s/article/configuring-g-suite-as-an-identity-provider). Read more about SAML in [the Auth0 documentation](https://auth0.com/docs/protocols/saml).

Snyk는 모든 SAML 기반 및 OpenID Connect(OIDC) 기반 SSO 및 ADFS와 통합할 수 있습니다. [Azure AD](https://docs.microsoft.com/en-us/azure/active-directory/fundamentals/active-directory-whatis) 및 [Google G Suite](https://community.snowflake.com/s/article/configuring-g-suite-as-an-identity-provider)를 비롯한 SSO용 엔터프라이즈 ID 공급자를 사용할 수도 있습니다. [Auth0 documentation](https://auth0.com/docs/protocols/saml)에서 SAML에 대해 자세히 알아보세요.

### 사용자 인증 및 프로비저닝

SSO를 구성하면 사용자가 이전에 자신의 계정을 생성한 경우에도 SSO를 통해 처음 로그인할 때 새 Snyk 계정이 프로비저닝됩니다.

로그인 프로세스에는 다음 단계가 포함됩니다:

1. 사용자가 로그인을 위해 Snyk.io에서 SSO를 선택하면 요청한 ID 제공업체로 리디렉션되고 인증됩니다.
2. ID 제공자는 이 인증을 Snyk 서버에 전달하고 각 사용자를 생성하기 위해 관련 데이터를 Snyk에 보냅니다.
3. Snyk은 해당 사용자의 디렉토리를 확인합니다.
4. 사용자가 이미 구성된 경우 Snyk은 적절한 액세스를 활성화합니다. 새 사용자의 경우 Snyk은 사용자를 디렉터리에 추가한 다음 적절한 액세스 권한이 있는 Snyk.io로 리디렉션합니다.

### 참조 사항

* 학습: [SSO, authentication and user provisioning](http://training.snyk.io/learn/course/sso/authentication-to-snyk/an-overview-of-authentication-and-provisioning?page=1)
