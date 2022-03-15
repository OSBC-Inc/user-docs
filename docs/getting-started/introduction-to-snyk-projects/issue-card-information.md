# Issue card

Issue card는 프로젝트의 세부 정보 페이지에 나타납니다. [프로젝트 정보 확인](view-project-information.md)을 참조하세요.

Issue card는 특정 취약점 또는 라이선스 문제에 대한 세부 정보와 이에 대한 해결 방안을 제시합니다.

![](../../.gitbook/assets/screenshot\_2021-03-01\_at\_16.19.01.png)

Header 섹션 정보는 다음과 같습니다.

![](../../.gitbook/assets/issue-card-header.png)

* [**Severity level**](../../introducing-snyk/snyks-core-concepts/severity-levels.md): 심각도 수준. 예: H (높음)
* **Issue name**: Issue 명
* **Score**: [우선순위 점수](../../features/fixing-and-prioritizing-issues/starting-to-fix-vulnerabilities/snyk-priority-score.md). 0 \~ 1,000점까지 존재.
* **Type**: 취약점 또는 라이선스 Issue.
* [CWE](https://cwe.mitre.org/index.html) (Common Weakness Evaluation), [CVSS](https://www.first.org/cvss/calculator/3.1) (Common Vulnerability Scoring System)와 해당 Issue에 대한 Snyk [Intel Vulnerability DB](https://snyk.io/vuln) 정보.
* **Social Trends**: Twitter에서 활발하게 논의되고 있는 문제에 대한 [Trending banner](../../features/fixing-and-prioritizing-issues/prioritizing-issues/prioritize-by-social-trends.md)입니다.

Body 섹션 정보는 다음과 같습니다.

![](../../.gitbook/assets/issue-card-body.png)

* **Introduced through**: 취약점이나 라이선스가 유입된 경로.
* **Fixed in:** 취약점이 수정된 파일.
* [Exploit maturity](../../features/fixing-and-prioritizing-issues/issue-management/evaluating-and-prioritizing-vulnerabilities.md): 공격 영향도.
* [Reachability](../../features/fixing-and-prioritizing-issues/prioritizing-issues/reachable-vulnerabilities.md): for example, **Reachable**.

추가 정보를 위해 card를 펼치면 다음 정보를 확인할 수 있습니다.

![](../../.gitbook/assets/screenshot\_2021-03-01\_at\_16.08.49.png)

* 자세한 경로 정보
* 수정 방안
* 취약점 개요
* 취약점 내의 모든 취약한 기능

프로젝트에 여러 필터를 적용하여 일련의 문제를 표시할 수 있습니다.

* 특정 취약점 또는 라이선스 지정
* 특정 심각도 수준 지정
* 우선순위 점수 범위 설정
* 공격 영항도 여부와 수준 설정
* open거나 패치되었거나 무시된 항목

프로젝트의 Issue card는 우선순위 점수 또는 심각도에 따라서 정렬할 수 있습니다.

## Card 작업 수행

Issue card에서 다음 작업을 수행할 수 있습니다.

* ****[**Ignore the issue**](../../features/fixing-and-prioritizing-issues/starting-to-fix-vulnerabilities/introduction-to-ignoring-issues.md): 문제에 대해서 조치를 취하거나 보고서에 표시할 필요가 없는경우 무시할 수 있습니다.
* ****[**Create a Jira ticket**](../../features/integrations/notifications-ticketing-system-integrations/jira.md): [Jira integration](../../features/integrations/notifications-ticketing-system-integrations/jira.md)이 있는 경우 issue board에 Snyk을 연결하고 프로젝트 세부 정보 페이지에서 직접 jira 티켓을 생성하여 취약점을 수정할 수 있습니다.
* [취약점 수정](../../products/snyk-open-source/open-source-basics/fixing-vulnerabilities.md): 취약점에 대한 수정 사항이 있는 경우 개별 취약점을 수정할 수 있습니다.
* **View more information about the CWE, CVE, and CVSS score**: Issue card에서 CWE, CVE, CVSS점수에 대한 추가 정보를 확인할 수 있습니다.
* **View the Snyk vulnerability database:** Issue card에서 특정 취약점에 대한 Snyk vulnerability database로 이동합니다.
