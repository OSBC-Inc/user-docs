# Set severity thresholds for CLI tests

To improve control over your tests, you can use the `--severity-threshold` option for the `snyk test` \*\*\*\* command with one of the supported levels: `low|medium|high|critical`. With this option, only vulnerabilities of **the specified level or higher** are reported.

`$ snyk test --severity-threshold=medium`

\{% hint style="info" %\} Setting `--severity-threshold` to `low` has the same effect as running the command without specifying the threshold; all vulnerabilities are reported. \{% endhint %\}

Note: The `--severity-threshold` option is available with the `snyk test`, `snyk monitor`, `snyk code`, `snyk container`, and `snyk iac` commands. See the [CLI commands help](https://github.com/snyk/user-docs/blob/5e52535b78618f57eda40eb08fc8fbf91e16f1f0/docs/features/snyk-cli/commands) pages for each command for details.
