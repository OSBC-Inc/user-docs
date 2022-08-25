# CLI 명령 도움말

Snyk CLI는 프로젝트를 검색하여 보안 취약성 및 라이센스 문제를 모니터링합니다.

자세한 내용은 [Snyk website](https://snyk.io)를 참조하십시오.

자세한 내용은 [CLI documentation](../)를 참조하십시오.

## 시작하는 방법

1. `synk auth`를 실행하여 인증
2. `synk test`로 로컬 프로젝트 테스트
3. `snyk monitor`를 통해 새로운 취약성에 대한 경고 받기

## 사용 가능한 명령

각 Snyk CLI 명령에 대해 자세히 알아보려면 `--help` 옵션을 사용하십시오. \
예: `snyk auth --help` or `snyk container --help`

**참고:** 문서 사이트의 도움말은 CLI의 `-help`와 동일합니다.

### ``[`snyk auth`](undefined.md)``

Snyk 계정을 사용하여 Snyk CLI를 인증합니다.

### ``[`snyk test`](undefined-1.md)``

프로젝트를 테스트하여 오픈 소스 취약성 및 라이센스 문제를 확인합니다.

**참고**: 모든 파일에서 알려진 오픈 소스 종속성을 검색하려면 `snyk test --unmanaged`를 사용합니다(C/C++만 해당).

### ``[`snyk monitor`](monitor.md)``

프로젝트를 스냅샷으로 만들고 지속적으로 모니터링하여 오픈 소스 취약성 및 라이센스 문제를 해결합니다.

### ``[`snyk container`](undefined-3.md)``

컨테이너 이미지에서 취약성을 테스트합니다.

### ``[`snyk iac`](iac.md)``

Infrastructure as Code 파일에서 보안 문제를 찾고 관리하는 명령입니다.

### ``[`snyk code`](undefined-1.md)``

정적 코드 분석을 사용하여 보안 문제를 찾습니다.

### ``[`snyk log4shell`](log4shell.md)``

Log4Shell 취약성을 찾습니다.

### ``[`snyk config`](undefined-2.md)``

Snyk CLI 구성을 관리합니다.

### ``[`snyk policy`](policy.md)``

패키지에 대한 `.synk` 정책을 표시합니다.

### ``[`snyk ignore`](ignore.md)``

.synk 정책을 수정하여 명시된 문제를 무시합니다.

## 디버그

`-d`옵션을 사용하여 디버그 로그를 출력합니다.

## Snyk CLI 구성

환경 변수를 사용하여 Snyk CLI를 구성하고 변수를 설정하여 Snyk API에 연결할 수 있습니다. [Snyk CLI 구성](../snyk-cli.md)을 참조하십시오.
