# Issue 무시

취약점이나 라이선스 Issue를 수정하고 싶지 않고 스캔 결과에서 해당 Issue를 보고 싶지 않다면 Snyk를 사용하여 일시적으로 또는 영구적으로 무시할 수 있습니다.

### Issue를 무시할 때

snyk.io UI, Snyk API, Snyk CLI 및 .snyk 파일을 사용하여 Issue를 무시하고 볼 수 있습니다.

보안 Issue를 무시하는 것이 기본 조치가 되어서는 안 되지만 때로는 필요합니다. 가장 좋은 방법은 취약점을 수정 또는 패치하거나 취약한 종속성을 제거하는 것이지만 여전히 Issue를 억제하려는 이유가 있을 수 있습니다. 예를 들어 Issue에 현재 수정 사항이 없는 경우 다음을 수행할 수 있습니다. 될 때까지 무시하십시오.

일부 Issue는 특정 프로젝트와 관련이 없습니다(예: 내부 서비스에 대한 DDOS 공격). 다른 경우 Issue에는 악용할 수 없도록 만드는 경로가 있습니다. 이러한 시나리오에서는 현재 취약점을 악용할 수 없지만 앞으로는 악용될 수 있으므로 여전히 Issue를 해결해야 합니다.

### UI의 Issue 무시

각 **Issue** 카드에는 Issue를 무시하려는 이유와 무시 기간을 선택할 수 있는 대화 상자가 열리는 무시 버튼이 있습니다.

![](<../../../.gitbook/assets/image (21).png>)

If you select **Ignore temporarily,** then you can check the **Until fix is available** checkbox:

**Ignore temporarily**를 선택하면 **Until fix is available** 확인란을 선택할 수 있습니다.

![](<../../../.gitbook/assets/image (19) (1).png>)

이렇게 하면 Issue가 수정되는 즉시 취약점이 다시 나타나며 선택적으로 Issue를 무시하는 이유에 대한 추가 세부정보를 제공할 수 있습니다. 현재 이 Issue에 사용할 수 있는 수정 사항이 없는 경우 기본적으로 선택되어 있습니다.

{% hint style="info" %}
무시 기간이 만료되거나 취약점이 수정될 수 있는 조건 중 하나라도 발생할 때까지 문제가 무시됩니다.
{% endhint %}

UI에서 Issue를 무시하면 무시한 사람이 표시되고 수정하거나 무시할 수 있습니다.

![](<../../../.gitbook/assets/image (14).png>)

### CLI의 Issue 무시

`snyk ignore` 명령을 사용하여 CLI를 통해 Issue를 억제할 수 있습니다.

`snyk ignore --id='npm:braces:20180219' --expiry='2018-04-01' --reason='testing'`

자세한 내용은 [Snyk CLI를 사용하여 취약성 무시](../../../snyk-cli/fix-vulnerabilities-from-the-cli/ignore-vulnerabilities-using-snyk-cli.md)를 참조하십시오.

`snyk ignore`를 사용하면 `.snyk` 정책 파일이 제공된 경로와 이유(제공된 경우)로 업데이트됩니다. 예를 들어:

```
'npm:moment:20170905':
- moment:
reason: The reason given
expires: '2017-12-29T16:10:16.946Z'
```

### CLI 또는 CI/CD에서 스캔, UI에서 무시

CLI(또는 CI/CD 실행)와 Snyk UI 간의 무시가 동기화됩니다. 따라서 순서 다음과 같습니다:

1. `snyk monitor`를 사용하여 프로젝트를 스캔하고 UI로 푸시합니다.
2. 스캔 결과를 보고 Issue를 무시하도록 선택합니다.
3. CI/CD 또는 CLI에서 `snyk test` 또는 `snyk monitor`를 실행할 때 문제가 무시됩니다.

예를 들어:

![](<../../../.gitbook/assets/image (15).png>)

UI에서 무시하기 전에 `snyk test`:

![](<../../../.gitbook/assets/image (18).png>)

UI에서 무시 후 `snyk test`:

![](<../../../.gitbook/assets/image (20).png>)

CLI 또는 CI/CD에서 `snyk monitor`로 가져온 프로젝트를 무시하는 경우 위의 내용이 사실인 것이 중요합니다.

SCM에서 가져온 동일한 저장소는 다른 프로젝트로 간주되며 SCM 프로젝트에 대한 무시는 CLI 또는 CI/CD의 `snyk test` 결과에 영향을 미치지 않습니다. SCM 및 CI 프로젝트는 두 개의 독립 실행형 프로젝트로 작동합니다.

### .snyk 파일 Issue 무시

모든 프로젝트에 대해 `.snyk` YAML 파일을 생성하여 취약점을 무시할 수 있습니다.

![](../../../.gitbook/assets/screen+shot+2017-05-10+at+11.16.57+am.png)

예를 들어 `fastreader`에서 SNYK ID가 [SNYK-RUBY-FASTREADER-20085](https://snyk.io/vuln/SNYK-RUBY-FASTREADER-20085)인 취약점을 2023년 1월 1일까지 "수정 사항 없음"으로 무시하려면 다음과 같이 작성합니다.

```
version v1.5.0
ignore:
    'SNYK-RUBY-FASTREADER-20085':
     - '* > fastreader':
      reason: 'No fix available'
      expires '2023-01-01T00:00:00.000Z'
```

자세한 내용은 [.snyk 파일](../../snyk-cli/undefined/.snyk.md)을 참조하십시오.

### 정책 조치 문제 무시

정책 규칙에 지정된 조건과 일치하는 모든 취약성을 무시하도록 [보안 정책](../security-policies/) 작업을 설정할 수 있습니다.

자세한 내용은 [보안 정책: 작업](../security-policies/security-policies-actions.md)을 참조하세요.

### Snyk 코드의 Issue 무시

[Snyk Code](../../../snyk-products/snyk-code/)의 경우 기능 무시는 다른 제품보다 광범위한 문제를 포착할 수 있습니다.

Snyk Code의 정적 코드 분석은 입력 코드를 **중간 표현**으로 변환하여 코드의 흐름을 포착하지만 일부 세부 사항은 추상화합니다. Snyk Code는 이 표현을 사용하여 코드를 리팩터링하거나 변수의 이름을 바꿀 때도 동일한 문제를 인식합니다.

따라서 Issue를 무시할 때 Snyk Code는 사소한 코드 변경에도 불구하고 코드의 여러 위치에서 발생하는 경우 해당 Issue를 무시할 수도 있습니다. 이렇게 하면 무시된 동일한 Issue가 있는 코드 조각에 대해 여러 중복 보고서가 표시되는 것을 방지할 수 있습니다.

예를 들어 다음 두 코드 조각(텍스트 차이에도 불구하고)은 변수 이름만 변경했기 때문에 동일한 문제를 통보합니다.

```
var fs = require('fs');
var logFileName = req.query.file || 'standard_log.log';
var logfile = fs.readFile(logFileName, "utf8", function(err, data) {...
```

```
var filesystem = require('fs');
var generalLogFileName = req.query.file || 'standard_log.log'; 
var handleLogFile = filesystem.readFile(generalLogFileName, "utf8", function(err, data) {...
```

Snyk Code에 대한 자세한 내용은[using-snyk-code-web.md](../../../products/snyk-code/using-snyk-code-web.md "mention") 를 참조하십시오.

### Snyk IaC의 Issue 무시

**snyk iac 테스트**와 함께 Snyk CLI를 사용하여 IaC 구성 파일을 스캔할 때 사용자와 관련이 없는 Issue는 무시할 수 있습니다.

IaC 구성 파일을 저장하는 작업 디렉토리의 루트에 저장되고 버전 관리되는[the-.snyk-file.md](../../../snyk-cli/test-for-vulnerabilities/the-.snyk-file.md "mention")를 사용하여 이 작업을 수행할 수 있습니다.

자세한 내용은[iac-ignores-using-the-.snyk-policy-file.md](../../../products/snyk-infrastructure-as-code/snyk-cli-for-infrastructure-as-code/iac-ignores-using-the-.snyk-policy-file.md "mention")를 참조하십시오.

### 무시 설정을 구성할 수 있는 인원 설정

취약성을 억제하는 것은 위험 수준을 수반하므로 이 기능을 관리자만 사용할 수 있도록 설정할 수 있습니다.:

1. organization settings > **General**으로 이동한 다음 무시 **Ignores**로 이동합니다.
2. **Issue를 무시하거나 Issue에 대한 무시 설정을 편집할 수 있는 기능**에서 **관리자 전용**을 선택합니다. 이것은 또한 CLI를 통해 추가되는 무시를 비활성화합니다.
3. **Require reason for each ignore** 아래에서 문제가 무시될 때 **추가 세부 정보** 필드를 필수 필드로 설정하도록 선택할 수도 있어 사용자가 무시할 때마다 이유를 입력할 수 있습니다.
4. **Update**를 클릭하여 변경합니다.

![](<../../../.gitbook/assets/Screenshot 2021-12-07 at 11.25.49.png>)

### 보고서에서 무시 사용

보고서 기능에 액세스할 수 있는 경우 조직의 프로젝트에서 얼마나 많은 Issue가 무시되었는지에 대한 개요와 이를 필터링하여 각 Issue를 드릴다운할 수 있는 옵션도 볼 수 있습니다. UI에서 Issue가 무시된 경우 추가 책임에 대한 크레딧을 포함하여 누가 Issue를 시작했는지 확인할 수 있습니다.

자세한 내용은 [보고서](../../../introducing-snyk/snyks-core-concepts/reporting.md)를 참조하십시오.
