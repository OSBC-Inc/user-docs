# Snyk Code CLI 결과 필터링 및 내보내기

### 특정 심각도 수준 이상의 문제만 표시

다음과 같이 입력합니다.

```
snyk code test <folder> --severity-threshold=<low|medium|high>
```

예를 들어 심각도 값이 **medium** 이상인 결과만 표시하려면 다음과 같이 하십시오.

```
snyk code test ./my-proj --severity-threshold=medium
```

### 테스트 형식을 JSON으로 출력

다음과 같이 입력합니다.

```
snyk code test <folder> --json
```

이 기능은 결과의 스냅샷을 로컬에 저장하거나 보고서 및 추가 분석을 위해 다른 도구로 처리하려는 경우에 유용할 수 있습니다.

예를 들어 CLI에서 다음과 같이 입력합니다.

```
snyk code test ./my-proj --json
```

### 테스트 형식을 SARIF로 출력

{% hint style="info" %}
SARIF는 정적 분석 도구의 출력을 위한 개방형 표준입니다. 자세한 내용은 [official SARIF page](https://sarifweb.azurewebsites.net)를 참조하십시오.
{% endhint %}

다른 도구에서 분석할 수 있도록 테스트 결과를 SARIF 파일로 보고 저장할 수 있습니다.

```
snyk code test ./my-proj --sarif
```

또는 파일에 저장하려면 다음과 같이 실행할 수 있습니다.

```
snyk code test ./my-proj --sarif-file-output=snyk.sarif
```
