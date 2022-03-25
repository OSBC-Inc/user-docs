# 심각도 수준

취약점에 심각도 수준이 적용되어 애플리케이션의 해당 취약점에 대한 위험을 나타냅니다. 심각도 수준은 [취약점 평가](https://snyk.io/learn/vulnerability-assessment/)의 핵심 요소이며 각 수준은 다음과 같습니다.

* **Low:** 애플리케이션이 공격하기위해 다음 취약점과 함께 사용할 수 있는 취약점 매핑을 허용하는 일부 데이터를 노출할 수 있습니다.
* **Medium:** 일부 조건에서 공격자가 애플리케이션의 민감한 데이터에 액세스하도록 허용할 수 있습니다.
* **High:** 공격자가 애플리케이션의 민감한 데이터에 액세스하도록 허용할 수 있습니다.
* **Critical:** 공격자가 민감한 데이터에 액세스하고 애플리케이션에서 코드를 실행할 수 있습니다.

{% hint style="info" %}
심각도 수준은 라이선스 문제에도 적용됩니다. [라이선스 개요](https://docs.snyk.io/snyk-open-source/licenses)를 참조하십시오.
{% endhint %}

### 심각도 수준 결정

**CVSS**(**Common Vulnerability Scoring System**)는 취약점의 심각도 수준을 나타냅니다.

Snyk에서는 [CVSS framework version 3.1](https://www.first.org/cvss/v3-1/)을 사용하여 취약점의 특성과 심각도를 제공합니다.

| **심각도 수준** | **CVSS 점수** |
| ---------- | ----------- |
| Low        | 0.0 - 3.9   |
| Medium     | 4.0 - 6.9   |
| High       | 7.0 - 8.9   |
| Critical   | 9.0 - 10.10 |

자세한 내용은 [Scoring security vulnerabilities 101: Introducing CVSS for CVEs](https://snyk.io/blog/scoring-security-vulnerabilities-101-introducing-cvss-for-cve/)를 참조하십시오.

### 심각도 및 우선순위 채점

심각도 수준은 [Snyk Exploit Maturity](https://snyk.io/blog/whats-so-wild-about-exploits-in-the-wild-and-how-can-we-prioritize-accordingly/) 및 [Reachable Vulnerabilities](https://snyk.io/blog/optimizing-prioritization-with-deep-application-level-context/) 정보와 함께 각 취약점에 대한 Snyk의 우선순위 점수에 적용되는 한 요인입니다. 이 점수는 개발자가 먼저 해결해야 할 취약점을 결정하는데 도움이 됩니다.

Snyk의 우선순위 점수에서 심각도 수준이 사용되는 방식에 대한 자세한 내용은 [Snyk 우선순위 점수](../../features/fixing-and-prioritizing-issues/starting-to-fix-vulnerabilities/snyk-priority-score.md)를 참조하십시오.

## Snyk에서 심각도 수준 확인

심각도 수준을 항상 표시하기 위해 Snyk 전체에 심각도 수준이 표시됩니다.

대시보드에서 다음과 같이 확인할 수 있습니다.

![](<../../.gitbook/assets/image (46).png>)

프로젝트에서 다음과 같이 확인할 수 있습니다.

![](<../../.gitbook/assets/image (43).png>)

프로젝트의 각 취약점 정보를 확인할 수 있습니다.

![](<../../.gitbook/assets/image (39).png>)

Snyk 사용에 대한 자세한 내용은 [시작하기](https://docs.snyk.io/getting-started)를 참조하십시오.
