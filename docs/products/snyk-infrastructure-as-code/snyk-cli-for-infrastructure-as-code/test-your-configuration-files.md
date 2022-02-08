# 구성 파일 테스트

Snyk Infrastructure as Code를 사용하여 CLI에서 직접 구성 파일을 테스트할 수 있습니다.

CLI를 사용하여 Kubernetes, Terraform 및 CloudFomation 파일을 스캔할 수 있습니다.

아래에서 더 자세한 정보를 확인할 수 있습니다.

* [Terraform](https://docs.snyk.io/snyk-infrastructure-as-code/snyk-cli-for-infrastructure-as-code/test-your-terraform-files-with-the-cli-tool)
* [Kubernetes](https://docs.snyk.io/snyk-infrastructure-as-code/snyk-cli-for-infrastructure-as-code/test-your-kubernetes-files-with-our-cli-tool)
* [CloudFormation](test-your-cloudformation-files-with-cli-tool.md)

{% hint style="info" %}
버전 1.594.0부터는 모든 구성 파일이 컴퓨터에서 삭제하지 않도록 로컬에서 처리됩니다.\
기본적으로 이전 버전은 Snyk으로 구성 파일을 전송하여 처리합니다. 최신 버전의 CLI로 업그레이드하는 것이 좋습니다.
{% endhint %}

You can use the CLI as follows:

예제가 `main.tf`을 표시하는 경우 파일 이름(예: `deployment.yaml`)을 바꿀 수 있습니다.

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

구성 파일의 디렉토리를 스캔할 수 있습니다. 이와 같이 진행하면 파일 및 폴더를 재귀적으로 검색합니다.

예를 들어, 현재 경로와 관련된 모든 디렉토리를 스캔하려면 다음과 같이 입력합니다.

```
snyk iac test
```

또는 스캔하고 반복하고싶은 특정 폴더 지정이 가능합니다.

```
snyk iac test my-folder
```

또는 다음과 같이 검색할 디렉토리의 깊이를 제한할 수 있습니다.

```
snyk iac test --detection-depth=3
```

이렇게 하면 제공된 디렉토리(PATH가 제공되지 않은 경우 현재 디렉토리)와 2단계의 하위 디렉토리로 검색이 제한됩니다.

## 테스트를 JSON 형식으로 출력

```
snyk iac test  --json
```

이는 결과의 스냅샷을 로컬에 저장하거나 보고 및 추가 분석을 위해 다른 도구에서 결과를 처리하는 경우에 사용될 수 있습니다.

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

결과를 파일에 저장하려면 다음과 같이 입력합니다.

```
snyk iac test main.tf --sarif-file-output=snyk.sarif
```

## 특정 심각도 수준 이상의 문제만 표시

```
snyk iac test  --severity-threshold=medium
```

예를 들어, CLI에서 다음과 같이 입력합니다.

```
snyk iac test main.tf --severity-threshold=medium
```

이는 심각도 수준이 medium 이상인 결과만 터미널에 표시됩니다.

## 특정 Snyk 조직 지정

Snyk UI의 조직 수준에서 보안 규칙의 심각도 설정을 제어할 수 있습니다. CLI 테스트에서 특정 조직을 대상으로 하여 실행해야 하는 규칙과 규칙의 심각도를 결정할 수 있습니다.

```
snyk iac test  --org=infrastructure
```

예를 들어, CLI에서 다음과 같이 입력합니다.

```
snyk iac test main.tf --org=infrastructure
```

다음과 같이 입력하여 Snyk Config에서 Org 플래그를 설정할 수 있기 때문에 매번 플래그를 지정할 필요가 없습니다.

```
snyk config set org=infrastructure
```
