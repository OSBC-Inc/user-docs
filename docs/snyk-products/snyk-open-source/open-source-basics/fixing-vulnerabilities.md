# 취약점 수정

Snyk은 취약점에 대한 실행 가능한 수정 가이드를 제공합니다. 자세한 내용은 [취약점 수정](broken-reference)을 참조하십시오.

Snyk은 다음을 사용하여 취약점을 수정하는 워크플로우를 지원합니다.

* [자동 pull / merge requests (PR/MR)](fixing-vulnerabilities.md#pull-merge-requests-pr-mr)
* [수동 pull / merge requests (PR/MR)](fixing-vulnerabilities.md#pull-merge-requests)

{% content-ref url="broken-reference" %}
[Broken link](broken-reference)
{% endcontent-ref %}

### 자동 **pull / merge requests** (PR/MR)

SCM(Source Code Manager)을 통해 가져온 프로젝트의 경우 Snyk은 다음 유형의 자동화된 PR/MR을 제공합니다.

* [새로운 취약점에 대한 pull requests 수정](fix-pull-requests-for-new-vulnerabilities.md)
* [pull request를 수정하여 알려진 취약점을 우선순위로 처리](fix-pull-requests-for-known-vulnerabilities-backlog.md)
* [디펜던시 업그레이드 pull requests](../dependency-management/upgrading-dependencies-with-automatic-prs.md)

### 프로젝트 코드에 대한 수동 pull / merge requests (PR/MR)

Snyk UI를 사용하여 프로젝트에서 직접 PR/MR을 생성하려면 다음과 같이 진행해야 합니다.

1. 프로젝트 목록에서 프로젝트로 이동합니다.
2. 특정 파일을 선택합니다.
3. **Open a Fix PR/MR** 또는 **Fix this vulnerability**를 선택합니다.
4. 적용할 수정 사항을 보여주는 미리 보기 화면이 나타납니다.
5. 이 화면에서 **Open a Fix PR**을 클릭하여 pull request를 생성합니다.

![](../../../.gitbook/assets/image18.png)
