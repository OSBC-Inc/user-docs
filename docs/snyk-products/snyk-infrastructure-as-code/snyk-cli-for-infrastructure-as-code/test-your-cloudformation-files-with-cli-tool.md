# CLI를 사용하여 CloudFormation 파일 테스트

Snyk Infrastructure as Code를 사용하면 CLI에서 직접 구성 파일을 테스트할 수 있습니다.

CloudFormation 파일에서 Snyk Infrastructure as Code는 yaml, json 형식 스캔을 지원합니다.

{% hint style="info" %}
AWS CDK 응용 프로그램을 스캔할 수도 있습니다. 자세한 내용은 [CLI를 사용하여 AWS CDK 파일 테스트 진행](test-your-aws-cdk-files-with-our-cli-tool.md) 문서를 참조하십시오.
{% endhint %}

CLI는 다음과 같이 사용할 수 있습니다.

## 지정된 파일에 대한 Issue를 테스트하는 방법

```
snyk iac test
```

예를 들어 CLI에서 다음과 같이 입력합니다.

```
snyk iac test deploy.yaml
```

다음과 같이 파일 이름을 추가하여 여러 파일을 지정할 수 있습니다.

```
snyk iac test file-1.yaml file-2.yaml
```
