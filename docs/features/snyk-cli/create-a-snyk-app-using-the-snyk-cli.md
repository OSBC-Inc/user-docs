# Snyk CLI를 사용하여 Snyk 앱 생성

{% hint style="warning" %}
모든 `apps`의 하위 command는 `--experimental` 플래그 뒤에서만 액세스할 수 있으며 동작은 사전 통지 없이 언제든지 변경될 수 있습니다. 모든 command를 주의해서 사용하십시오
{% endhint %}

Snyk CLI를 사용하여 `snyk apps create`를 실행하여 [Snyk Apps](https://github.com/snyk/user-docs/tree/5e52535b78618f57eda40eb08fc8fbf91e16f1f0/docs/features/integrations/snyk-apps)를 생성할 수 있습니다.

옵션을 사용하여 Snyk CLI에 전달하거나 `--interactive` 모드(예: `snyk apps --experimental --interactive`)를 사용하여 Snyk 앱 관련 데이터를 전달할 수 있습니다.

모든 `Snyk Apps` 관련 하위 command는 최상위 앱 command 아래 그룹화됩니다(예: `snyk apps create`).

## snyk 앱의 하위 command

`snyk apps` command에서 사용 가능한 모든 하위 command에 대해 알아보려면 `--help` 옵션을 사용하십시오(예: `snyk apps --help`).

### snyk 앱 옵션

`--interactive`

대화식 모드에서 command를 사용합니다.

`--org=<ORG_ID>`

Snyk 앱을 생성할 `<ORG_ID>`를 지정합니다. `create` command에 필요합니다.

`--name=<SNYK_APP_NAME>`

인증 흐름 중에 사용자에게 표시될 Snyk 앱의 이름입니다. `create` command에 필요합니다.

`--redirect-uris=<REDIRECT_URIS>`

쉼표로 구분된 리디렉션 URI 목록입니다. 이것은 인증 후 콜백을 허용하는 리디렉션 URI 목록을 형성합니다. `create` command에 필요합니다.

`--scopes=<SCOPES>`

Snyk 앱에 필요한 쉼표로 구분된 범위 목록입니다. 이는 앱이 승인 중에 요청할 수 있는 범위 목록을 형성합니다. `create` command에 필요합니다.

### 예

Snyk 앱 만들기

`snyk apps create --experimental --org=48ebb069-472f-40f4-b5bf-d2d103bc02d4 --name='My Awesome App' --redirect-uris=https://example1.com,https://example2.com --scopes=apps:beta`

또는

`snyk apps create --experimental --interactive`
