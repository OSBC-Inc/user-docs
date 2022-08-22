# CLI reference

### 사용법

`snyk [COMMAND] [SUBCOMMAND] [OPTIONS] [PACKAGE] [CONTEXT`-SPECIFIC\_OPTIONS`]`

### 설명

Snyk CLI는 프로젝트에서 알려진 취약성을 찾아 수정하는 빌드 타임 도구입니다. Snyk CLI 및 Snyk에 대한 자세한 설명은 [Snyk CLI](https://github.com/snyk/user-docs/tree/5e52535b78618f57eda40eb08fc8fbf91e16f1f0/docs/features/snyk-cli)를 참조하십시오. Snyk CLI 사용 방법에 대한 자세한 내용은 [CLI 시작](https://github.com/snyk/user-docs/tree/5e52535b78618f57eda40eb08fc8fbf91e16f1f0/docs/features/snyk-cli/getting-started-with-the-cli)을 참조하십시오.

### 사용 가능한 CLI Command

각 Snyk CLI 명령에 대해 자세히 알아보려면 `--help` 옵션 (예: `snyk auth --help` 또는 `snyk container --help` ) 을 사용하십시오. 도움말 명령인 `snyk help [<COMMAND>]` 를 사용할 수도 있습니다.

이 목록의 각 명령은 이러한 문서의 해당 도움말 페이지에 연결됩니다. Snyk CLI command에 대한 모든 [옵션 목록](https://github.com/snyk/user-docs/tree/5e52535b78618f57eda40eb08fc8fbf91e16f1f0/docs/features/snyk-cli/cli-reference#options)은 이 페이지 끝에 있습니다. 각 Command의 도움말에서 옵션에 대해 자세히 설명합니다.

#### [`snyk auth`](https://github.com/snyk/user-docs/blob/5e52535b78618f57eda40eb08fc8fbf91e16f1f0/docs/features/snyk-cli/commands/auth.md)

Snyk 계정을 사용하여 Snyk CLI를 인증합니다.

#### [`snyk test`](https://github.com/snyk/user-docs/blob/5e52535b78618f57eda40eb08fc8fbf91e16f1f0/docs/features/snyk-cli/commands/test.md)

프로젝트를 테스트하여 오픈 소스 취약성 및 라이센스 문제를 확인합니다.

#### [`snyk monitor`](https://github.com/snyk/user-docs/blob/5e52535b78618f57eda40eb08fc8fbf91e16f1f0/docs/features/snyk-cli/commands/monitor.md)

프로젝트를 스냅샷으로 만들고 지속적으로 모니터링하여 오픈 소스 취약성 및 라이센스 문제를 해결합니다.

#### [`snyk container`](https://github.com/snyk/user-docs/blob/5e52535b78618f57eda40eb08fc8fbf91e16f1f0/docs/features/snyk-cli/commands/container.md)

컨테이너 이미지에서 취약성을 테스트합니다.

#### [`snyk iac`](https://github.com/snyk/user-docs/blob/5e52535b78618f57eda40eb08fc8fbf91e16f1f0/docs/features/snyk-cli/commands/iac.md)

Infrastructure as Code 파일에서 보안 문제를 찾습니다.

#### [`snyk code`](https://github.com/snyk/user-docs/blob/5e52535b78618f57eda40eb08fc8fbf91e16f1f0/docs/features/snyk-cli/commands/code.md)

정적 코드 분석을 사용하여 보안 문제를 찾습니다.

#### [`snyk log4shell`](https://github.com/snyk/user-docs/blob/5e52535b78618f57eda40eb08fc8fbf91e16f1f0/docs/features/snyk-cli/commands/log4shell.md)

Log4Shell 취약성을 찾습니다.

#### [`snyk config`](https://github.com/snyk/user-docs/blob/5e52535b78618f57eda40eb08fc8fbf91e16f1f0/docs/features/snyk-cli/commands/config.md)

Snyk CLI 구성을 관리합니다.

#### [`snyk policy`](https://github.com/snyk/user-docs/blob/5e52535b78618f57eda40eb08fc8fbf91e16f1f0/docs/features/snyk-cli/commands/policy.md)

패키지에 대한 `.synk` 정책을 표시합니다.

#### [`snyk ignore`](https://github.com/snyk/user-docs/blob/5e52535b78618f57eda40eb08fc8fbf91e16f1f0/docs/features/snyk-cli/commands/ignore.md)

`.synk` 정책을 수정하여 명시된 문제를 무시합니다.

### 새로운 CLI Command

#### ``[`snyk fix`](../fix-vulnerabilities-from-the-cli/automatic-remediation-with-snyk-fix.md)``

지원되는 에코시스템에 대한 권장 업데이트를 자동으로 적용합니다.

#### ``[`snyk apps`](https://docs.snyk.io/features/snyk-cli/create-a-snyk-app-using-the-snyk-cli)``

Snyk CLI를 사용하여 Snyk 앱을 만듭니다.

### CLI commands의 Sub-commands

다음은 Snyk CLI command에 대한 sub-command 목록입니다. 각 sub-command 뒤에는 sub-command가 적용되는 command가 뒤따릅니다. command는 도움말 문서에 연결됩니다. 각 sub-command에 대한 자세한 내용은 도움말 문서를 참조하십시오.

`test`: sub-command of [`code`](https://docs.snyk.io/features/snyk-cli/commands/code), [`container`](https://docs.snyk.io/features/snyk-cli/commands/container), and [`iac`](https://docs.snyk.io/features/snyk-cli/commands/iac)

`monitor`: sub-command of [`container`](https://docs.snyk.io/features/snyk-cli/commands/container)

`get <KEY>`: sub-command of [config](https://docs.snyk.io/features/snyk-cli/commands/config)

`set <KEY>=<VALUE>`: sub-command of [config](https://docs.snyk.io/features/snyk-cli/commands/config)

`unset <KEY>`: sub-command of [config](https://docs.snyk.io/features/snyk-cli/commands/config)

`clear`: sub-command of [config](https://docs.snyk.io/features/snyk-cli/commands/config)

### 종료 코드

Possible exit codes and their meaning:

**0**: success, no vulnerabilities found\
**1**: action\_needed, vulnerabilities found\
**2**: failure, try to re-run command\
**3**: failure, no supported projects

### Snyk CLI 구성

You can use environment variables to configure the Snyk CLI and also set variables to configure the Snyk CLI to connect with the Snyk API. See [Configure the Snyk CLI](https://docs.snyk.io/features/snyk-cli/configure-the-snyk-cli).

### 디버그

Use `-d` option to output the debug logs.

### 옵션

A list of all the options for Snyk CLI commands and the commands to which they apply is being developed.
