# 사용자 지정 매핑 옵션

이 옵션을 사용하면 IdP(Identity Provider)가 제공하는 데이터를 기반으로 Snyk 그룹 및 조직에 사용자를 동적으로 할당하여 확장된 사용자 프로비저닝 및 액세스 모델을 구현할 수 있습니다. Snyk 내 역할 및 권한에 대한 자세한 내용은 [이 문서](../managing-users-and-permissions/managing-permissions.md)를 참조하십시오. 이 옵션을 구현하려면 Customer Success Manager와 협력하십시오.

### 요구 사항

* [여기](set-up-snyk-single-sign-on-sso.md)에 있는 해당 IdP에 대한 SSO 정보 워크시트 작성
* 역할 배열 매핑을 채우기 위한 IdP 내 사용자 정의 속성의 적절한 구성([아래](custom-mapping-option.md#example-roles-array-mapping) 예)

### 역할 배열 매핑 이해

IdP 내에서 먼저 역할이라는 사용자 지정 매핑을 문자열 배열로 전달해야 합니다. [다음은 Okta에서 사용자 지정 매핑을 구성하는 방법에 대한 예제 문서입니다](example-setting-up-custom-mapping-for-okta.md). 추가 IdP 공급자에 대한 사용자 지정 매핑을 구성하는 방법에 대한 IdP 설명서를 참조하십시오.

### Snyk이 역할 배열 매핑을 처리하는 방법

이 옵션을 구성하려면 다음 패턴 중 하나를 준수하도록 SAML 속성 또는 OIDC 클레임 내에서 `roles` 배열을 보내야 합니다.

**1. {prefix}-groupadmin**

* 이 역할 매핑은 그룹 관리자 및 조직 관리자 역할을 가진 사용자를 할당합니다.
* **접두사**는 모든 역할 매핑에 있습니다. Snyk이 처리할 `roles` 배열 값을 식별할 수 있도록 하는 식별자입니다. 기본적으로 이 값은 **snyk**입니다. 다른 값이 필요한 경우 Customer Success Manager와 협력하십시오.
  * Note: **접두사**는 완전히 소문자여야 합니다.
* **groupadmin**은 이 역할을 가진 모든 사용자를 사용자가 할당된 모든 그룹과 그룹에 속하는 모든 조직에 대한 그룹 관리자 및 조직 관리자로 구성합니다.

**2. {prefix}-{groupID}**

* 이 역할 매핑은 지정된 그룹 아래의 모든 조직에 대해 조직 협력자 역할을 가진 사용자를 할당합니다.
* **groupID**는 Snyk의 그룹에 대한 ID 문자열입니다(그룹 수준의 snyk URL에서 찾을 수 있음).
  * Group ID를 찾는 방법: https://app.snyk.io/group/\<Group ID> 또는 Group dropdown -> ![](../../../.gitbook/assets/cog\_icon.png) -> General -> Group ID

**3.** **{prefix}-{orgslug}-{role}**

* 이 역할 매핑은 **orgslug**에 지정된 Snyk 조직에 대해 지정된 협업자 또는 관리자 역할을 가진 사용자를 할당합니다.
* **orgslug**는 Snyk에서 조직 이름의 고유 식별자입니다.
  * **orgslug**를 찾는 방법: https://app.snyk.io/org/{orgslug} 또는 [API](https://snyk.docs.apiary.io/#reference/groups/list-all-organizations-in-a-group/list-all-organizations-in-a-group)를 통해 (Note: **orgslug**는 대부분의 경우 조직의 이름이지만 항상 그런 것은 아닙니다.)
  * Note: **orgslug**는 최대 60자의 값이 될 수 있으며 완전히 소문자여야 합니다.
* **역할**은 **공동 작업자** 또는 **관리자**입니다.

### 역할 배열 매핑 형식

그룹 관리자 역할이 있는 사용자를 할당하려면 다음 형식을 사용하십시오.

```
{
    "roles": [
        "{prefix}-groupadmin"
    ]
}
```

조직 공동 작업자 역할이 있는 사용자를 지정하려면 다음 형식을 사용하십시오.

```
{
    "roles": [
        "{prefix}-{groupID}"
    ]
}
```

사용자를 조직 관리자 또는 조직 공동 작업자로 지정하려면 역할 배열에 다음 형식을 사용하십시오.\
\
Note: 조직별로 다른 역할을 할당할 수 있습니다. 아래 예에서는 사용자를 **orgslug** 조직의 조직 관리자로 할당하지만 **orgslug2** 조직의 공동 작업자를 할당합니다.

```
{
    "roles": [
        "{prefix}-{orgslug}-admin",
        "{prefix}-{orgslug2}-collaborator"
    ]
}
```

### 역할 배열 매핑의 예

다음 예는 매핑 규칙에 따라 Snyk 사용자에게 역할을 할당하는 방법을 보여줍니다.

* 고객의 이름은 ABC이고 ABC라는 그룹이 하나 있습니다.
* 고객은 Snyk 내에 Application-SecurityScanner1, Partner-Plugins 및 Application-Payments의 3개 조직이 있습니다.
* 고객은 서로 다른 요구를 가진 비즈니스 개발, 엔지니어링, 보안 및 제품의 4개 팀이 있습니다.:
  * 비즈니스 개발 팀은 ABC 그룹에 액세스할 수 있어야 하며 Partner-Plugins 조직만 Org Admin으로 액세스해야 합니다.
  * 엔지니어링은 ABC 그룹, Application-SecurityScanner1 조직을 Org Admin으로, Partner-Plugins 조직을 Org Admin으로, Application-Payments를 Org Collaborator로 액세스해야 합니다.
  * 보안은 그룹 관리자로 ABC 그룹에 액세스하고 조직 관리자로 3개 조직 모두에 액세스해야 합니다.
  * 제품 팀은 조직 협력자로서 ABC 그룹 및 3개 조직 모두에 액세스할 수 있어야 합니다.

비즈니스 개발 팀의 경우 {prefix}-{orgslug}-{role} 매핑을 사용합니다.

```
{
    "roles": [
        "snyk-partner-plugins-admin"
    ]
}
```

엔지니어링 팀의 경우 {prefix}-{orgslug}-{role} 매핑을 사용합니다.

```
{
    "roles": [
        "snyk-application-securityscanner1-admin",
        "snyk-partner-plugins-admin",
        "snyk-application-payments-collaborator"
    ]
}
```

보안 팀의 경우 {prefix}-groupadmin 매핑을 사용합니다.

```
{
    "roles": [
        "snyk-groupadmin"
    ]
}
```

제품 팀의 경우 groupID 값을 삽입해야 하는 {prefix}-{groupID} 매핑을 사용할 것입니다.

```
{
    "roles": [
        "snyk-{groupID}"
    ]
}
```

### 사용자 지정 매핑의 역할 요약 다이어그램

![](../../../.gitbook/assets/custom-mapping-screenshot.png)
