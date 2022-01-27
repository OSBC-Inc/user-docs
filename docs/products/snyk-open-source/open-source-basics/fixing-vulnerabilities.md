# 취약점 수정

Snyk은 취약점에 대한 실행 가능한 수정 가이드를 제공합니다. 자세한 내용은 [remediate-your-vulnerabilities.md](../../../features/fixing-and-prioritizing-issues/issue-management/remediate-your-vulnerabilities.md "mention")를 참조하세요.&#x20;

Snyk은 다음 요청을 사용하여 취약점을 수정하는 워크플로우를 지원합니다.

* [Automatic pull / merge requests (PRs / MRs)](fixing-vulnerabilities.md#automatic-pull-merge-requests).
* [Manual pull / merge requests](fixing-vulnerabilities.md#manual-pull-merge-requests-for-a-project-code).

{% content-ref url="../../../features/fixing-and-prioritizing-issues/starting-to-fix-vulnerabilities/what-languages-do-we-support-fix-pull-requests-or-merge-requests.md" %}
[what-languages-do-we-support-fix-pull-requests-or-merge-requests.md](../../../features/fixing-and-prioritizing-issues/starting-to-fix-vulnerabilities/what-languages-do-we-support-fix-pull-requests-or-merge-requests.md)
{% endcontent-ref %}

### 자동 **pull / merge requests**

SCM(소스 코드 관리자)을 통해 가져온 프로젝트의 경우 Snyk은 다음 유형의 자동화된 pull / merge requests를 제공합니다.

* [Fix pull requests for new vulnerabilities](https://docs.snyk.io/snyk-open-source/open-source-basics/fix-pull-requests-for-new-vulnerabilities)
* [Fix pull requests to clear the backlog of vulnerabilities in priority order](fix-pull-requests-for-known-vulnerabilities-backlog.md)
* [Dependency upgrade pull requests](https://docs.snyk.io/snyk-open-source/dependency-management/upgrading-dependencies-with-automatic-prs)

### 프로젝트 코드에 대한 수동 pull / merge requests

Snyk UI를 사용하여 프로젝트에서 직접 PR/MR을 생성하기 위해 다음과 같은 절차를 진행합니다.

1. 프로젝트 목록에서 프로젝트로 이동
2. 파일 선택
3. **Open a Fix PR/MR** 또는 **Fix this vulnerability**를 선택하세요.
4. A preview screen appears, showing you what fixes will be applied
5. Click **Open a Fix PR** on this screen to generate the pull request

![](../../../.gitbook/assets/image18.png)
