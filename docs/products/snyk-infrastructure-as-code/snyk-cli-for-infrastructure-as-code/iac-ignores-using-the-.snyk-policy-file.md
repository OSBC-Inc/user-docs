# IaC에서 .snyk 정책 파일 사용 무시

Snyk CLI에서 Snyk iac test를 사용하여 IaC 구성 파일을 검색할 때 사용자와 관련이 없는 문제는 무시할 수 있습니다.

[.snyk 정책 파일](../../../features/snyk-cli/test-for-vulnerabilities/the-.snyk-file.md)을 사용하여 이 작업을 수행할 수 있습니다. 이 파일은 IaC 구성 파일을 저장할 작업 디렉토리의 root에 저장하거나 버전이 지정되는 것이 좋습니다.

## 경로 무시

Snyk CLI를 사용한 실행의 경우 **.snyk** 파일에 정의된 문제만 무시합니다.

가져온 Git 저장소에서 실행하는 경우 다음과 같이 적용됩니다.

* Snyk UI에서 issues를 무시할 수 있습니다. 이 경우 Snyk UI를 사용하여 수행된 스캔에만 적용됩니다.
* 중요 : 이 두개의 ignore 소스는 동기화되지 않습니다.

## .snyk 파일

{% hint style="info" %}
.snyk 파일에는 IaC 프로젝트에 대한 몇 가지 제한이 있습니다(표준 기능은 [The .snyk file](../../../features/snyk-cli/test-for-vulnerabilities/the-.snyk-file.md) 참조).

* **패치** 섹션이 아직 지원되지 않으므로 무시합니다.
* IaC 지원 언어 설정이 없습니다. 이 섹션은 무시합니다.
{% endhint %}

하나 이상의 디렉토리를 전달하거나 현재 작업 디렉토리의 기본 인수를 사용하여 디렉토리에 대해 `snyk iac test`를 실행할 대 Snyk CLI는 각 디렉토리에서 `.snyk` 파일을 찾습니다.

정책 파일의 구문은 다음과 같습니다.

```
version: v1.19.0
ignore:
  SNYK-CC-K8S-1:
    - '*':
        reason: None Given
        expires: 2021-08-26T08:40:35.249Z
        created: 2021-07-27T08:40:35.251Z
```

이 파일은 `snyk ignore` 명령문으로 생성할 수 있습니다. 자세한 내용은 [Ignore vulnerabilities](https://docs.snyk.io/snyk-cli/fix-vulnerabilities-from-the-cli/ignore-vulnerabilities-using-snyk-cli)를 참조하세요.

'\*' 키를 이용하여 CLI가 SNYK-CC-K8S-1 취약점의 모든 인스턴스를 무시할 수 있습니다. IaC 문제 ID로 표시된 여러 항목을 추가하여 여러 취약점을 무시할 수 있습니다.

## 단일 파일 무시

Ignore rules는 범위를 더 좁힐 수 있습니다. 범위를 단일 파일로 지정하려면 '\*'를 정책 파일이 포함된 테스트 대상 디렉토리를 기준으로 해당 파일의 경로로 변경하세요.

```
version: v1.19.0
ignore:
  SNYK-CC-K8S-1:
    - 'staging/deployment.yaml > *':
        reason: None Given
        expires: 2021-08-26T08:40:35.249Z
        created: 2021-07-27T08:40:35.251Z
  - 'staging/cronjob.yaml > *':
        reason: None Given
        expires: 2021-08-26T08:40:35.249Z
        created: 2021-07-27T08:40:35.251Z
```

위의 예에서 우리는 2개의 특정 파일의 문제를 무시하고 있습니다.

## 취약점 인스턴스 무시

파일 내의 개별 취약성 인스턴스는 무시될 수 있습니다. 이렇게 하려면 `snyk iac test` 출력에서 "리소스 경로"를 가져와 파일 경로에 추가해야 합니다.

예를 들어, 스니펫이 다음과 같이 출력됩니다.

```
Testing production/deployment.yaml...Infrastructure as code issues:
  ✗ Container is running in privileged mode [High Severity] [SNYK-CC-K8S-1] in Deployment
    introduced by [DocId: 0] > input > spec > template > spec > containers[web] > securityContext > privileged
```

다음과 같이 정책 파일을 수정할 수 있습니다.

```
version: v1.19.0
ignore:
  SNYK-CC-K8S-1:
    - 'production/deployment.yaml > [DocId:1] > spec > template > spec > containers[web] > securityContext > privileged':
        reason: None Given
        expires: 2021-08-26T08:40:35.249Z
        created: 2021-07-27T08:40:35.251Z
```

## 정책 플래그 및 정책 파일 참고 사항

테스트 중인 디렉토리당 정책 파일이 두 개 이상 있을 수 없습니다. 예를 들어 `snyk iac test dir1/ dir2/`는 `dir1/.snyk`와 `dir2/.snyk`를 로드하지만 `dir1/foo/bar/.snyk` 파일이 있으면 CLI에서 로드하지 않습니다.

`snyk iac test`를 실행할 때 CLI는 `$PWD/.snyk`를 로드합니다. 일반적인 패턴 중 하나는 저장소의 root에 있는 저장소당 하나의 정책 파일을 사용하는 것입니다.

CLI에서는 정책 파일의 위치를 재정의하는 `--policy-path=...` 플래그를 허용합니다. 경로는 `.snyk` 파일이 들어 있는 디렉토리이거나 `.snyk` 파일의 경로일 수 있습니다. 정책 파일의 실제 이름은 `.snyk`이여야 합니다.

`snyk iac test`에 대한 인수가 디렉토리가 아닌 파일인 경우 정책이 자동으로 로드되지 않습니다. 이 경우 정책을 로드하려면 `--policy-path`를 지정해야 합니다.

CLI에서는 `--ignore-policy` 플래그를 허용하므로 사용 시 발견된 `.snyk` 정책 파일이 무시됩니다.
