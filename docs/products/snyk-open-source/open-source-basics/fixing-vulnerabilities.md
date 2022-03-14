# 취약점 수정

Snyk은 취약점에 대한 실행 가능한 수정 가이드를 제공합니다. 자세한 내용은 [Fix your vulnerabilities](../../../features/fixing-and-prioritizing-issues/issue-management/remediate-your-vulnerabilities.md)를 참조하십시오.

Snyk은 다음 요청을 사용하여 취약점을 수정하는 워크플로우를 지원합니다.

* [Automatic pull / merge requests (PRs / MRs)](fixing-vulnerabilities.md#pull-merge-requests).
* [Manual pull / merge requests](fixing-vulnerabilities.md#pull-merge-requests-1).

{% content-ref url="../../../features/fixing-and-prioritizing-issues/starting-to-fix-vulnerabilities/what-languages-do-we-support-fix-pull-requests-or-merge-requests.md" %}
[what-languages-do-we-support-fix-pull-requests-or-merge-requests.md](../../../features/fixing-and-prioritizing-issues/starting-to-fix-vulnerabilities/what-languages-do-we-support-fix-pull-requests-or-merge-requests.md)
{% endcontent-ref %}

### 자동 **pull / merge requests**

SCM(소스 코드 관리자)을 통해 가져온 프로젝트의 경우 Snyk은 다음 유형의 자동화된 pull / merge requests를 제공합니다.

* [새로운 취약점에 대한 pull requests 수정](fix-pull-requests-for-new-vulnerabilities.md)
* [우선 순위 순서로 취약점의 백로그를 지우도록 pull requests 수정](fix-pull-requests-for-known-vulnerabilities-backlog.md)
* [디펜던시 업그레이드 pull requests](../dependency-management/upgrading-dependencies-with-automatic-prs.md)

### 프로젝트 코드에 대한 수동 pull / merge requests

Snyk UI를 사용하여 프로젝트에서 직접 PR/MR을 생성하기 위해 다음과 같은 절차를 진행합니다.

1. 프로젝트 목록에서 프로젝트로 이동합니다.
2. 파일을 선택합니다.
3. **Open a Fix PR/MR** 또는 **Fix this vulnerability**를 선택하십시오.
4. 적용할 수정 사항을 보여주는 미리 보기 화면이 나타납니다.
5. 이 화면에서 **Open a Fix PR**을 클릭하여 pull request를 생성합니다.

![](../../../.gitbook/assets/image18.png)
