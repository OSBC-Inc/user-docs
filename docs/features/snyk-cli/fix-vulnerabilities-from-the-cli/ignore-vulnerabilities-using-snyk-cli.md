# Snyk CLI를 사용하여 취약점 무시

{% hint style="info" %}
[Snyk Open Source](../../../snyk-products/snyk-open-source/)의 경우 이 옵션이 기본적으로 작동합니다.\
[Snyk Container](../../../snyk-products/snyk-container/)의 경우 이러한 옵션도 작동하지만 무시를 등록한 후 `snyk test` 또는 `snyk monitor`를 호출할 때 `--policy-path=` 옵션을 사용해야 합니다(예: `snyk container test node --policy-path=.snyk.`). \
[Infrastructure as Code용 Snyk CLI](../../../snyk-products/snyk-infrastructure-as-code/snyk-cli-for-infrastructure-as-code/)의 경우 [.snyk 정책 파일을 이용한 무시](../../../snyk-products/snyk-infrastructure-as-code/snyk-cli-for-infrastructure-as-code/iac-ignores-using-the-.snyk-policy-file.md)를 참조하십시오. \
[Snyk Code](../../../snyk-products/snyk-code/)의 경우 이러한 옵션이 아직 구현되지 않았습니다.
{% endhint %}

Sometimes, Snyk alerts you to a vulnerability that has no update or Snyk patch available, or that you do not believe to be currently exploitable in your application. When this happens you may want to tell Snyk to ignore the vulnerability for a certain period of time.

You can ignore a specific vulnerability in a project using the `snyk ignore` command.

`snyk ignore --id=<ISSUE_ID> [--expiry=<EXPIRY>] [--reason=<REASON>] [--policy-path=<PATH_TO_POLICY_FILE>] [<OPTIONS>]`

The `snyk ignore` command supports the following options:

| **OPTION**                            | **DESCRIPTION**                                                                                                                                                                                                                                                                                                                                                                                       | **DEFAULT** | **REQUIRED** |
| ------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------- | ------------ |
| `--id`                                | <p>The Snyk ID for the issue to ignore. Found by running <code>snyk test</code> and grabbing the last segment of the URL for a given vulnerability.</p><p><strong>Example:</strong> For the vulnerability found at <a href="https://snyk.io/vuln/npm:tough-cookie:20160722">https://snyk.io/vuln/npm:tough-cookie:20160722</a>, the Snyk ID is:</p><p><code>--id=npm:tough-cookie:20160722</code></p> | None        | Yes          |
| `--expiry`                            | <p>Expiry date in YYYY-MM-DD format (<a href="https://tools.ietf.org/html/rfc2822#page-14">RFC2822</a> and <a href="https://www.iso.org/iso-8601-date-and-time-format.html">ISO 8601</a> are supported).</p><p>Example: <code>--expiry=2017-04-30</code>.</p>                                                                                                                                         | 30 days     | No           |
| `--reason`                            | Human-readable \<REASON> to ignore this issue. Example: `reason='Not currently exploitable'`.                                                                                                                                                                                                                                                                                                         | None        | No           |
| `--policy-path=<PATH_TO_POLICY_FILE>` | Path to a .snyk policy file to pass manually.                                                                                                                                                                                                                                                                                                                                                         | None        | No           |
| `--path`                              | Path to resource for which to ignore the issue. Example: `path='tough-cookie@2.15.8'`                                                                                                                                                                                                                                                                                                                 | All         | No           |
