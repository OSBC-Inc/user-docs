# 프로젝트 속성에 정책 할당

프로젝트 속성을 프로젝트에 적용한 후 해당 속성에 적용되는 정책을 생성할 수 있습니다. 프로젝트와 정책은 정책에 할당된 속성을 기반으로 연결됩니다.

{% hint style="info" %}
속성에 할당된 정책은 항상 조직에 할당된 정책보다 우선합니다.
{% endhint %}

정책은 하나 이상의 프로젝트 속성에 적용될 수 있습니다. 그러나 속성 집합은 하나의 정책에만 할당할 수 있습니다. 예를 들어 `Critical`, `Production`, `Frontend`에 적용된 정책이 이미 있는 경우 이러한 정확한 속성만 일치하는 다른 정책을 생성할 수 없습니다.

Reminder: 프로젝트 속성에 할당된 정책은 CLI에서 snyk 모니터를 실행할 때 적용되며 프로젝트 속성이 적용된 CLI 프로젝트에서 실행된다고 가정합니다. 프로젝트 속성 정책은 **snyk test**에 적용되지 않습니다.

## 정책에 속성 추가/제거

속성을 추가하려면 속성 선택기 패널에서 원하는 속성 확인란을 클릭합니다.

정책에서 속성을 제거하려면 속성 선택기 패널에서 원하는 속성 확인란의 선택을 취소합니다.

![](../../../.gitbook/assets/screenshot\_2021-03-11\_at\_1.20.42\_pm.png)

{% hint style="info" %}
예를 들어 해당 정책과 연결할 속성을 아직 결정하지 않은 경우 속성이 선택되지 않은 정책을 만들고 저장할 수 있습니다. 이 정책은 모든 속성이 비어 있는 프로젝트에는 적용되지 않습니다.
{% endhint %}

## Matching projects and policies

To be associated with a policy, a project must have all the attributes listed on the policy (the project could also have more attributes that are not listed on the policy).

For example, if you have a policy assigned to `Critical`, `External`, and `Frontend`, this policy applies to projects which includes those same attributes, but not to a project with the attributes `Critical` and `External`.\
Here is our sample policy:

![](../../../.gitbook/assets/screenshot\_2021-03-11\_at\_11.54.33\_am.png)

Here is a project that will inherit the policy:

![](../../../.gitbook/assets/screenshot\_2021-03-11\_at\_12.26.02\_pm.png)

Here is a project that will not inherit the policy:

![](../../../.gitbook/assets/screenshot\_2021-03-11\_at\_12.29.03\_pm.png)

## Applying multiple policies to a project

It is possible that more than one policy can be apply for a project. For example, if you have a policy assigned to `Critical` and `External` and another policy assigned to `Critical` and `Production`. If you have a project that has the attributes `Critical`, `External` and `Production`, it could apply to either of these policies!

If more than one policy can be associated with a project, the order of the policies on the policy manager page determines precedence. The policy closest to the top of the list takes precedence over other applicable policies below it. To change the order of policies, either drag and drop the policies into the right order, or use the **...** button on the right hand side to move the policy up or down in the list.

![](../../../.gitbook/assets/screenshot\_2021-03-11\_at\_12.51.25\_pm.png)
