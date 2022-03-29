# CLI 출력 이해

Snyk은 제공된 구성 파일에서 Issue를 분석하고 CLI에서 직접 Issue를 해결하는 방법에 대한 조언을 제공합니다.

예를 들어, Terraform 파일을 스캔합니다.

```
snyk iac test aws_api_gateway_stage_logging.tf
```

다음 스크린샷과 같이 출력을 제공할 수 있습니다.

![](../../../.gitbook/assets/screenshot-2021-09-28-at-19.58.22.png)

이 예제는 Terraform 파일을 스캔한 결과이지만 이 가이드는 Kubernetes 또는 CloudFormation을 포함한 모든 파일 형식에 적용됩니다.

**심각도별로 정렬된 취약점 목록이 출력**되며, 각 취약점은 다음과 같이 자세히 설명할 수 있습니다.

**A clear heading line** - 탐지된 Issue, 해당 Issue의 심각도 및 특정 Issue에 대한 Snyk 정책 ID를 지정합니다.

**Location** - Issue가 확인된 구성 파일 내의 속성 경로입니다. 자세한 내용은 아래 예를 참조하십시오.

**Example**

![](../../../.gitbook/assets/screenshot-2021-09-28-at-20.00.36.png)

Issue의 경로는 다음과 같습니다.

```
resource > aws_api_gateway_stage[denied] > access_log_settings
```

다음 코드에서는 1번째 줄이 `access_log_settings` 필드가 누락된 "denied"라는 이름의 `aws_api_gateway_stage` 블록의 내용을 나타내는 것을 볼 수 있습니다.

{% code title="aws_api_gateway_stage_logging.tf" %}
```
resource "aws_api_gateway_stage" "denied" {
  xray_tracing_enabled = true
}
```
{% endcode %}
