# 구성 파일 테스트

Snyk Infrastructure as Code를 사용하여 CLI에서 직접 구성 파일을 테스트할 수 있습니다.

CLI를 사용하여 Kubernetes, Terraform 및 CloudFomation 파일을 스캔할 수 있습니다.

아래에서 더 자세한 정보를 확인할 수 있습니다.

* [Terraform](https://docs.snyk.io/snyk-infrastructure-as-code/snyk-cli-for-infrastructure-as-code/test-your-terraform-files-with-the-cli-tool)
* [Kubernetes](https://docs.snyk.io/snyk-infrastructure-as-code/snyk-cli-for-infrastructure-as-code/test-your-kubernetes-files-with-our-cli-tool)
* [CloudFormation](test-your-cloudformation-files-with-cli-tool.md)

{% hint style="info" %}
CLI 버전 1.594.0부터 모든 구성 파일은 로컬에서 처리되어 시스템을 벗어나지 않습니다.\
이전 버전은 기본적으로 구성 파일을 Snyk으로 전송하여 처리합니다. 최신 버전의 CLI로 업그레이드하는 것을 권장합니다.
{% endhint %}

다음 예에서는 `main.tf` 파일 이름(예: `deployment.yaml`)을 변경할 수 있습니다.

## 지정된 파일 테스트

```
snyk iac test
```

예를 들어, CLI에서 다음과 같이 입력하여 테스트할 파일을 지정할 수 있습니다.

```
snyk iac test main.tf
```

다음과 같이 파일 이름을 차례로 추가하여 여러 파일을 지정할 수 있습니다.

```
snyk iac test file-1.tf file-2.tf
```

## 파일 디렉토리 테스트

구성 파일의 디렉토리를 스캔할 수 있습니다. 이와 같이 진행하면 파일 및 폴더를 재귀적으로 스캔합니다.

예를 들어, 현재 경로와 관련된 모든 디렉토리를 스캔하려면 다음과 같이 입력합니다.

```
snyk iac test
```

또는 특정 폴더를 지정하여 스캔할 수 있습니다.

```
snyk iac test my-folder
```

또는 다음과 같이 스캔할 디렉토리의 깊이를 제한할 수 있습니다.

```
snyk iac test --detection-depth=3
```

이렇게 하면 지정된 디렉토리(PATH가 제공되지 않은 경우 현재 디렉토리)와 2단계의 하위 디렉토리로 스캔이 제한됩니다.

## 테스트를 JSON 형식으로 출력

```
snyk iac test  --json
```

이는 결과의 스냅샷을 로컬에 저장하거나 보고서 및 추가 분석을 위해 다른 도구에서 결과를 처리하는 경우에 사용될 수 있습니다.

예를 들어, 다음과 같이 입력하여 지정된 파일에 대한 결과를 JSON 형식으로 출력할 수 있습니다.

```
snyk iac test main.tf --json
```

## 테스트를 SARIF 형식으로 출력

SARIF는 정적 분석 도구의 출력을 위한 개방형 표준입니다.

테스트 결과를 다른 도구에서 분석하기 위해 SARIF 파일로 확인하고 저장할 수 있습니다.

```
snyk iac test main.tf --sarif
```

결과를 파일 저장하려면 다음과 같이 입력합니다.

```
snyk iac test main.tf --sarif-file-output=snyk.sarif
```

## 특정 심각도 수준 이상의 Issue만 표시

```
snyk iac test  --severity-threshold=medium
```

예를 들어, CLI에서 다음과 같이 입력합니다.

```
snyk iac test main.tf --severity-threshold=medium
```

이는 심각도 수준이 medium 이상인 결과만 표시됩니다.

## 특정 Snyk 조직 지정

Snyk UI의 조직 수준에서 보안 규칙의 심각도 설정을 제어할 수 있습니다. CLI 테스트에서 특정 조직을 대상으로 하여 실행해야 하는 규칙과 규칙의 심각도를 결정할 수 있습니다.

```
snyk iac test  --org=infrastructure
```

예를 들어, CLI에서 다음과 같이 입력합니다.

```
snyk iac test main.tf --org=infrastructure
```

다음과 같이 입력하여 `snyk config`에서 `org` 옵션을 설정할 수 있기 때문에 매번 `--org` 옵션을 지정할 필요가 없습니다.

```
snyk config set org=infrastructure
```
