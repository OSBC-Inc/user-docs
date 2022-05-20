# Issue 무시 소개

{% hint style="info" %}
Issue 무시에 대한 자세한 내용은 [프로젝트에 우선순위가 지정되지 않은 Issue 무시](https://docs.snyk.io/fixing-and-prioritizing-issues/issue-management/ignore-issues)를 참조하십시오.
{% endhint %}

## Snyk UI

각 Issue 카드에는 해당 Issue를 무시할 수 있는 **Ignore** 버튼이 있습니다.

![](../../../.gitbook/assets/new-ignore-2.png)

## Snyk CLI

Snyk CLI에서 **snyk ignore**을 사용하여 Issue를 무시할 수 있습니다. 예시는 아래와 같습니다.

`snyk ignore --id='npm:braces:20180219' --expiry='2018-04-01' --reason='testing'`
