# Summary 탭

**Reports** 영역의 기본 대시보드는 모든 프로젝트에서 발견된 모든 Issue(취약점 및 라이선스)를 한눈에 볼 수 있도록 표시하여 다음과 같은 특정 영역에 대한 데이터를 제공합니다.

* Security Issues
* License Issues
* 전체 프로젝트 활동 – 모든 프로젝트, 테스트 및 Issues 요약

{% hint style="info" %}
**Note**\
네 개의 탭 각각에 있는 데이터는 보고 있는 그룹이나 조직뿐만 아니라 Reports 영역 상단에서 적용한 필터를 기반으로 표시됩니다.
{% endhint %}

대시보드는 다음 이미지와 유사하게 나타납니다.

![](../../.gitbook/assets/mceclip0-30-.png)

특정 기간의 추가 데이터를 빠르게 보려면 관련 그래프 위에 마우스를 올려놓고 팝업을 확인하십시오.

## **Summary** 탭 요소

다음 표에서는 **Summary** 영역의 여러 부분을 설명합니다.

| **Element**         | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Security Issues     | <p>심각도별로 분류된 Security Issue의 합계입니다. Security Issue는 프로젝트를 스캔할 때 발견되는 취약점입니다.</p><p>Security issue summary 영역의 모든 통계는 연결되어 있습니다. 숫자를 클릭하면 선택한 심각도에 대한 취약점으로만 필터링된 <strong>Reports</strong> 영역의 <strong>Isseus</strong> 탭으로 이동할 수 있습니다.</p><p>예를 들어 <strong>Security</strong> Issues에서 300 high 심각도 상자를 클릭하면 해당 300 high 심각도의 취약점으로만 필터링된 <strong>Issues</strong> 탭으로 이동합니다.</p><p>Values:</p><ul><li>Critical 심각도</li><li>High 심각도</li><li>Medium 심각도</li><li>Low 심각도</li></ul> |
| License **** Issues | <p>심각도별로 분류된 License issues의 합계입니다.</p><p><strong>License issue summary</strong> 영역의 모든 통계는 연결되어 있습니다. 숫자를 클릭하면 특정 라이선스 issues 그룹으로 필터링된 <strong>Reports</strong> 영역의 <strong>Issues</strong> 탭으로 이동합니다.</p><p>예를 들어 <strong>License</strong> Isseus에서 28 medium 심각도 상자를 클릭하면 <strong>Issues</strong> 탭으로 이동하고 해당 28 medium 심각도 license Issues로만 필터링 됩니다.</p><p>Values:</p><ul><li>High severity</li><li>Medium severity</li><li>Low severity</li></ul>                        |
| Issues over time    | Issues 그래프에는 확인된 Issues의 수(critical, high, medium, low)를 표시합니다.                                                                                                                                                                                                                                                                                                                                                                                                                |
| Exposure window     | Isses가 식별된 후 해결될 때까지 경과된 시간입니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                |

**Activity** 영역의 경우 다음과 같습니다.

| **Value**               | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Tests run               | 테스트 실행 횟수                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| Projects                | 프로젝트 수                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| New issues              | 해당 기간에 Issue가 발생한 횟수(재도입된 Issue 및 삭제된 프로젝트 포함)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| Fixed issues            | Number of fixes applied in the time period (in해당 기간에 적용된 수정 사항 수(재도입된 Issue 및 삭제된 프로젝트 포함)                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| Tests preventing issues | 실행되었으며 새로운 취약점이 도입되는 것을 방지한 Snyk 테스트 수                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| Ignored issues          | <p>발견되었지만 무시된 총 Issue 수와 사용 가능한 수정 사항이 있는 무시된 총 Issue 수입니다. 이러한 Issue는 이 <strong>Summary</strong> 영역의 다른 총계에서 계산되지 않습니다.</p><p>이러한 값은 <strong>Reports</strong> 영역의 <strong>Issues</strong> 탭에 연결되어 무시된 특정 Issue의 특정 그룹으로 필터링됩니다.</p><p><strong>Ignored</strong> 처리된 Issue 상자에서 숫자를 클릭하여 무시된 Issue만 필터링된 <strong>Issues</strong> 탭으로 이동합니다. 같은 상자에서 수정 가능한 번호를 클릭하면 <strong>Issues</strong> 탭으로 이동하여 수정 가능하지만 무시되는 Issue만 필터링됩니다.</p><p><strong>Note:</strong></p><p>Issue를 무시하면 Reports의 Summary 탭에 있는 데이터와 동기화되기까지 최대 1시간이 걸릴 수 있습니다.</p> |

## **Summary tab** 작업

다음 드롭다운이 창 상단에 나타납니다.

![](../../.gitbook/assets/mceclip1-19-.png)

**Summary filters**—관련 Issue 유형을 선택하여 표시할 Issue를 표시한 다음 화살표를 다시 클릭하여 닫습니다.
