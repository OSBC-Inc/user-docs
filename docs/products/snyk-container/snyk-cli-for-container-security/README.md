# 컨테이너 보안을 위한 Snyk CLI

[CLI](../../../features/snyk-cli/)(Snyk Container Command Line Interface)는 로컬 시스템의 컨테이너 이미지에서 취약점을 찾고 수정하는 데 도움이 됩니다.

CLI를 사용하려면 먼저 CLI를 [설치](../../../features/snyk-cli/install-the-snyk-cli/)한 다음 [인증](../../../features/snyk-cli/commands/auth.md)해야 합니다.

## 이미지 테스트

이미지 테스트를 실행하려면:

```
snyk container test debian
```

이 명령은 다음을 수행합니다.

1. 이미지를 Docker 데몬에서 로컬로 사용할 수 없는 경우 다운로드합니다.
2. 이미지에 설치된 소프트웨어를 결정합니다.
3. 해당 BOM을 Snyk 서비스로 보냅니다.
4. 이미지의 취약점 목록을 반환합니다.

Snyk을 사용하여 원격 레지스트리에서 가져올 수 있는 모든 이미지 또는 로컬에서 빌드하고 로컬 Docker 데몬에서 사용할 수 있게 만든 이미지를 테스트할 수 있습니다.

```
snyk container test <repository>:<tag>
```

Docker 파일을 사용하여 이미지를 빌드할 경우  `container test`를 실행하여 이 파일을 지정할 수 있습니다.

```
snyk container test <repository>:<tag> --file=Dockerfile
```

Dockerfile을 지정하면 더 많은 컨텍스트를 제공하고 Snyk이 발견된 취약점을 수정하는 방법에 대한 명확한 권장 사항을 제공할 수 있습니다.

## 이미지 모니터링

Snyk Container를 사용하여 이미지를 모니터링할 수도 있습니다. 이는 다음과 같은 이점을 제공합니다.

* Snyk은 이미지에 영향을 미치는 새로운 취약점이 공개되면 이미지를 로컬에서 다시 테스트할 필요 없이 사용자에게 알려줍니다.
* Snyk은 대화식으로 결과를 필터링하고 웹 브라우저의 취약점 목록을 탐색합니다.
* Snyk에서 결과를 다른 팀원들과 공유할 수 있습니다.

또한 모든 프로젝트의 취약점에 대한 종합 보고서에 액세스할 수 있습니다.

{% hint style="info" %}
**기능 가용성**\
이 집계 보고서 기능은 모든 유료 요금제에서 사용할 수 있습니다. 자세한 내용은 [pricing plans](https://snyk.io/plans/)를 참조하십시오.
{% endhint %}

이미지 모니터링을 실행하려면:

```
snyk container monitor <repository>:<tag>
```

이 명령은 다음을 수행합니다.

1. 이미지를 Docker 데몬에서 로컬로 사용할 수 없는 경우 다운로드합니다.
2. 이미지에 설치된 소프트웨어를 결정합니다.
3. 해당 BOM을 Snyk 서비스로 보냅니다.
4. 결과를 볼 수 있는 Snyk 서비스에 대한 링크를 반환합니다.

![](../../../.gitbook/assets/monitor.png)

{% hint style="info" %}
**참고**\
Snyk Container에서 `test`와 `monitor`를 모두 사용하는 것이 일반적입니다. `test` 명령은 빠른 확인에 좋습니다. `monitor` 명령을 사용하여 결과를 지속적으로 보장하고 보다 쉽게 공유할 수 있습니다.
{% endhint %}

## 추가 정보

* [Snyk Container CLI 결과 이해](https://docs.snyk.io/snyk-container/snyk-cli-for-container-security/understanding-snyk-container-cli-results)
* [고급 CLI 사용](https://docs.snyk.io/snyk-container/snyk-cli-for-container-security/advanced-snyk-container-cli-usage)
* [컨테이너 보안](https://snyk.io/learn/container-security/)에 대해 자세히 알아보기
