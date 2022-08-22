---
description: "각 SCM 스크립트의 \bFlag"
---

# Flags

| SCM             | Credentials         | Orgs            | Repo        | Exclusion File Path   | Json     | Skip Snyk monitored repos  | Import file folder path | Repo type for import file | Additional flags                                |
| --------------- | ------------------- | --------------- | ----------- | --------------------- | -------- | -------------------------- | ----------------------- | ------------------------- | ----------------------------------------------- |
| **Azure**       | `"token"`           | `"projectKeys"` | `"repo"`    | `"exclusionFilePath"` | `"json"` | `"skipSnykMonitoredRepos"` | `"importConfDir"`       | `"importFileRepoType"`    | `"org" [required]`                              |
| **BB Cloud**    | `"user"/"password"` | `"workspaces"`  | `"repo"`    | `"exclusionFilePath"` | `"json"` | `"skipSnykMonitoredRepos"` | `"importConfDir"`       | `"importFileRepoType"`    |                                                 |
| **BB Server**   | `"token"`           | `"projectKeys"` | `"repo"`    | `"exclusionFilePath"` | `"json"` | `"skipSnykMonitoredRepos"` | `"importConfDir"`       | `"importFileRepoType"`    | `"url" [required]`                              |
| **GitHub**      | `"token"`           | `"orgs"`        | `"repo"`    | `"exclusionFilePath"` | `"json"` |                            |                         |                           |                                                 |
| **GitHub Ent.** | `"token"`           | `"orgs"`        | `"repo"`    | `"exclusionFilePath"` | `"json"` |                            |                         |                           | `"url" [required], "fetchAllOrgs" [optional]**` |
| **GitLab**      | `"token"`           | `"groups"`      | `"project"` | `"exclusionFilePath"` | `"json"` |                            |                         |                           |                                                 |
| **GitLab Ent.** | `"token"`           | `"groups"`      | `"project"` | `"exclusionFilePath"` | `"json"` |                            |                         |                           | `"url" [required]`                              |

{% hint style="info" %}
Flag 이름은 SCM에 있는 flag 이름과 일치합니다. Bitbucket 서버, GitHub Enterprise 및 GitLab Enterprise와 같은 "Private" SCM은 명령에서 flag로 설정될 호스트 URL이 필요합니다.
{% endhint %}

{% hint style="info" %}
"`fetch AllOrgs`" flag는 깃허브 엔터프라이즈에 고유하며 GHE에서 Orgs에 대한 두 가지 접근 level을 구분합니다.\
1\. With the flag - 제공된 토큰이 액세스할 수 있는 모든 Orgs를 가져옵니다.\
2\. Without the flag - 토큰이 제공된 **사용자**에게 일부 작업 권한(예: 읽기 권한 등)이 있는 Orgs만 가져옵니다.
{% endhint %}

{% hint style="info" %}
생성된 import file을 synk-api-import tool로 사용하는 방법에 대한 자세한 내용은 [import file 생성 및 사용](creating-and-using-the-import-files.md)을 참조하십시오.
{% endhint %}
