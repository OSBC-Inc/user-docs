# Advanced failing of builds in Snyk CLI

Snyk CLI는 빌드 실패 시 다음 옵션을 제공합니다.

```
--severity-threshold=low|medium|high
```

제공된 수준 이상의 취약점만 보고합니다.

```
--fail-on=all|upgradable|patchable
```

수정할 수 있는 취약점이 있는 경우에만 실패합니다.

```
--fail-on=all
```

업그레이드하거나 패치할 수 있는 취약점이 하나 이상 있으면 실패합니다.

```
--fail-on=upgradable
```

업그레이드할 수 있는 취약점이 하나 이상 있으면 실패합니다.

```
--fail-on=patchable
```

패치할 수 있는 취약점이 하나 이상 있으면 실패합니다. 취약점에 수정 사항이 없고 이 옵션을 사용 중인 경우 테스트를 통과합니다.

Snyk CLI 자체에는 기본적으로 더 복잡한 사용 사례에 대한 테스트를 실패할 수 있는 기능이 없습니다. 다음은 보다 복잡한 합격/불합격 기준을 달성하는 몇 가지 방법입니다.

### Combining security policies with --severity-threshold

[Security policies](https://docs.snyk.io/fixing-and-prioritizing-issues/policies) provide the capability to change the severity of a vulnerability if the severity matches specific criteria when a project is tested against an organization using that policy. You could, for example, change the severity of a vulnerability from high to low, and if you run `snyk test` with the CLI with

```
 --severity-threshold=medium|high
```

this previously high severity vulnerability no longer fails the build.

\{% hint style="info" %\} Security policies do not have all attributes available for criteria matching. Refer to the security policy configuration to see what is available as it is added to over time. \{% endhint %\}

Here is an example of `snyk test` using `--severity-threshold=high` running against a default organization with no policy applied to it.

![](https://camo.githubusercontent.com/de965fce454134d8cadaaf22fe093c4fdf1722a7349e99f1d2d8bc4cf9726836/68747470733a2f2f67626c6f627363646e2e676974626f6f6b2e636f6d2f6173736574732532462d4d56584b6472682d6a59334b44475073386c512532462d4d5a545f57334f316f46794d417a46396733732532462d4d5a5472633044364e6a5436566c53316a6d55253246696d6167652e706e673f616c743d6d6564696126746f6b656e3d32376530656538632d313437662d343934322d616461342d303864653037663637633430)

Here is an example `snyk test` using `--severity-threshold=high` running against an organization with a policy that downgrades this particular vulnerability severity to `low`. There are no vulnerabilities found.

![](https://github.com/snyk/user-docs/raw/5e52535b78618f57eda40eb08fc8fbf91e16f1f0/docs/.gitbook/assets/test-organization-with-policy-applied.png)

### Companion tools

The following discusses use of snyk-delta or snyk-filter, open source companion tools for the Snyk CLI.

snyk-delta finds the delta of vulnerabilities between the current test and a previously monitored snapshot.

snyk-delta is available from npmjs.org, and may be pulled into your CI/CD pipeline using

```
npm install -g snyk-delta
```

snyk-filter provides for user-defined pass/fail criteria based on any available data in the `snyk test` JSON output.

snyk-filter is available from npmjs.org and may be pulled into your CI/CD pipeline using npm install

```
npm install -g snyk-filter
```

#### Fail current build only if new vulnerabilities are being introduced

**Inline mode**

```
snyk test --json --print-deps | snyk-delta
```

Possibly point to a specific snapshot by specifying org + project coordinates

```
snyk test --json --print-deps | snyk-delta --baselineOrg xxx --baselineProject xxx
```

**Standalone**

```
snyk-delta --baselineOrg xxx --baselineProject xxx --currentOrg xxx --currentProject xxx
```

Refer to the [snyk-delta project on GitHub](https://github.com/snyk-tech-services/snyk-delta) for more information.

#### Fail build for CVSS score higher than ...

```
snyk test --json | snyk-filter -f /path/to/example-cvss-9-or-above.yml
```

#### Custom criteria and filtering

snyk-filter can utilize any combination of criteria available in the `snyk test` JSON output.

You may also have different criteria for display from what will fail the build. This allows you to do things like display all vulnerabilities in the test output, while failing only on some specific criteria.

Refer to the [snyk-filter project on GitHub](https://github.com/snyk-tech-services/snyk-filter) for examples and more information.
