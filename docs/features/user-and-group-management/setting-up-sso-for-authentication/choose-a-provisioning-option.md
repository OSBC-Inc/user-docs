# 프로비저닝 옵션 선택

조직의 새 사용자가 Snyk에 액세스하는 방법을 결정합니다.

## 모두에게 개방

열기 옵션을 사용하면 모든 사용자는 SSO를 사용하여 로그인하여 Snyk에 자동으로 액세스할 수 있습니다. 선택한 그룹의 모든 조직에 액세스할 수 있습니다. 그들의 계정은 모두 동일한 역할로 프로비저닝되며 두 가지 옵션이 있습니다.

* **조직 관리자** 역할을 통해 모든 새 사용자는 다른 조직 관리자 및 공동 작업자를 관리하고, 그룹 보고서를 보고, 그룹 내 조직과 작업할 수 있습니다.
* **조직 협력자** 역할은 조직에 액세스할 수 있습니다.

Snyk Support에 새 사용자가 조직에 대해 **관리자** 역할 또는 **협력자** 역할을 맡을지 여부를 알립니다. 선택한 역할은 모든 사용자에게 적용됩니다.

## 초대 필요

초대 필요 또는 **그룹 구성원** 옵션을 사용하여 관리자는 사용자를 초대하거나 사용자가 조직에 대한 액세스를 요청할 수 있습니다.

사용자를 조직에 초대하는 방법에는 두 가지가 있습니다. 회원 초대 ([manage-users-in-your-organizations.md](../managing-users-and-permissions/manage-users-in-your-organizations.md "mention") 참조 또는 [API endpoint](https://snyk.docs.apiary.io/#reference/organizations/user-invitation-to-organization/invite-users)를 사용하여 프로세스를 자동화하십시오.

초대되지 않은 사용자가 SSO를 사용하여 로그인하는 경우 Snyk에 액세스할 수 있지만 관리자가 초대하거나 수동으로 조직에 추가할 때까지 프로젝트를 볼 수 없습니다. 새 사용자가 액세스를 요청할 수 있도록 적절한 담당자가 있는 조직 목록을 표시할 수 있습니다.

## 사용자 지정 매핑

{% hint style="info" %}
기능 가용성

이 기능은 엔터프라이즈 플랜에서 사용할 수 있습니다. 자세한 내용은 [요금제](https://snyk.io/plans/)를 참조하세요.
{% endhint %}

사용자 지정 규칙으로 사용자 계정을 프로비저닝할 수 있습니다.

Snyk 그룹마다 SSO를 다르게 구성할 수 있습니다. 또한 ID 공급자의 정보를 기반으로 사용자를 특정 조직 및 역할 할당에 매핑할 수 있습니다.

고객 성공 관리자 및 Snyk 기술 서비스와 협력하여 이 SSO 옵션 구현을 준비하십시오.

사용자 지정 매핑 옵션에 대해 자세히 알아보려면 영업 담당자에게 문의하십시오.
