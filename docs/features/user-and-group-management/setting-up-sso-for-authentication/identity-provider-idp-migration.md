# Identity Provider (IdP) migration

레거시 IdP에서 새 IdP로 마이그레이션할 때 새 IdP 메타데이터 정보를 Snyk에 제출해야 합니다.

To migrate identity providers:

Identity Provider를 migrate 하려면:

1. [SSO resources](set-up-snyk-single-sign-on-sso.md#resources)에서 올바른 워크시트를 다운로드합니다.
2. IdP 메타데이터 정보로 워크시트 작성
3. 워크시트 제출(지원 티켓을 올리려면 [지원 팀에 문의](https://support.snyk.io/hc/en-us/requests/new))

Snyk 내에서 새 사용자가 생성되는 것을 방지하려면 SAML 프로토콜을 유지 관리하고 동일한 엔티티 ID와 ACS URL을 모두 사용해야 합니다. SAML 프로토콜을 변경하는 경우 [지원 팀에 문의](https://support.snyk.io/hc/en-us/requests/new)[https://support.snyk.io/hc/en-us/requests/new](https://support.snyk.io/hc/en-us/requests/new)하십시오.

이 작업이 완료되면 지원 팀에서 귀하에게 연락하여 업데이트된 메타데이터가 새 IdP를 통해 액세스 권한을 부여했는지 확인합니다.
