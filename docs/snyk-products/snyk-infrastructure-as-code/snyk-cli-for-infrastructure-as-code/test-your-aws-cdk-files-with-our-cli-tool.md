# CLI를 사용하여 AWS CDK 파일 테스트

## CLI를 사용하여 AWS CDK 파일 테스트 진행

Snyk Infrastructure as Code를 사용하여 CLI에서 직접 구성 파일을 테스트할 수 있습니다.

CDK CLI를 사용하여 CloudFormation 파일을 생성하고, Snyk CLI를 사용하여 AWS [CDK(Amazons Cloud Development Kit)](https://aws.amazon.com/ko/cdk/)를 스캔할 수 있습니다.

## CDK 애플리케이션 스캔

먼저 CloudFormation을 생성할 애플리케이션 스택이 들어 있는 디렉토리로 이동합니다.

다음으로 CloudFormation 파일을 생성합니다.

```
cdk synth
```

이 파일은 YAML output으로 터미널에 표시되고 `cdk.out` 디렉토리에 JSON 파일이 생성됩니다.

Snyk IaC CLI 명령을 사용하여 JSON 파일을 스캔하고  `cdk.out/.json` 파일을 스캔할 애플리케이션의 이름으로 변경합니다.

```
snyk iac test cdk.out/.json
```
