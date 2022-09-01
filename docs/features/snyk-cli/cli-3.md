# 계정으로 CLI 인증

Snyk 계정에 사용할 Snyk CLI를 연결하려면 먼저 시스템을 인증해야 합니다. 이 단계에서는 저장소 권한이 필요하지 않으며 이메일 주소만 있으면 됩니다. 인증을 마치면 CLI를 사용하여 [시작](cli.md)할 수 있습니다. \
다음을 인증할 수 있습니다:

* CLI에서 `snyk auth`를 실행하여 브라우저를 통해 [인증 command 도움말](cli-command/undefined.md)을 참조하십시오.
* API 토큰 사용
* `SNYK_TOKEN` 환경 변수 사용은 [Snyk CLI 구성](snyk-cli.md)을 참조하십시오. CI/CD 환경에서 SNYK\_TOKEN을 사용합니다.

API 토큰을 사용하여 인증하려면:

1. [Snyk 계정](https://app.snyk.io/login?redirectUri=L2FjY291bnQ%3D\&from=snyk\_auth\_link)으로 이동합니다(**계정 설정** > **API 토큰** 섹션).
2. **KEY** 필드에서 **클릭하여 표시**합니다. 그런 다음 API 토큰을 선택하고 복사합니다. 스크린샷이 나옵니다.
3. CLI에서 `snyk auth [<API_TOKEN>]` 또는 `snyk config set api=<token>`을 실행합니다. `<API_TOKEN>`은 Snyk API에 의해 검증됩니다.

![Snyk 계정 설정, API 토큰](../../.gitbook/assets/spaces\_-MdwVZ6HOZriajCf5nXH\_uploads\_git-blob-0b8b145c9440bf28748591963d82d378b069290d\_API-token-CLI-auth-details-22-01.png)
