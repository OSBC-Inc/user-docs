# Issues 탭

### 개요

**Issues** 탭에는 프로젝트 전체에서 알려진 모든 취약점 및 라이선스 불일치가 표시되며, 각 Issue에 대한 세부 정보와 영향을 받는 프로젝트 및 각 Issue를 해결할 수 있는 방법이 표시됩니다.

{% hint style="info" %}
각 기본 탭의 데이터는 보고 있는 그룹이나 조직뿐만 아니라 Reports 영역 상단에서 적용한 필터를 기반으로 표시됩니다.
{% endhint %}

기본적으로 Issue는 다음 예와 유사하게 Issue별로 그룹화되어 표시됩니다.

![](../../.gitbook/assets/mceclip0-31-.png)

{% hint style="info" %}
사용한 필터 및 검색을 기준으로 현재 보고 있는 Issue 수가 Issue 탭에 나타납니다.
{% endhint %}

#### 그룹화 및 그룹화 해제된 보기

기본 그룹화 보기를 사용하여 Issue당 영향을 받는 프로젝트 수와 프로젝트에 영향을 미치는 Issue의 종류 및 수를 검사하여 전반적인 조직의 전반적인 상태를 확인할 수 있습니다.

또는 **View issues ungrouped**를 클릭하여 데이터 그룹화를 해제하고, Issue가 발생한 각 프로젝트에 대해 별도의 행을 봅니다. 즉, 여러 프로젝트에 영향을 미치는 경우 동일한 Issue가 여러 번 나타날 수 있습니다. 이 그룹화되지 않은 보기는 영향을 받는 프로젝트에 대한 자세한 정보와 권장 수정 사항을 제공합니다.

{% hint style="info" %}
보기 간에 전환하려면 **View issues ungrouped** 또는 **View issues grouped**를 클릭합니다.
{% endhint %}

### Issues 탭 요소

#### All views

다음 필드는 두 보기(grouped 및 ungrouped)에 대해 나타납니다.

| Element          | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Severity         | <p>다음은 Issue와 관련된 심각도의 아이콘입니다.</p><p><img src="../../.gitbook/assets/image (3) (2).png" alt="">Critical</p><p><img src="../../.gitbook/assets/image (16).png" alt="">High</p><p><img src="../../.gitbook/assets/image (12).png" alt="">Medium</p><p><img src="../../.gitbook/assets/image (36).png" alt="">Low</p>                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Score            | [Snyk의 우선순위 점수](https://docs.snyk.io/features/fixing-and-prioritizing-issues/starting-to-fix-vulnerabilities/snyk-priority-score)입니다. Issue를 해결해야 할 순서를 안내하는 데 유용합니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| Issue            | Issue의 공식 이름과 프로젝트에 포함된 영향을 받는 모든 패키지 목록입니다. Issue는 Package 페이지에 연결되어 있습니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| Identifiers      | 연결된 모든 CVE 식별자입니다. 각 식별자는 관련성이 있을 경우 전체 공식 CVE 또는 CWE 취약점 세부 정보에 개별적으로 연결됩니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| Projects         | <p></p><p>그룹화되지 않은 Issue를 볼 때 이는 특정 Issue의 영향을 받는 모든 프로젝트의 전체 목록과 프로젝트 소스를 가리킵니다.</p><p>그룹화된 Issue를 보는 경우 이 열에는 해당 Issue의 영향을 받는 프로젝트 수가 표시됩니다.</p><p>해당 그룹의 영향을 받는 모든 프로젝트 목록이 표시되는 패널을 열려면 총 프로젝트 수를 클릭합니다. 이 보기의 세부 정보는 다음과 같습니다.</p><ul><li>Project</li><li>Status</li><li>Introduced - 프로젝트에서 Issue가 발견된 날짜</li><li>Fixable - 업그레이드 또는 패치로 Issue를 제거할 수 있는지 여부</li></ul>                                                                                                                                                                                                                                                                                                                                                                                            |
| Exploit maturity | <p></p><p>취약점에 대한 공격이 얼마나 실용적인지(<a href="../fixing-and-prioritizing-issues/issue-management/evaluating-and-prioritizing-vulnerabilities.md">취약점 평가 및 우선순위 지정</a> 참조)</p><ul><li><strong>Mature:</strong> 이 취약점에 쉽게 사용할 수 있는 공개된 코드 익스플로잇이 존재합니다.</li><li><strong>Proof of concept:</strong> 이 취약점을 악용하는 방법을 보여주는 공개된 이론적 개념 증명 또는 자세한 설명을 사용할 수 있습니다.</li><li><strong>No known exploit:</strong> 이 취약점에 대한 개념 증명 코드나 공격이 발견되지 않았거나 공개되지 않았습니다.</li><li><p><strong>No data</strong>: 이 값은 다음 중 하나를 나타냅니다.</p><ul><li>이 Issue는 취약점이 아니라 라이선스 문제입니다. - <a href="../../snyk-products/snyk-open-source/licenses/">라이선스선</a> 참고</li><li><del><em>에코시스템은</em></del> 현재 Snyk에서 지원하지 않습니다.</li><li>이 기능이 릴리즈되기 전에 프로젝트를 가져왔습니다. 이 데이터를 스캔하려면 프로젝트를 다시 가져오십시오.</li></ul></li></ul> |

#### Ungrouped view 전용

다음 필드는 그룹 해제된 Issue를 볼 때만 나타납니다.

| **Element**  | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| ------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Fixable      | <p>업그레이드 또는 패치를 사용하여 이 취약점을 해결할 수 있습니다.</p><p>(또한 <a href="https://support.snyk.io/hc/en-us/articles/4405034808209-Fixed-in-version-vs-fixable-attribute-in-vulnerabilities">버전에서 수정됨 vs. 취약점의 수정 가능한 속성</a> )</p><ul><li><strong>Patch</strong>: Snyk 패치로 해결할 수 있는 Issue</li><li><strong>Upgrade</strong>: 영향을 받는 패키지를 업그레이드하여 해결할 수 있는 Issue</li><li><strong>Pin</strong>: 간접 의존성을 직접 의존성으로 만들어 해결할 수 있는 Issue<br><strong>Note:</strong> 현재 Python에만 해당</li><li><strong>No</strong>: 현재 알려진 수정 사항이 없는 Issue</li></ul> |
| Introduced   | 프로젝트에 Issue가 도입된 날짜입니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| Status       | <p>취약점의 현재 상태입니다.</p><ul><li><strong>Open</strong>: 처리되지 않은 Issue</li><li><strong>Fixed</strong>: Snyk에 의해 자동으로 수정 PR이 제출된 Issue</li><li><strong>Patched</strong>: Snyk 패치로 해결된 Issue</li><li><strong>Ignored</strong>: 무시 정책이 적용되는 Issue</li></ul>                                                                                                                                                                                                                                                                     |
| Reachability | <p>코드에서 취약한 기능으로 가는 취약점 경로가 있는지 여부입니다. (<a data-mention href="../fixing-and-prioritizing-issues/prioritizing-issues/reachable-vulnerabilities.md">reachable-vulnerabilities.md</a> )</p><ul><li><strong>Reachable</strong>: 애플리케이션의 코드부터 취약한 기능까지 명확한 경로가 있습니다.</li><li><strong>Potentially reachable</strong>: 취약점에 노출될 수 있는 징후가 있습니다.</li><li><strong>No path found</strong>: 취약점에 도달할 수 있는지 여부를 결정할 수 있는 정보가 부족합니다.</li></ul>                                                                                        |
| Jira issue   | 프로젝트에 Jira 통합이 구성되어 있고 Snyk의 Issue에 대해 Jira Issue가 제기되면 이 열에 Jira key가 표시되고 Jira 내에서 동일한 Issue로 연결됩니다.                                                                                                                                                                                                                                                                                                                                                                                                                  |

### Issues 탭 작업

다음 작업은 아래와 같습니다.

![](../../.gitbook/assets/uuid-ef7a494d-8b10-9b28-dc63-3f9224519070-en.png)

**Issues 검색:** CVE, CWE 또는 식별자 이름(즉, DDoS)을 기준으로 검색할 수 있습니다. CVE 또는 CWE로 검색할 때 정확한 값(예: CVE-1234)를 제공해야 하지만 식별자 이름을 검색할 때 단어의 일부를 입력하면 결과가 반환됩니다.

**Issue filters:** **Issues tab elements**에 설명된 대로 우선순위 점수 범위, 특정 Issue 유형, 악용 성숙도, 상태, 고정 가능한 값 및 도달 가능성을 선택하여 표시할 Issue를 표시합니다.

![](../../.gitbook/assets/screenshot\_2020-07-30\_at\_11.30.19\_am.png)

**Export** - Issue 데이터를 내보낼 형식을 선택하려면 버튼을 클릭합니다.

* CSV
* 로컬 환경의 Print 창에서 미리 보기를 인쇄/생성합니다. 생성하는 데 몇 초 정도 걸릴 수 있습니다.

{% hint style="warning" %}
한 번에 2,000개의 Issue만 생성할 수 있습니다.
{% endhint %}
