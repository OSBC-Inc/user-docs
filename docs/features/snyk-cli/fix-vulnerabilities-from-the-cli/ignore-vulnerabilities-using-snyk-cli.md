# Snyk CLI를 사용하여 취약점 무시

[Snyk Open Source](../../../snyk-products/snyk-open-source/)의 경우 이 옵션이 기본적으로 작동합니다.\
[Snyk Container](../../../snyk-products/snyk-container/)의 경우 이러한 옵션도 작동하지만 무시를 등록한 후 `snyk test` 또는 `snyk monitor`를 호출할 때 `--policy-path=` 옵션을 사용해야 합니다(예: `snyk container test node --policy-path=.snyk.`). \
[Infrastructure as Code용 Snyk CLI](../../../snyk-products/snyk-infrastructure-as-code/snyk-cli-for-infrastructure-as-code/)의 경우 [.snyk 정책 파일을 이용한 무시](../../../snyk-products/snyk-infrastructure-as-code/snyk-cli-for-infrastructure-as-code/iac-ignores-using-the-.snyk-policy-file.md)를 참조하십시오. \
[Snyk Code](../../../snyk-products/snyk-code/)의 경우 이러한 옵션이 아직 구현되지 않았습니다.

때때로 Snyk는 업데이트나 Snyk 패치를 사용할 수 없거나 현재 응용 프로그램에서 악용될 수 있다고 생각되지 않는 취약점에 대해 경고합니다. 이 경우 특정 기간 동안 취약점을 무시하도록 Snyk에 지시할 수 있습니다.

`snyk ignore` command를 사용하여 프로젝트의 특정 취약점을 무시할 수 있습니다.

`snyk ignore --id=<ISSUE_ID> [--expiry=<EXPIRY>] [--reason=<REASON>] [--policy-path=<PATH_TO_POLICY_FILE>] [<OPTIONS>]`

`snyk ignore` command은 다음 옵션을 지원합니다:

| **OPTION**                            | **DESCRIPTION**                                                                                                                                                                                                                                                                                                                                                                                       | **DEFAULT** | **REQUIRED** |
| ------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------- | ------------ |
| `--id`                                | <p>The Snyk ID for the issue to ignore. Found by running <code>snyk test</code> and grabbing the last segment of the URL for a given vulnerability.</p><p><strong>Example:</strong> For the vulnerability found at <a href="https://snyk.io/vuln/npm:tough-cookie:20160722">https://snyk.io/vuln/npm:tough-cookie:20160722</a>, the Snyk ID is:</p><p><code>--id=npm:tough-cookie:20160722</code></p> | None        | Yes          |
| `--expiry`                            | <p>Expiry date in YYYY-MM-DD format (<a href="https://tools.ietf.org/html/rfc2822#page-14">RFC2822</a> and <a href="https://www.iso.org/iso-8601-date-and-time-format.html">ISO 8601</a> are supported).</p><p>Example: <code>--expiry=2017-04-30</code>.</p>                                                                                                                                         | 30 days     | No           |
| `--reason`                            | Human-readable \<REASON> to ignore this issue. Example: `reason='Not currently exploitable'`.                                                                                                                                                                                                                                                                                                         | None        | No           |
| `--policy-path=<PATH_TO_POLICY_FILE>` | Path to a .snyk policy file to pass manually.                                                                                                                                                                                                                                                                                                                                                         | None        | No           |
| `--path`                              | Path to resource for which to ignore the issue. Example: `path='tough-cookie@2.15.8'`                                                                                                                                                                                                                                                                                                                 | All         | No           |
