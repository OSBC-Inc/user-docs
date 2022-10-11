# 공유 정책 개요

**전제 조건**

**정책** 설정을 업데이트하려면 그룹의 그룹 관리자여야 합니다.

{% hint style="info" %}
**기능 가용성**

이 기능은 Enterprise 고객이 사용할 수 있습니다. 자세한 내용은 [요금제](https://snyk.io/plans/)를 참조하세요.
{% endhint %}

## Navigate to the Policy manager

1. Log in to Snyk
2. Navigate to your group
3. Click on the Policies tab in the navigation bar to see all the policies that exist within your group, broken out by category. This list will include the [default policy](shared-policies-overview.md#default-policies), which is automatically created for new groups for each policy category and cannot be removed.

![](../../../.gitbook/assets/screen\_shot\_2021-08-11\_at\_2.15.48\_pm.png)

The Policy manager appears similar to the following:

![](../../../.gitbook/assets/screenshot\_2021-03-26\_at\_11.04.50\_am.png)

## Default policies

Each policy category has its own default policy. Default policies can only be applied to organizations, not project attributes.

When you create a **new** **organization**, it will automatically be added to the default policy, unless you have selected to copy an existing organization's settings. Organizations can be moved to a different policy if desired.

The default policy cannot be deleted; however, the default policy name, description, and the rules can be edited to match your preferences. A default policy can also contain no rules if you'd prefer.

To learn more about how to add and remove organizations to the default policy, read more about it [here](https://docs.snyk.io/fixing-and-prioritizing-issues/policies/assign-a-policy-to-organizations).
