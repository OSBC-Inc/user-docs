# CLI 명령어 도움말

Snyk CLI는 프로젝트를 검색하여 보안 취약성 및 라이센스 문제를 모니터링합니다.

자세한 내용은 [Snyk website](https://snyk.io)를 참조하십시오.

자세한내용내용 [CLI documentation](https://docs.snyk.io/features/snyk-cli)를 참조하십시오.

## How to get started

1. Authenticate by running `snyk auth`
2. Test your local project with `snyk test`
3. Get alerted for new vulnerabilities with `snyk monitor`

## Available commands

To learn more about each Snyk CLI command, use the `--help` option, for example, `snyk auth --help` or `snyk container --help`

**Note:** The help on the docs site is the same as the `--help` in the CLI.

### [`snyk auth`](broken-reference)

Authenticate Snyk CLI with a Snyk account.

### [`snyk test`](broken-reference)

Test a project for open source vulnerabilities and license issues.

**Note**: Use `snyk test --unmanaged` to scan all files for known open source dependencies (C/C++ only).

### [`snyk monitor`](broken-reference)

Snapshot and continuously monitor a project for open source vulnerabilities and license issues.

### [`snyk container`](broken-reference)

Test container images for vulnerabilities.

### [`snyk iac`](broken-reference)

Commands to find and manage security issues in Infrastructure as Code files.

### [`snyk code`](broken-reference)

Find security issues using static code analysis.

### [`snyk log4shell`](broken-reference)

Find Log4Shell vulnerability.

### [`snyk config`](broken-reference)

Manage Snyk CLI configuration.

### [`snyk policy`](broken-reference)

Display the `.snyk` policy for a package.

### [`snyk ignore`](broken-reference)

Modify the `.snyk` policy to ignore stated issues.

## Debug

Use `-d` option to output the debug logs.

## Configure the Snyk CLI

You can use environment variables to configure the Snyk CLI and also set variables to configure the Snyk CLI to connect with the Snyk API. See [Configure the Snyk CLI](https://docs.snyk.io/features/snyk-cli/configure-the-snyk-cli)
