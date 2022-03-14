# 프로젝트 issues, fixes, dependencies 확인

프로젝트에서 다음 정보를 확인할 수 있습니다.

* **Issues:** 취약점 및 라이선스 문제의 수.
* **Fixes**: 취약점에 대해서 수정을 진행합니다.
* **Dependencies**: 직접 및 전이(충첩) 종속성의 총 수.

### Issues 확인

프로젝트 요약 세부 정보 아래 **Issues** 탭에서 취약점 및 라이선스 문제를 확인할 수 있습니다.

![](<../../.gitbook/assets/Screenshot 2021-10-19 at 11.49.30.png>)

왼쪽 영역을 사용하여 문제를 필터링하고 검색합니다. 체크박스를 통해 **문제 유형, 심각도, 공격 영향도, 상태** 별로 필터링합니다. **우선 순위 점수** 표시 범위를 슬라이더를 이용하여 변경할 수 도 있습니다.(기본적으로 0 \~ 1000으로 설정).

issue 세부 정보는 우선 순위 점수별로 정렬된 영역에 나타납니다. **View Issue Details**를 참조하세요.

#### Fix issues (PR 수)

Snyk은 **Issues**와 **Fixes** 탭의 **Open a fix PR** 섹션에 표시된 대로 스캔 중에 식별된 문제를 수정하는 기능을 제공합니다.

![](../../.gitbook/assets/image27.png)

**Fix this vulnerability**를 클릭하여 특정 Issues를 수정하도록 선택할 수 있습니다.

![](../../.gitbook/assets/image26.png)

개요는 [취약점 수정](../../products/snyk-open-source/open-source-basics/fixing-vulnerabilities.md)을 참조하세요.\
자세한 내용은 [Fixing and prioritizing issues](../../features/fixing-and-prioritizing-issues/)를 참조하세요.

#### Issues 세부정보 확인

각 Issues에 대해 우선 순위 점수를 포함한 취약점의 세부 정보를 표시합니다([Snyk 우선순위 점수](../../features/fixing-and-prioritizing-issues/starting-to-fix-vulnerabilities/snyk-priority-score.md) 참조).

![](../../.gitbook/assets/image12.png)

**More about this issue**를 클릭하면 [Snyk's vulnerability database](https://snyk.io/product/vulnerability-database/)를 사용하여 취약점에 대한 자세한 정보를 확인할 수 있으며 CVSS 점수를 포함하여 문제에 대한 더 자세한 사항을 확인할 수 있습니다.

![](../../.gitbook/assets/image15.png)

### Fixes 확인

**Fixes**탭에서 프로젝트의 전이 종속성에 대한 Snyk을 통해 수정 가이드를 제공합니다.

![](<../../.gitbook/assets/Screenshot 2021-10-19 at 11.57.07.png>)

자세한 내용은 [취약점 수정](../../products/snyk-open-source/open-source-basics/fixing-vulnerabilities.md)을 참조하세요.

### Dependencies 확인

Snyk은 애플리케이션의 패키지 관리자를 사용하여 디펜던시 트리를 빌드하고 프로젝트의 **dependency** 탭에 표시합니다. 이는 어떤 구성 요소가 취약점을 가지고 있는지 확인할 수 있으며 디펜던시가 애플리케이션에 어떻게 도입되었는지 제공합니다.

![](../../.gitbook/assets/image23.png)

예를 들어 위 내용에서 직접 종속성 **body-parser@ 1.9.0**에서 가져온 전이 종속성 **qs@2.2.4**에 기반한 취약점을 나타냅니다.
