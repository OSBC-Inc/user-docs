# Issue 해결 및 우선순위 지정

Snyk은 취약점 및 라이선스 컴플라이언스 Issue를 찾는 데 그치지 않습니다. 우선순위 점수, 보고서 및 정책 설정 기능을 통해 가장 중요한 Issue의 우선순위를 지정하고 먼저 해결할 수 있습니다.

### 우선순위 점수 사용

[Snyk 우선순위 점수는](starting-to-fix-vulnerabilities/snyk-priority-score.md) Kubernetes 구성 데이터 및 실행 중인 컨테이너의 신호를 포함한 여러 업계 표준 기준에 따라 Issue의 우선순위를 지정합니다.

![](../../.gitbook/assets/image%20\(86\)%20\(2\).png)

### 프로젝트 속성 적용 <a href="#h.r3thgse7qt7n" id="h.r3thgse7qt7n"></a>

다음과 같은 [프로젝트 속성](../../getting-started/introduction-to-snyk-projects/view-project-information/project-attributes.md)을 적용하여 세분화된 수준에서 우선순위를 제어합니다.

* Lifecycle stage
* Business criticality
* Environment

### Issue 정리

Snyk의 [보고서 기능](../../introducing-snyk/snyks-core-concepts/reporting.md)을 사용하면 필요한 Issue, 디펜던시 및 라이선스의 상태를 최신 상태로 유지할 수 있으며 그렇지 않은 [Issue는 무시](issue-management/ignore-issues.md)할 수 있습니다.

![](../../.gitbook/assets/image%20\(66\)%20\(4\).png)

### reachability 평가 <a href="#h.ts3kx23p4m7p" id="h.ts3kx23p4m7p"></a>

Snyk의 [도달 가능한 취약점](prioritizing-issues/reachable-vulnerabilities.md) 스캔을 사용하여 취약한 함수가 애플리케이션에서 호출되는지 여부를 식별하여 위험을 측정합니다.

### 보안 정책 설정

사용자 정의 가능한 [보안 정책](security-policies/) 통해 자동으로 특정 취약점에 대한 우선순위를 지정하거나 우선순위를 낮춥니다.

![](../../.gitbook/assets/image%20\(82\)%20\(3\).png)

### Issue 해결

Issue 우선순위를 결정했으면 이제 [취약점 수정](starting-to-fix-vulnerabilities/)을 시작할 때입니다.

Snyk은 업그레이드를 위한 자동 PR을 생성하고 권장 수정 사항을 제안할 수 있습니다. Snyk이 패치 및 직접 의존성 업그레이드를 통해 코드 보안을 유지하는 방법에 대한 자세한 내용은 [remediate-your-vulnerabilities.md](issue-management/remediate-your-vulnerabilities.md "mention")을 참조하십시오.
