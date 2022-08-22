# CLI reference

### 사용법

`snyk [COMMAND] [SUBCOMMAND] [OPTIONS] [PACKAGE] [CONTEXT`-SPECIFIC\_OPTIONS`]`

### 설명

The Snyk CLI is a build-time tool to find and fix known vulnerabilities in your projects. For a more detailed description of the Snyk CLI and Snyk, see [Snyk CLI](https://github.com/snyk/user-docs/blob/5e52535b78618f57eda40eb08fc8fbf91e16f1f0/docs/features/snyk-cli). For an introduction on how to use the Snyk CLI, see [Getting started with the CLI](https://github.com/snyk/user-docs/blob/5e52535b78618f57eda40eb08fc8fbf91e16f1f0/docs/features/snyk-cli/getting-started-with-the-cli).

### 사용 가능한 CLI Command

To learn more about each Snyk CLI command, use the `--help` option, for example, `snyk auth --help` or `snyk container --help`. You can also use the help command: `snyk help [<COMMAND>]`.

Each command in this list is linked to the corresponding help page in these docs. A list of all the [options](https://github.com/snyk/user-docs/blob/5e52535b78618f57eda40eb08fc8fbf91e16f1f0/docs/features/snyk-cli/cli-reference/#options) for Snyk CLI commands is at the end of this page. The options are explained in detail in the help for each command.

#### [`snyk auth`](https://github.com/snyk/user-docs/blob/5e52535b78618f57eda40eb08fc8fbf91e16f1f0/docs/features/snyk-cli/commands/auth.md)

Authenticate Snyk CLI with a Snyk account.

#### [`snyk test`](https://github.com/snyk/user-docs/blob/5e52535b78618f57eda40eb08fc8fbf91e16f1f0/docs/features/snyk-cli/commands/test.md)

Test a project for open source vulnerabilities and license issues.

#### [`snyk monitor`](https://github.com/snyk/user-docs/blob/5e52535b78618f57eda40eb08fc8fbf91e16f1f0/docs/features/snyk-cli/commands/monitor.md)

Snapshot and continuously monitor a project for open source vulnerabilities and license issues.

#### [`snyk container`](https://github.com/snyk/user-docs/blob/5e52535b78618f57eda40eb08fc8fbf91e16f1f0/docs/features/snyk-cli/commands/container.md)

Test container images for vulnerabilities.

#### [`snyk iac`](https://github.com/snyk/user-docs/blob/5e52535b78618f57eda40eb08fc8fbf91e16f1f0/docs/features/snyk-cli/commands/iac.md)

Find security issues in Infrastructure as Code files.

#### [`snyk code`](https://github.com/snyk/user-docs/blob/5e52535b78618f57eda40eb08fc8fbf91e16f1f0/docs/features/snyk-cli/commands/code.md)

Find security issues using static code analysis.

#### [`snyk log4shell`](https://github.com/snyk/user-docs/blob/5e52535b78618f57eda40eb08fc8fbf91e16f1f0/docs/features/snyk-cli/commands/log4shell.md)

Find Log4Shell vulnerability.

#### [`snyk config`](https://github.com/snyk/user-docs/blob/5e52535b78618f57eda40eb08fc8fbf91e16f1f0/docs/features/snyk-cli/commands/config.md)

Manage Snyk CLI configuration.

#### [`snyk policy`](https://github.com/snyk/user-docs/blob/5e52535b78618f57eda40eb08fc8fbf91e16f1f0/docs/features/snyk-cli/commands/policy.md)

Display the `.snyk` policy for a package.

#### [`snyk ignore`](https://github.com/snyk/user-docs/blob/5e52535b78618f57eda40eb08fc8fbf91e16f1f0/docs/features/snyk-cli/commands/ignore.md)

Modify the `.snyk` policy to ignore stated issues.

### 새로운 CLI Command

#### ``[`snyk fix`](../fix-vulnerabilities-from-the-cli/automatic-remediation-with-snyk-fix.md)``

Apply the recommended updates for supported ecosystems automatically.

#### ``[`snyk apps`](https://docs.snyk.io/features/snyk-cli/create-a-snyk-app-using-the-snyk-cli)``

Create a Snyk App using the Snyk CLI.

### CLI commands의 Sub-commands

The following is a list of the sub-commands for Snyk CLI commands. Each sub-command is followed by the command(s) to which the sub-command applies. The commands are linked to their help docs. For details concerning each sub-command, see the help docs.

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
