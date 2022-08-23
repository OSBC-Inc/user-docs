# CLI 테스트에 대한 severity threshold 설정

테스트에 대한 제어력을 향상시키려면 `snyk test` \*\*\* command에 대해 `low|medium|high|critical` 중 하나와 `--severity-threshold` 옵션을 사용할 수 있습니다. 이 옵션을 사용하면 지정된 level 이상의 취약성만 보고됩니다.

`$ snyk test --severity-threshold=medium`

\{% hint style="info" %\} `--severity-threshold`를 low로 설정하면 임계값을 지정하지 않고 명령을 실행하는 것과 동일한 효과가 있으며 모든 취약성이 보고됩니다. \{% endhint %\}

주의: `--severity-threshold` 옵션은 `snyk test`, `snyk monitor`, `snyk code`, `snyk container` 및 `snyk iac` command를 사용하여 사용할 수 있습니다. 자세한 내용은 각 command에 대한 [CLI commands help](https://github.com/snyk/user-docs/tree/5e52535b78618f57eda40eb08fc8fbf91e16f1f0/docs/features/snyk-cli/commands) 페이지를 참조하십시오.
