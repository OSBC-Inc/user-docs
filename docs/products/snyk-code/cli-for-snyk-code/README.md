# CLI를 통해 Snyk Code 사용

{% hint style="info" %}
조직에 Snyk Code가 활성화되어 있는지 확인하십시오. 자세한 내용은 [Getting started with Snyk Code](../../../getting-started/getting-started-snyk-products/getting-started-with-snyk-code.md#stage-1-enable-snyk-code)를 참조하십시오.
{% endhint %}

Snyk Code용 Snyk Command Line Interface([CLI](../../../features/snyk-cli/))는 로컬 컴퓨터에서 코드의 보안 결함을 찾고 수정하는 데 도움이 됩니다.&#x20;

## Snyk CLI 설치

다음 중 하나를 사용하여 Snyk CLI를 설치할 수 있습니다:

* npm: `npm install -g snyk`
* Homebrew: `brew tap snyk/tap && brew install snyk`
* Scoop: `scoop bucket add snyk <https://github.com/snyk/scoop-snyk>`
* GitHub에서 사용 가능한 [**manual installer**](https://github.com/snyk/snyk/releases)

자세한 설치 지침 및 옵션은 [Install the Snyk CLI](../../../features/snyk-cli/install-the-snyk-cli/)를 참조하십시오.

## 인증

After the installation, authenticate with Snyk to test your image, running snyk auth from the CLI:

```
snyk auth
```

인증에 대한 자세한 내용은 [Authenticate the CLI with your account](../../../features/snyk-cli/install-the-snyk-cli/authenticate-the-cli-with-your-account.md)을 참조하십시오.

## 프로젝트 또는 폴더 테스트

현재 폴더를 테스트하려면 매개변수 없이 `snyk code test`를 실행하십시오.

다른 컨텍스트를 테스트하려면 파일이나 폴더의 경로를 매개변수로 하여 `snyk code test <my-folder-path>` 를 실행하십시오.

제공된 폴더 내의 모든 파위 폴더도 검색됩니다.

### "Not supported" 메시지

{% hint style="danger" %}
~~_**org**  **your.org**_~~**에서는 Snyk Code가 지원되지 않습니다.**

Snyk Code용 CLI를 사용하려면 최소 1.716.0 버전이 필요합니다.
{% endhint %}
