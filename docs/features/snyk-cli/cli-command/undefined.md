# 인증

## 사용법

`snyk auth [<API_TOKEN>] [<OPTIONS>]`

## 설명

`snyk auth`명령은 시스템을 인증하여 Snyk CLI를 Snyk 계정과 연결합니다

`$ snyk auth`를 실행하면 Snyk 계정에 로그인하고 인증하라는 메시지가 포함된 브라우저 창이 열립니다. 이 단계에서는 저장소 권한이 필요하지 않으며 이메일 주소만 있으면 됩니다.

인증이 완료되면 CLI 사용을 시작할 수 있습니다. [CLI 시작하기](../cli.md) 참조

## 값

일부 환경 및 구성에서는 `<API_TOKEN>`을 사용해야 합니다. [계정으로 CLI 인증](../cli-3.md) 참조

값은 사용자 토큰 또는 서비스 계정일 수 있습니다. [서비스 계정](../../integrations/managing-integrations/service-accounts.md) 참조

CI/CD 환경에서는 `SNYK_TOKEN` 환경 변수를 사용합니다. [Snyk CLI 구성](../snyk-cli-1.md) 참조

이 환경 변수를 설정한 후 CLI 명령을 사용할 수 있습니다.

## 디버그

`-d` 옵션을 사용하여 디버그 로그를 출력합니다.
