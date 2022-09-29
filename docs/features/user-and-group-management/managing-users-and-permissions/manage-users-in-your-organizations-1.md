# 그룹의 사용자 관리

{% hint style="warning" %}
**이 기능은 현재 비공개 베타입니다.**
{% endhint %}

{% hint style="info" %}
**기능 가용성**

그룹은 엔터프라이즈 및 비즈니스 플랜에서 사용할 수 있습니다. 자세한 내용은 [요금제](https://snyk.io/plans/)를 참조하세요.
{% endhint %}

그룹 및 구성원 최상위 메뉴 옵션을 선택하여 그룹 구성원을 관리합니다.

![](<../../../.gitbook/assets/Screenshot 2022-04-26 at 05.38.32.png>)

As a Group Admin (see [managing-permissions.md](managing-permissions.md "mention")), you can:

그룹 관리자([managing-permissions.md](managing-permissions.md "mention") 참조)는 다음을 수행할 수 있습니다.

* [그룹 및 조직 구성원 보기](manage-users-in-your-organizations-1.md#undefined)
* [개별 회원 보기](manage-users-in-your-organizations-1.md#undefined-1)
* [보기 필터링 및 정렬](manage-users-in-your-organizations-1.md#undefined-2)
* [구성원 삭제](manage-users-in-your-organizations-1.md#undefined-3)
* [그룹 구성원을 그룹 관리자로 승격](manage-users-in-your-organizations-1.md#undefined-4)

{% hint style="warning" %}
외부 사용자를 그룹스에 직접 추가할 수 없습니다. 먼저 조직에 추가한 다음 그룹에 추가해야 합니다. 자세한 내용은 [manage-users-in-your-organizations.md](manage-users-in-your-organizations.md "mention")를 참조하십시오.
{% endhint %}

### 그룹 및 조직 구성원 보기

그룹 구성원 페이지에서 그룹과 연결된 모든 구성원, 해당 역할 및 인증 유형, 구성원인 조직 수를 찾을 수 있습니다.

그룹 수준에서 사용할 수 있는 두 가지 표준 역할(**그룹 구성원** 및 **그룹 관리자**)이 있습니다.\
그룹 관리자는 Snyk에서 모든 권한을 가집니다. [managing-permissions.md](managing-permissions.md "mention") 참. 그러나 그룹 구성원이 된다고 해서 사용자에게 직접 권한이 부여되는 것은 아닙니다. 조직 구성원으로 추가하거나 그룹 관리자로 승격해야 합니다.

![](<../../../.gitbook/assets/image (1) (1).png>)

### 개별 회원 보기

Click on each member to view more details about their memberships.

If the user is a **Group Member**, you can see their role for each of the orgs they are a member of. You can filter by role since a Group Member can have different roles for different orgs. You can also remove the user from the group or orgs by invoking the respective delete buttons.

![](../../../.gitbook/assets/Screenshot%202022-04-26%20at%2006.28.53.png)

For a **Group Admin**, they are by default added as Org Admin across all Organizations in your Group. You cannot change a group admin's role for a specific org, or delete them from one or more orgs. However, you can remove a group admin from the group using the **Remove from group** option.

![](../../../.gitbook/assets/Screenshot%202022-04-26%20at%2006.24.09.png)

### 보기 필터링 및 정렬

#### Filter views

Click the filter icon (<img src="../../../.gitbook/assets/Screenshot%202022-03-11%20at%2008.47.59.png" alt="" data-size="line">) to expand the filter sidebar, to filter members displayed, by role or authentication method:

![](../../../.gitbook/assets/Screenshot%202022-04-26%20at%2006.33.04.png)

#### Sort views

You can sort by Name, Authentication method, Role, and Date joined.

You can sort user views by clicking on the column heading:

![](../../../.gitbook/assets/Screenshot%202022-03-11%20at%2009.01.07.png)

### 구성원 삭제

To delete a member from the group:

1. Click the ![](../../../.gitbook/assets/Screenshot%202022-03-11%20at%2008.05.56.png) icon next to the user.
2. Click **Delete member from** _**your group's name**_ when prompted.

### 그룹 구성원을 그룹 관리자로 승격

You can promote a Group Member to a Group Admin by selecting the role dropdown next to them and choosing the Group Admin role.

![](../../../.gitbook/assets/Screenshot%202022-04-26%20at%2006.40.05.png)

{% hint style="warning" %}
If the user is not already a part of your group, you must first add that user as a member of at least one org; see [Add Members](manage-users-in-your-organizations.md#add-members). The user then appears here with the role as Group Member, so you can then promote the user to Group Admin.
{% endhint %}
