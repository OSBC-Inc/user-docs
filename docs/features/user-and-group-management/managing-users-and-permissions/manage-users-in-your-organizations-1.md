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

각 회원을 클릭하면 회원에 대한 자세한 내용을 볼 수 있습니다.

사용자가 **그룹 구성원**인 경우 구성원인 각 조직에 대한 역할을 볼 수 있습니다. 그룹 구성원은 조직마다 다른 역할을 가질 수 있으므로 역할별로 필터링할 수 있습니다. 해당 삭제 버튼을 호출하여 그룹 또는 조직에서 사용자를 제거할 수도 있습니다.

![](<../../../.gitbook/assets/image (2).png>)

**그룹 관리자**의 경우 기본적으로 그룹의 모든 조직에서 조직 관리자로 추가됩니다. 특정 조직에 대한 그룹 관리자의 역할을 변경하거나 하나 이상의 조직에서 삭제할 수 없습니다. 그러나 그룹에서 제거 옵션을 사용하여 그룹에서 **그룹 관리자를 제거**할 수 있습니다.

### 보기 필터링 및 정렬

**보기 필터링**

Click the filter icon (<img src="../../../.gitbook/assets/Screenshot%202022-03-11%20at%2008.47.59.png" alt="" data-size="line">) to expand the filter sidebar, to filter members displayed, by role or authentication method:

![](<../../../.gitbook/assets/Screenshot 2022-04-26 at 06.33.04.png>)

**보기 정렬**

이름, 인증 방법, 역할, 가입 날짜별로 정렬할 수 있습니다.

열 머리글을 클릭하여 사용자 보기를 정렬할 수 있습니다:

![](<../../../.gitbook/assets/spaces\_-MdwVZ6HOZriajCf5nXH\_uploads\_git-blob-06ff515c5fc71e1a8bcc045d0803b12ee54e23fb\_Screenshot 2022-03-11 at 09.01.07 (1).png>)

### 구성원 삭제

그룹에서 구성원을 삭제하려면:

1. 사용자 옆에 있는 ![](../../../.gitbook/assets/Screenshot%202022-03-11%20at%2008.05.56.png) 아이콘을 클릭합니다.
2. 메시지가 표시되면 **Delete member from** _**your group's name**_를 클릭합니다.

### 그룹 구성원을 그룹 관리자로 승격

그룹 구성원 옆에 있는 역할 드롭다운을 선택하고 그룹 관리자 역할을 선택하여 그룹 구성원을 그룹 관리자로 승격할 수 있습니다.

![](<../../../.gitbook/assets/Screenshot 2022-08-09 at 12.40.00.png>)

{% hint style="warning" %}
사용자가 아직 그룹의 일부가 아닌 경우 먼저 해당 사용자를 하나 이상의 조직 구성원으로 추가해야 합니다. [구성원 추가](manage-users-in-your-organizations.md#undefined)를 참조하십시오. 그러면 사용자가 그룹 구성원 역할로 여기에 나타나므로 사용자를 그룹 관리자로 승격할 수 있습니다.
{% endhint %}
