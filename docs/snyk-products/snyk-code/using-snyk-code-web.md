# 웹을 통해 Snyk Code 사용

## 프로젝트 취약점 보기

표준 Snyk 웹 인터페이스와 함께 Snyk Code를 사용하여 코드의 취약점을 찾아 수정합니다.

1. **Project** 영역에서 프로젝트를 선택합니다.
2. Snyk Code는 해당 프로젝트에 대한 정보 및 취약점 카드를 표시합니다.

![](../../.gitbook/assets/snykcofe\_priority\_score.png)

제공되는 정보는 다음을 포함하여 표준 Snyk 프로젝트 정보를 보여줍니다.([Snyk projects](https://support.snyk.io/hc/en-us/sections/360004724958-Snyk-projects) 참조).

* 프로젝트가 마지막으로 테스트된 시간을 보여주는 스냅샷 정보입니다.
* **Overview**, **History** 및 **Settings** 정보. 예를 들어, **History** 섹션을 사용하여 프로젝트의 이전 스냅샷을 볼 수 있습니다.
* 화면 왼쪽에는 있는 필터가 있습니다.

## 취약점 카드 세부 정보

각 취약점 카드에는 해당 취약점에 대한 구체적인 세부 정보가 표시됩니다.

![](../../.gitbook/assets/snykcode\_issue\_card.png)

카드 세부 정보는 다음과 같습니다.

* 심각도 수준(예: 높음을 나타내는 **H**), 이름(예: **Cross-site Scripting**) 및 [우선 순위 점수](https://docs.snyk.io/fixing-and-prioritizing-issues/starting-to-fix-vulnerabilities/snyk-priority-score) 값입니다.
* [CWE 유형:](https://cwe.mitre.org/data/index.html) 링크를 클릭하여 해당 유형의 취약점에 대한 자세한 정보를 볼 수 있습니다.
* 취약한 영역을 정확히 보여주는 코드 스니펫입니다.
* 취약점에 대한 명확하고 유용한 텍스트 설명입니다.

자세한 내용은 [Issue card information](https://docs.snyk.io/getting-started/introduction-to-snyk-projects/issue-card-information)를 참조하십시오.

* 이 취약점을 무시하려면 **Ignore**을 클릭합니다. ([Ignore a vulnerability](using-snyk-code-web.md) 참조)
* 자세한 정보를 보려면 **Full details**를 클릭합니다. ([View full details](using-snyk-code-web.md) 참조)

## 전체 세부 정보 보기

자세한 정보를 보려면 취약점 카드에서 **Full details**를 클릭합니다.

![Data flow page preview.](../../.gitbook/assets/data-flow.png)

![Fix analysis page preview.](../../.gitbook/assets/fix-analysis.png)

전체 세부 정보에는 취약점 카드의 모든 정보와 다음과 같은 정보가 포함됩니다:

* **Data Flow**: 이 영역에서는 소스(사용자 입력)에서 싱크(클린한 입력을 받아야 하며 다른 방법으로 악용될 수 있는 작업)에 이르기까지 코드의 전체 issue 흐름을 보여줌으로써 문제가 어디에 있고 애플리케이션 전체에 걸쳐 어떻게 흘러가는지를 이해하는 데 도움이 됩니다. 위의 예에서 개발자는 입력을 검사하지 않았으므로 공격자가 Path Traversal을 통해 암호 파일과 같은 중요한 데이터를 포함하여 파일 시스템의 모든 파일에 액세스할 수 있습니다.
* **Fix Analysis:** 이 영역에서는 issue와 수정 방법에 대한 자세한 정보를 제공합니다. 개발자는 이 취약점 유형에 대한 수정 관련 정보, 취약점 개요 정보(이해 및 접근 방식) 및 수정 사례를 볼 수 있습니다.
* 원본 파일에 대한 링크를 열어 직접 변경할 수 있습니다. ([Open the source code file](using-snyk-code-web.md) 참조).
* 영향을 받는 코드를 보여주는 전체 창으로, **Data flow** 정보에 따라 특정 줄이 강조 표시됩니다.

## 관련 소스코드 파일 열기

1.  소스코드 파일 자체를 열려면 코드 링크를 클릭하십시오 (예: GitHub)

    ![](../../.gitbook/assets/link.png)
2. 파일이 열리고 취약점을 수정할 정확한 위치가 표시됩니다. (in this example, by adding the sanitation required to the input).
3. 이제 필요에 따라 수정하여 코드의 취약점을 해결할 수 있습니다.

![](../../.gitbook/assets/open-code2.png)

## 예: Cross-site Scripting (XSS)

이것은 일반적인 취약점인 Cross-site Scripting (XSS)의 예를 보여줍니다. XSS 취약점으로 인해 공격자는 애플리케이션의 기능 및 데이터에 대한 제어 권한을 확보하는 등 사용자가 애플리케이션과 상호 작용하는 것을 손상시킬 수 있습니다.

취약점 카드는 이 취약점에 대한 주요 정보를 보여줍니다.

![](../../.gitbook/assets/snykcode\_issue\_card.png)

이 취약점에 대한 자세한 정보를 보려면 **Full details**를 클릭하십시오.

![](../../.gitbook/assets/xss-2.png)

(위의 예제는 서버가 반환하는 응답에 non-sanitized된 HTTP 입력이 유입되어 악성 코드가 실행 중일 수 있음을 보여주고 있습니다.)

코드 링크를 클릭하여 소스코드 파일을 직접 연 다음 변경하여 이 취약점을 수정하십시오.
