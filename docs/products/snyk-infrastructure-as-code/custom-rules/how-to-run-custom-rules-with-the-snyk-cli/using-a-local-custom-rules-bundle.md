# 로컬 custom rules bundle 사용

{% hint style="info" %}
예제에 `bundle.tar.gz`가 표시된 경우 이 값을 bundle 이름으로 바꿀 수 있습니다. 예를 들어 `bundle-v1.0.0.tar.gz` 또는 `./bundles/team-bundle.tar.gz`를 입력합니다.
{% endhint %}

프로젝트의 폴더에서 다음 명령어을 실행하세요.

```
snyk iac test --rules=bundle.tar.gz
```

이제 configuration 스캔 결과에 기본 Snyk rules와 custom rules의 이슈가 모두 포함됩니다. [Understanding configuration issues](https://docs.snyk.io/snyk-infrastructure-as-code/snyk-cli-for-infrastructure-as-code/understanding-configuration-scan-issues)를 참조하세요.

### Troubleshooting

**-d** 플래그로 명령어를 실행하여 디버그 로그를 사용하도록 설정합니다.

```
snyk iac test --rules=bundle.tar.gz -d
```

다음과 같은 문제가 발생할 수 있습니다.

* bundle에 대한 잘못된 경로 또는 존재하지 않는 bundle에 대한 경로를 제공합니다. `--rules` 플래그에 전달된 경로가 현재 위치에서 액세스할 수 있는지 확인합니다.

```
We were unable to extract the rules provided at: ./invalid/location/bundle.tar.gz
```

* [Getting Started with the SDK](../getting-started-with-the-sdk/)의 지침에 따라 bundle을 생성했는지 확인하세요.

```
We were unable run the test. Please run the command again with the `-d` flag and contact support@snyk.io with the contents of the output.
```

설명할 수 없는 문제를 발견하셨다면 지원 티켓을 올려주세요.
