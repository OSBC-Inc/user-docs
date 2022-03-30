# 로컬 custom rules bundle 사용

{% hint style="info" %}
예제에 `bundle.tar.gz`의 bundle 이름을 바꿀 수 있습니다. 예를 들어 `bundle-v1.0.0.tar.gz` 또는 `./bundles/team-bundle.tar.gz`입니다.
{% endhint %}

프로젝트 폴더에서 다음 명령어를 실행하십시오.

```
snyk iac test --rules=bundle.tar.gz
```

이제 구성 파일 스캔 결과에 기본 Snyk rules와 custom rules의 Issue가 모두 포함됩니다. [구성 파일 Issue 이해](../../snyk-cli-for-infrastructure-as-code/understanding-configuration-scan-issues.md)를 참조하십시오.

### Troubleshooting

**-d** 플래그로 명령어를 실행하여 디버그 로그를 활성화합니다.

```
snyk iac test --rules=bundle.tar.gz -d
```

다음과 같은 문제가 발생할 수 있습니다.

* bundle에 대한 잘못된 경로 또는 존재하지 않는 bundle에 대한 경로를 제공합니다. `--rules` 옵션에 전달된 경로가 현재 위치에서 액세스할 수 있는지 확인하십시오.

```
We were unable to extract the rules provided at: ./invalid/location/bundle.tar.gz
```

* 손상되었거나 잘못된 bundle을 제공합니다. [SDK 시작하기](../getting-started-with-the-sdk/)에 따라서 bundle을 생성했는지 확인하십시오.

```
We were unable run the test. Please run the command again with the `-d` flag and contact support@snyk.io with the contents of the output.
```

설명할 수 없는 문제를 발견하셨다면 [지원 팀에 문의하십시오.](https://support.snyk.io/hc/en-us/requests/new)
