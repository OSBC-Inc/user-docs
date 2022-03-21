# CLI를 통한 Snyk Code 사용

{% hint style="info" %}
조직에 Snyk Code가 활성화되어 있는지 확인하십시오. 자세한 내용은 [Snyk Code 시작하기](../getting-started-with-snyk-code.md)를 참조하십시오.
{% endhint %}

Snyk Code용 Snyk [CLI](../../../features/snyk-cli/)(Command Line Interface)는 로컬 컴퓨터에서 코드의 보안 결함을 찾고 수정하는 데 도움이 됩니다.

CLI 를 사용하려면 먼저 CLI를 [설치](../../../features/snyk-cli/install-the-snyk-cli/)한 후 [인증](../../../features/snyk-cli/commands/auth.md)해야 합니다.

## 프로젝트 또는 폴더 테스트

현재 폴더를 테스트하려면 매개변수 없이 `snyk code test`를 실행하십시오.

다른 컨텍스트를 테스트하려면 파일이나 폴더의 경로를 파라미터로 하여 `snyk code test <my-folder-path>`를 실행하십시오.

제공된 폴더 내의 모든 하위 폴더도 스캔됩니다.

### "Not supported" 메시지

{% hint style="danger" %}
**Snyk Code is not supported for org** _**your.org**_

Snyk Code용 CLI를 사용하려면 최소 1.716.0 버전이 필요합니다.
{% endhint %}
