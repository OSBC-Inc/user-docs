# Snyk SSO(Single Sign-On) 설정

개발자와 팀이 기존 SSO 공급자를 통해 Snyk에 쉽게 액세스할 수 있도록 싱글 사인온을 설정하여 프로젝트 상태를 확인하고 보고서를 보고 취약점을 해결하는 등의 작업을 수행할 수 있습니다.

Snyk과 ID Provider 간에 신뢰를 구축하는 데 필요한 정보는 사용 중인 SSO 유형에 따라 다릅니다.

새 사용자가 할당될 위치를 나타내는 그룹 및 조직이 하나 이상 있는지 확인하십시오. [그룹, 조직 및 사용자를](../../../introducing-snyk/snyks-core-concepts/groups-organizations-and-users.md) 참조하십시오.

{% hint style="info" %}
요청한 정보(아래에 자세히 설명)를 수집했으면 SSO 설정을 요청하기 위한 지원 티켓을 만드십시오.

SAML을 사용하는 비즈니스 플랜의 경우 그룹 관리자는 Snyk Single Sign-On을 구성할 수 있으며 이 [가이드](self-serve-single-sign-on-sso.md)에서는 단계를 자세히 설명합니다.
{% endhint %}

## 개요

IdP(ID Provider)와 Snyk 간의 신뢰를 설정하는 프로세스에는 SSO 관리자와 Snyk 지원 간에 조정된 몇 가지 개별 단계가 필요합니다.

* 고유한 ID Provider 플랫폼에서 Snyk 환경 및 사용자 속성에 대한 세부사항을 입력하십시오.
* IdP의 세부 정보를 Snyk에 제공합니다.
* 테스트할 사용자를 설정하고 해당 사용자의 사용자 이름과 암호를 Snyk에 보냅니다.
* Snyk에서 제공하는 링크를 사용하여 페이로드를 생성합니다.
* Snyk가 연결을 완료한 후 로그인 프로세스가 올바르게 작동하는지 확인하십시오.
* 사용자는 로그인할 때 Snyk에 프로비저닝됩니다. 초대가 필요한 경우 관리자가 적절한 조직에 추가할 때까지 사용자는 조직 목록만 볼 수 있습니다.

Snyk과 회사 네트워크 모두에서 SSO가 구성된 후 Snyk, Auth0(Snyk 대신) 및 네트워크 간에 신뢰 관계가 설정됩니다. 민감한 데이터는 암호화되어 사용자 로그인을 활성화할 목적으로만 Auth0에 저장됩니다.

각 유형의 SSO 연결에는 ID 공급자와 Snyk 간의 신뢰를 설정하기 위해 서로 다른 세부 정보가 필요합니다. 다음 섹션에서는 이러한 세부 정보를 설명합니다. 자세한 내용은 이 문서의 끝에 있는 리소스 섹션의 워크시트에도 포함되어 있습니다.

## SSO에 SAML 사용

Snyk와 신뢰를 설정하려면 ID 공급자에 엔티티 ID, ACS URL 및 서명 인증서를 추가하십시오.

* **Entity ID**는 Snyk를 SAML 엔터티 또는 서비스 공급자로 고유하게 식별하는 URL입니다. **참고로 기본 엔터티 ID는 기본값이 설정되어 있지 않으므로 수동으로 확인해야 합니다.**
* **ACS(Assertion Consumer Service)**는 네트워크의 사용자와 Snyk 간의 통신을 가능하게 하기 위해 ID 제공자의 요청을 수신하는 Snyk 네트워크의 끝점입니다. 이 URL을 회신 URL이라고도 합니다.
* **Signing certificate**는 신뢰 관계를 유지하는 데 필요한 서버에 저장된 Snyk 인증서입니다. 여기에는 인증에 필요한 암호화 키가 포함되어 있습니다.

Use these details to set up the connection with your Identity provider (IdP):

다음 세부 정보를 사용하여 IdP(Identity provider)와의 연결을 설정합니다:

| **세부 정보**           | **설**                                                                                                                                                                            |
| ------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Entity ID           | **urn:auth0:snyk:saml-**_**{customer\_name}**_ ({customer\_name}을 회사 이름으로 바꿉니다.)                                                                                                 |
| ACS URL             | [https://snyk.auth0.com/login/callback?connection=saml-](https://snyk.auth0.com/login/callback?connection=saml-)_**{customer\_name}**_ ({customer\_name}을(를) 회사와 동일한 이름으로 바꿉니다.) |
| Signing certificate | [https://snyk.auth0.com/pem](https://snyk.auth0.com/pem)                                                                                                                         |

Identity provider의 정보를 Snyk에 매핑하려면 사용자 속성의 이름을 다음과 같이 지정합니다(동일한 대문자 및 철자 사용):

| **속**        | **설**                   |
| ------------ | ----------------------- |
| **email**    | **사용자 이메일 주소**          |
| **name**     | **인증할 사람의 이름**          |
| **username** | ID provider**의 사용자 이름** |

사용자 속성이 일치하지 않으면 SSO에 대한 Snyk 구성에 더 많은 시간이 소요됩니다.

## Snyk에 제공할 SAML 정보

ID 공급자 및 조직에서 다음 정보를 얻습니다. 이 정보를 Snyk에 제공하여 서비스 제공자 측에서 신뢰를 구축하십시오.

| 정보                         | 설명                                                                               |
| -------------------------- | -------------------------------------------------------------------------------- |
| Sign-in URL                | ID provider 로그인 페이지의 URL                                                         |
| X509 Signing Certificate   | Base64 형식으로 인코딩된 ID provider 공개 키                                                |
| Sign-out URL               | 선택 사항이지만 권장 사항 - 사용자가 Snyk에서 로그아웃할 때마다 리디렉션되는 URL                                |
| User ID attribute          | 선택적 기본값은**http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier** |
| Protocol binding           | HTTP-POST가 권장되며 HTTP-Redirect도 지원됩니다.                                            |
| IdP initiated flow가 지원됩니까? | IdP initiated flow에는 보안 위험이 있으므로 권장되지 않습니다. 활성화하기 전에 위험을 이해했는지 확인하십시오.           |
| Email domains 와 subdomains | SSO에 액세스해야 하는 이메일 도메인 및 하위 도메인                                                   |

## SSO에 OIDC(OpenID Connect) 사용

ID provider와 Snyk 간의 연결에 OIDC를 사용하는 경우 ID provider에 콜백/리디렉션 URI 및 OAuth 권한 부여 유형을 추가하여 Snyk와의 신뢰를 설정합니다.

| 정보                     | 설명                                                                             |
| ---------------------- | ------------------------------------------------------------------------------ |
| Callback/Redirect URIs | [https://snyk.auth0.com/login/callback](https://snyk.auth0.com/login/callback) |
| OAuth Grant Type       | 암시(또는 uthorization Code)                                                       |

## Snyk에 제공할 OIDC 정보

ID provider 및 조직에서 다음 정보를 얻습니다. 이 정보를 Snyk에 제공하여 서비스 제공자 측에서 신뢰를 구축하십시오.

| 정보                         | 설명                                  |
| -------------------------- | ----------------------------------- |
| Issuer URL                 | 연결하려는 OpenID Connect 제공자의 검색 문서 URL |
| Client ID                  | 인증 서버의 고유한 공개 식별자                   |
| Client Secret              | IdP가 암시적 부여 유형을 허용하지 않는 경우에만 필요합니다. |
| Email domains 와 subdomains | SSO에 액세스해야 하는 이메일 도메인 및 하위 도메인      |

## Azure AD를 SSO로 사용 (App Registration/OIDC를 통해)

ID provider와 Snyk 간의 연결에 Azure AD를 사용하는 경우 Snyk와의 신뢰를 설정하려면 ID provider에 리디렉션 URI를 추가해야 합니다.

{% hint style="info" %}
인증 시 SCM 사용자 계정 이름 대신 Azure AD 이름을 사용하십시오. 그렇지 않으면 연결 오류가 발생할 수 있습니다.iption
{% endhint %}

| 정보            | 설명                                                                             |
| ------------- | ------------------------------------------------------------------------------ |
| Redirect URIs | [https://snyk.auth0.com/login/callback](https://snyk.auth0.com/login/callback) |

## Snyk에 제공할 Azure AD 정보

ID 공급자 및 조직에서 다음 정보를 얻습니다. 이 정보를 Snyk에 제공하여 서비스 제공자 측에서 신뢰를 구축하십시오.

| 정보                        | 설명                                                  |
| ------------------------- | --------------------------------------------------- |
| Client ID                 | 인증 서버의 고유한 공개 식별자                                   |
| Client Secret             | 승인된 요청자에게 토큰을 부여하는 권한 부여의 비밀                        |
| Microsoft Azure AD Domain | 개요에서 생성한 Snyk 앱에서 찾을 수 있는 디렉터리(테넌트) ID에 표시된 숫자 및 문자 |

## ADFS를 SSO로 사용

ID 공급자와 Snyk 간의 연결에 ADFS를 사용할 때 영역 식별자, 콜백 URL 및 서명 인증서를 ID 공급자에 추가하여 Snyk와의 신뢰를 설정하십시오.

| 정보               | **설명**                                                                         |
| ---------------- | ------------------------------------------------------------------------------ |
| Realm Identifier | **urn:auth0:snyk**                                                             |
| Callback URL     | [https://snyk.auth0.com/login/callback](https://snyk.auth0.com/login/callback) |
| Signing cert     | [https://snyk.auth0.com/pem](https://snyk.auth0.com/pem) (암호화가 아닌 서명으로 추가)     |

## Snyk에 제공할 ADFS 정보

ID 공급자 및 조직에서 다음 정보를 얻습니다. 서비스 제공자 측에서 신뢰를 구축하기 위해 이 정보를 Snyk에 제공합니다.

* ADFS URL 또는 Federation Metadata XML file

## Map Enterprise 사용자

Enterprise 플랜의 경우 Snyk은 새 사용자가 SSO를 사용하여 처음 로그인할 때 특정 조직 및 역할에 매핑할 수 있습니다. 이 옵션을 사용하려면 조직에 대한 특정 명명 규칙을 비롯한 추가 구성이 필요합니다.

고객 성공 관리자 및 Snyk 기술 서비스와 협력하여 이 SSO 옵션 구현을 준비하십시오.

## SSO 연결 완료

ID 제공자와의 연결을 설정하고 Snyk 지원에 필요한 세부 정보를 제공하면 Snyk에서 페이로드를 생성하기 위한 링크를 보냅니다.

Snyk은 생성된 페이로드를 사용하여 구성을 완료하므로 이 링크를 처음 클릭한 후 표시되는 오류 메시지는 무시하십시오.

Snyk이 구성을 완료하면 지원 에이전트는 쿠키가 로그인 프로세스를 방해하는 것을 방지하기 위해 시크릿 모드에서 로그인 페이지에 액세스하도록 요청합니다.

* 프로덕션 환경에 로그인하려면 [https://app.snyk.io/login/sso](https://app.snyk.io/login/sso)를 사용하십시오.
* 테스트 환경에 로그인하려면 [https://test.snyk.io](https://test.snyk.io)를 사용하십시오.

로그인을 완료하려면:

1. 이메일 주소를 입력합니.
2. **Continue to provider를** 선택합니다..
3. 다른 응용 프로그램에서와 마찬가지로 ID 공급자로 로그인합니다.
4. 그룹 관리자로 승격할 사용자를 Snyk 지원에 알리십시오.

## Resources

이 워크시트에는 ID 제공자에 입력할 정보와 Snyk 지원팀에 Single Sign-On을 요청하기 위해 티켓을 제출하기 전에 수집해야 하는 정보가 포함되어 있습니다.

{% file src="../../../.gitbook/assets/sso-azure-worksheet.pdf" %}

{% file src="../../../.gitbook/assets/sso-saml-worksheet.pdf" %}

{% file src="../../../.gitbook/assets/sso-adfs-worksheet.pdf" %}

{% file src="../../../.gitbook/assets/sso-oidc-worksheet.pdf" %}
