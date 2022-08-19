# CLI 명령 도움말

Snyk CLI는 프로젝트를 검색하여 보안 취약성 및 라이센스 문제를 모니터링합니다.

자세한 내용은 [Snyk website](https://snyk.io)를 참조하십시오.

자세한 내용은 [CLI documentation](https://docs.snyk.io/features/snyk-cli)를 참조하십시오.

## 시작하는 방법

1. `synk auth`를 실행하여 인증
2. `synk test`로 로컬 프로젝트 테스트
3. `snyk monitor`를 통해 새로운 취약성에 대한 경고 받기

## 사용 가능한 명령

각 Snyk CLI 명령에 대해 자세히 알아보려면 `--help` 옵션을 사용하십시오. \
예: `snyk auth --help` or `snyk container --help`

**참고:** 문서 사이트의 도움말은 CLI의 `-help`와 동일합니다.

### [auth.md](../cli-commands-help/auth.md "mention")

Snyk 계정을 사용하여 Snyk CLI를 인증합니다.

### `snyk test`

Test a project for open source vulnerabilities and license issues.

**Note**: Use `snyk test --unmanaged` to scan all files for known open source dependencies (C/C++ only).

### `snyk monitor`

Snapshot and continuously monitor a project for open source vulnerabilities and license issues.

### `snyk container`

Test container images for vulnerabilities.

### `snyk iac`

Commands to find and manage security issues in Infrastructure as Code files.

### `snyk code`

Find security issues using static code analysis.

### `snyk log4shell`

Find Log4Shell vulnerability.

### `snyk config`

Manage Snyk CLI configuration.

### `snyk policy`

Display the `.snyk` policy for a package.

### `snyk ignore`

Modify the `.snyk` policy to ignore stated issues.

## Debug

Use `-d` option to output the debug logs.

## Configure the Snyk CLI

You can use environment variables to configure the Snyk CLI and also set variables to configure the Snyk CLI to connect with the Snyk API. See [Configure the Snyk CLI](https://docs.snyk.io/features/snyk-cli/configure-the-snyk-cli)
