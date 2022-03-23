# CLI 도구를 사용하여 Helm Charts 테스트 진행

Helm 템플릿을 Kuberenetes 매니페스트 파일로 렌더링한 다음 Snyk CLI에서 `snyk iac` 명령을 사용하여 Helm Charts를 스캔합니다.

예를 들어 `./helm` 디렉토리에 Helm 프로젝트가 있는 경우 다음 명령을 실행하여 템플릿 파일을 `./output`디렉토리로 출력합니다.

{% tabs %}
{% tab title="macOS/Linux/Unix" %}
```
helm template ./helm --output-dir ./output
snyk iac test ./output
```
{% endtab %}

{% tab title="Windows PowerShell" %}
```
helm template .\helm\ --output-dir .\output\
snyk iac test .\output\
```
{% endtab %}
{% endtabs %}

unix 기반 터미널의 경우 `Helm template`의 output을 단일 파일로 직접 연결할 수도 있습니다.

```
helm template ./helm > output.yaml
snyk iac test output.yaml
```

현재 Snyk CLI는 표준 입력에서 읽을 수 없지만 이 기능은 연구하고 있는 기능입니다.
