# 셀프 서비스 SSO (Single Sign-On)

SSO에 SAML을 사용하는 비즈니스 플랜의 그룹 관리자는 스스로 Snyk Single Sign-on을 구성할 수 있습니다.

새 사용자가 할당될 위치를 나타내는 그룹 및 조직이 하나 이상 있는지 확인하십시오. [그룹, 조직 및 사용자](https://github.com/snyk/user-docs/blob/118bd8f19001bd64415f0ce63897f568c4b5327a/docs/introducing-snyk/snyks-core-concepts/groups-organizations-and-users.md)를 참조하십시오.

### SSO에 SAML 사용

#### 프로세스 개요

ID 공급자(IdP)와 Snyk 간의 신뢰를 설정하는 프로세스에는 그룹 관리자의 몇 가지 단계가 필요합니다.

1. 화면에 표시되는 Snyk 환경 및 사용자 속성에 대한 세부 정보를 사용하여 **IdP(identity provider)**를 구성합니다.
2. 그룹 SSO 설정 페이지에서 **IdP(identity provider)**의 **SAML 속성**을 입력합니다.
3. Snyk SSO 설정을 구성하고 구성원이 로그인하는 방법을 선택합니다.
4. SSO 로그인을 확인하여 로그인 프로세스가 올바르게 작동하는지 확인합니다.

{% hint style="info" %}
Snyk와 회사 네트워크 모두에서 SSO가 구성된 후 Snyk, Auth0(Snyk 대신) 및 네트워크 간에 신뢰 관계가 설정됩니다. 민감한 데이터는 암호화되어 사용자 로그인을 활성화할 목적으로만 Auth0에 저장됩니다.
{% endhint %}

**사용자 로그인**

사용자는 로그인할 때 Snyk에 프로비저닝됩니다(see [choose-a-provisioning-option.md](choose-a-provisioning-option.md "mention")). 새 사용자 역할이 그룹 구성원으로 선택되면 관리자가 적절한 조직에 추가할 때까지 조직 목록만 표시됩니다.

### Step 1. **IdP(identity provider) 구성**

Snyk과 신뢰를 설정하려면 **IdP(identity provider)**에 엔티티 ID, ACS URL 및 서명 인증서를 추가하십시오.

* **Entity ID**는 Snyk를 SAML 엔터티 또는 서비스 공급자로 고유하게 식별하는 URL입니다. **참고로 기본 엔터티 ID는 기본값이 설정되어 있지 않으므로 수동으로 확인해야 합니다.**
* **ACS(Assertion Consumer Service)**는 네트워크의 사용자와 Snyk 간의 통신을 가능하게 하기 위해 ID 제공자의 요청을 수신하는 Snyk 네트워크의 끝점입니다. 이 URL을 회신 URL이라고도 합니다.
* **Signing certificate**는 신뢰 관계를 유지하는 데 필요한 서버에 저장된 Snyk 인증서입니다. 여기에는 인증에 필요한 암호화 키가 포함되어 있습니다.

**그룹 관리자**는 여기에서 ID 공급자(IdP)와의 연결을 설정하는 데 필요한 Snyk 세부 정보를 찾을 수 있습니다.

그룹의 그룹 개요에 액세스하려면, Settings [![](https://github.com/snyk/user-docs/raw/118bd8f19001bd64415f0ce63897f568c4b5327a/docs/.gitbook/assets/image%20\(70\).png)](https://github.com/snyk/user-docs/blob/118bd8f19001bd64415f0ce63897f568c4b5327a/docs/.gitbook/assets/image%20\(70\).png) > **SSO** 클릭 합니다.:

![Group settings](<../../../.gitbook/assets/spaces\_-MdwVZ6HOZriajCf5nXH\_uploads\_git-blob-7c963a7698c8f188b6bdb5c4607f2ff6342f2fc2\_Screenshot 2022-02-24 at 14.32.24.png>)

아이덴티티 공급자의 정보를 Snyk에 매핑하려면 사용자 속성의 이름을 다음과 같이 지정합니다(동일한 대문자 및 철자 사용).

| 속성       | 설명                             |
| -------- | ------------------------------ |
| email    | 사용자의 이메일 주소                    |
| name     | 인증할 사람의 이름                     |
| username | IdP(identity provider)의 사용자 이름 |

Okta의 예는 다음과 같습니다:

![SAML 속성 문](<../../../.gitbook/assets/spaces\_-MdwVZ6HOZriajCf5nXH\_uploads\_git-blob-87aed5a7567d270144716af224ee3edca23f4ed0\_Screenshot 2022-02-24 at 14.19.18.png>)

{% hint style="warning" %}
사용자 속성이 일치하지 않으면 SSO에 대한 Snyk 구성이 작동하지 않습니다.
{% endhint %}

이러한 속성에 대한 자세한 내용은 3단계. [Snyk SSO 설정](self-serve-single-sign-on-sso.md#step-3.-snyk-sso-settings)을 참조하십시오.

### Step 2. SAML 속성 입력

ID 제공자가 Snyk를 확인하도록 설정했으면 이제 ID 제공자 및 조직에서 다음 정보를 얻으십시오.

서비스 공급자 측에서 신뢰를 설정하려면 **create a connection**을 클릭합니다.

![Create a connection](<../../../.gitbook/assets/spaces\_-MdwVZ6HOZriajCf5nXH\_uploads\_git-blob-7844d49ff6a872addf0ac691c6861241c257e71e\_image (115).png>)

아래 양식에 SAML 속성을 제공하십시오.

* **Sign in URL** (필수): Identity Provider 로그인 URL
* **Sign out URL**: 사용자가 Snyk에서 로그아웃할 때 URL 리디렉션, 권장
* **X509 signing certificate** (필수): ID 제공자 공개 키입니다. ID 공급자로부터 인증서를 다운로드하여 여기에 붙여넣습니다. 시스템은 이를 **Base64 형식**으로 인코딩합니다.
* SSO 액세스가 필요한 **이메일 도메인 및 하위 도메인** (필수)
* **Protocol binding**: HTTP-POST가 권장됩니다. HTTP 리디렉션도 지원됩니다.
* **IdP-Initiated workflow**: 아이덴티티 공급자에 Snyk 타일을 추가하려면 이 옵션을 활성화합니다.\
  **Note**: IdP 시작 SSO 동작은 [보안 위험](https://auth0.com/docs/authenticate/protocols/saml/saml-sso-integrations/identity-provider-initiated-single-sign-on#risks-and-considerations)을 수반하므로 권장하지 않습니다. 위험은 IdP 측에서 설명되며 이 옵션을 활성화하기 전에 이해해야 합니다.

![SAML 속성 입력](<../../../.gitbook/assets/spaces\_-MdwVZ6HOZriajCf5nXH\_uploads\_git-blob-9a29beafbedae069ce872bc08404b22ff66b72c5\_Screenshot 2022-02-24 at 14.40.24.png>)

세부 정보를 입력한 후 **Save Changes**을 클릭합니다. 오류가 있으면 Snyk가 강조 표시합니다. 언제든지 SAML 속성을 편집하고 변경 사항을 저장할 수 있으며 SSO 연결에 즉시 반영됩니다.

### Step 3. Snyk SSO 설정

이제 성공 배너에서 아래 **Configure Snyk SSO settings**를 클릭하여 설정을 완료합니다.

![아래에서 Snyk SSO 설정 구성](<../../../.gitbook/assets/spaces\_-MdwVZ6HOZriajCf5nXH\_uploads\_git-blob-478495d5923fb488fd08c7cfd74a529a9fc44d75\_Screenshot 2022-02-24 at 15.37.44.png>)

새 사용자의 역할 선택 ([choose-a-provisioning-option.md](choose-a-provisioning-option.md "mention") 참조):

![사용자 역할 선택](<../../../.gitbook/assets/spaces\_-MdwVZ6HOZriajCf5nXH\_uploads\_git-blob-9299bcf27310f208fca09004da345c02a7d147f8\_Screenshot 2022-02-24 at 15.28.30.png>)

**프로필 속성 값**은 사용자의 SAML 페이로드 데이터를 매핑하여 Snyk가 적절한 이메일, 이름 및 userName을 수신하도록 하는 데 사용됩니다. SAML 페이로드의 원시 json에 있는 정확한 키여야 합니다.

값은 **nameIdAttributes.value**로 시스템에 의해 자동으로 채워집니다.

{% hint style="info" %}
SSO 관리자에게 문의하여 ID 공급자가 구성될 때 이메일 주소, 이름(표시 이름, 이름 + 성) 및 사용자 이름(고유 식별자)이 표시되는 방식을 결정하는 것이 좋습니다. ([#step-1.-configure-your-identity-provider](self-serve-single-sign-on-sso.md#step-1.-configure-your-identity-provider "mention")에 설명된 대로)
{% endhint %}

선택이 끝나면 **Save Changes**을 클릭하여 SSO 구성을 완료합니다.

### 4. SSO 로그인 확인

SSO 설정이 성공적으로 저장되면 설정한 SSO 연결 화면에 표시된 직접 로그인 URL을 클릭합니다. 그리고 Snyk Group에 로그인할 수 있는 IDP로 이동합니다.

![직접 로그인 URL](<../../../.gitbook/assets/spaces\_-MdwVZ6HOZriajCf5nXH\_uploads\_git-blob-f4ade072ec1aee46903402ad1d286e5dd2393244\_Screenshot 2022-02-24 at 16.00.49.png>)

또는 시크릿 모드에서 snyk에 로그인하여 쿠키가 간섭하는 것을 방지하고 SSO 로그인이 작동하는지 확인할 수 있습니다.

(직접 SSO 링크:[https://app.snyk.io/login/sso](https://app.snyk.io/login/sso)) 또는:

1. [https://snyk.io](https://snyk.io)
2. 로그인
3. SSO
4. 이메일 주소를 입력하십시오.
5. 계속해서 IDP로 이동하여 로그인합니다.
