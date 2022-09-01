# Snyk CLI 구성

[환경 변수](snyk-cli.md#undefined)를 사용하여 Snyk CLI를 구성할 수 있습니다. 변수를 설정하여 [Snyk API에 연결하도록 Snyk CLI를 구성](snyk-cli.md#snyk-api)할 수도 있습니다.

## 환경 변수

다음 환경 변수를 설정하여 CLI 설정을 변경할 수 있습니다.

`SNYK_TOKEN`

Snyk 구성 설정(`~/.config/configstore/snyk.json`)에서 사용할 수 있는 토큰을 재정의할 수 있습니다. CI/CD 환경에서 `SNYK_TOKEN`을 사용합니다. `SNYK_TOKEN`을 설정한 후 CLI를 사용하여 [시작](cli.md)할 수 있습니다..

계정 토큰을 가져오는 방법에 대한 정보는 [계정으로 CLI 인증](cli-3.md)을 참조하십시오. 서비스 계정을 사용하여 인증할 수도 있습니다. 자세한 내용은 [서비스 계정](../integrations/managing-integrations/service-accounts.md)을 참조하세요. 추가 정보는 [타사 도구에 대한 인증](../user-and-group-management/authentication/authentication-for-third-party-tools.md)을 참조하십시오.

`SNYK_CFG_<KEY>`

snyk 구성 옵션으로도 사용할 수 있는 모든 키를 재정의할 수 있습니다.

예를 들어, `SNYK_CFG_ORG=myorg` 는 `config`의 기본 조직 옵션을 "myorg"로 재정의합니다.

`SNYK_REGISTRY_USERNAME`

컨테이너 명령의 경우 컨테이너 레지스트리에 연결할 때 사용할 사용자 이름을 지정합니다. `--username` 플래그를 사용하면 이 값이 무시됩니다. Docker가 있는 경우 로컬 Docker 바이너리 자격 증명을 위해 무시됩니다.

`SNYK_REGISTRY_PASSWORD`

컨테이너 명령의 경우 컨테이너 레지스트리에 연결할 때 사용할 비밀번호를 지정하십시오. `--password` 플래그를 사용하면 이 값이 무시됩니다. Docker가 있는 경우 로컬 Docker 바이너리 자격 증명을 위해 무시됩니다.

## Snyk API에 연결하기 위한 구성

기본적으로 Snyk CLI는 `https://snyk.io/api/v1`에 연결합니다.

`SNYK_API`

Snyk 요청에 사용할 API 호스트를 설정합니다. 온프레미스 인스턴스 또는 프록시 서버를 사용할 때 유용합니다. `http` 프로토콜로 설정하면 `SNYK_HTTP_PROTOCOL_UPGRADE`가 `0`으로 설정되지 않는 한 CLI가 요청을 `https`로 업그레이드합니다.

`SNYK_HTTP_PROTOCOL_UPGRADE=0`

값을 `0`으로 설정하면 `http` URL을 대상으로 하는 API(및 CLI) 요청이 `https`로 업그레이드되지 않습니다. 프로토콜이 설정되지 않은 경우 기본 동작은 이러한 요청을 `http`에서 `https`로 업그레이드하는 것입니다. 이는 예를 들어 역방향 프록시에 유용합니다.

`HTTPS_PROXY` and `HTTP_PROXY`

`https` 및 `http` 호출에 사용할 프록시를 지정할 수 있습니다. `HTTPS_PROXY`의 `https`는 `https` 프로토콜을 사용하는 요청이 이 프록시를 사용함을 의미합니다. 프록시 자체는 `https`를 사용할 필요가 없습니다.

`SNYK_DISABLE_ANALYTICS=1`

모든 Snyk CLI 분석을 비활성화합니다.

`SNYK_OAUTH_TOKEN=<OAuth token>`

확인에 필요한 경우 OAuth 토큰을 지정합니다.

자세한 내용은 [How can I use Snyk behind a proxy?](https://support.snyk.io/hc/en-us/articles/360000925358-How-can-I-use-Snyk-behind-a-proxy-) 를 참조하십시오.
