# 권한 관리

{% hint style="info" %}
**기능 가용성**

무료 구독 플랜을 사용하면 7일마다 최대 200개의 보류 중인 초대를 보낼 수 있으며 관리자 역할만 있습니다. 엔터프라이즈 플랜에는 관리자와 공동 작업자가 있습니다. 자세한 내용은 [요금제](https://snyk.io/plans/)를 참조하세요.
{% endhint %}

권한을 편집하려면 관련 권한이 스스로 필요합니다. 예를 들어 그룹 관리자만 다른 사용자를 그룹 관리자로 지정할 수 있습니다.

회사에 현재 그룹 관리자가 없는 경우 [Snyk 지원](https://support.snyk.io/hc/en-us/requests/new)에 최소 한 명의 사용자를 승격하도록 요청해야 합니다.

### 역할 변경

사용자의 역할을 변경하려면:

1. Click on the **Members** tab in the Snyk Web UI (example link: **https://app.snyk.io/org/your-org-name/manage/members**)
2. Find the member to update
3. Update the role for that member, using the dropdown next to role

### Permissions per role

| User permissions                               | Group Administrator | Organization Administrator | Organization Collaborator |
| ---------------------------------------------- | ------------------- | -------------------------- | ------------------------- |
| Add/delete projects                            | x                   | x                          | x                         |
| Update project with new snapshot               | x                   | x                          | x                         |
| Open fix PR's                                  | x                   | x                          | x                         |
| Delete snapshot from project history           | x                   | x                          | x                         |
| Invite/remove team members                     | x                   | x                          |                           |
| Change team members’ roles                     | x                   | x                          |                           |
| Create an org level service account\*          | x                   | x                          |                           |
| Manage plans and billing for this organization | x                   | x                          |                           |
| Leave organization                             | x                   | x                          | x                         |
| Delete organization                            | x                   | x                          |                           |
| View organization reporting                    | x                   | x                          | x                         |
| Create an organization                         | x                   |                            |                           |
| Create group level Service accounts\*          | x                   |                            |                           |
| Set a License policy\*                         | x                   |                            |                           |
| Set a Security policy\*\*                      | x                   |                            |                           |
| Set global notifications preferences           | x                   |                            |                           |
| Access to the account overall reporting        | x                   |                            |                           |

(\*) Only in paid accounts\
(\*\*) Only in Enterprise Plan
