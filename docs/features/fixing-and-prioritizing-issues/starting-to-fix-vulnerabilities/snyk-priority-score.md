# Snyk 우선순위 점수

**Snyk 우선순위 점수는 무엇입니까?**

Snyk은 Issue의 우선순위를 가능한 한 빠르고 쉽게 정하기 위해 Priority Score(우선순위 점수)를 생성하여 가장 위험한 Issue가 가장 높은 점수를 받도록 합니다.

Snyk의 보안 그룹은 ~~_추세적인 취약점과 야생에서 찾을 수 있는 공격 또는 개념 증명 사이의 중요한 상관 관계를 발견했습니다._~~ Social trend는 모든 Issue, 취약점 및 라이선스에 대해 계산되고 표시되며 0에서 1,000까지의 범위(0은 낮은 위험으로 간주되고 1,000은 위험으로 간주됨)를 나타냅니다. 이는 사용자에게 고려된 많은 고려사항을 반영하는 높은 수준의 세분성을 제공합니다. 세분성은 동일한 점수로 끝나는 너무 많은 Issue를 방지하므로 사용자는 높은 정확도로 한 눈에 우선순위를 결정할 수 있습니다.

{% hint style="info" %}
Snyk은 우선순위를 결정하기 위해 CVSS 점수만을 사용하지 않습니다. Snyk의 우선순위 점수는 CVSS 점수, 수정 사항의 가용성, 알려진 익스플로잇, 취약점이 얼마나 새로운지, 도달 가능한지 여부를 포함한 여러 요소를 처리하는 종합적인 점수 시스템입니다. 자세한 내용은 [작동 방식](snyk-priority-score.md) 섹션을 참조하십시오.
{% endhint %}

## 작동 원리

각 Issue에 대해 Snyk은 독점 알고리즘에 의해 여러 요소를 처리하고 가중치를 부여하여 해당 Issue에 대한 점수를 산출합니다.

{% hint style="info" %}
Snyk은 새로운 요소를 포함하도록 우선순위 알고리즘을 지속적으로 개선하고, 요소의 가중치를 업데이트하여 최신 정보가 주어진 경우 항상 가장 정확하고 최신의 우선순위 표현을 제공합니다.
{% endhint %}

현재 이러한 요소에는 다음이 포함됩니다.

* [**Severity levels**](https://docs.snyk.io/introducing-snyk/snyks-core-concepts/severity-levels): 해당 Issue에 대한 CVSS 프레임워크 v3.1 점수를 사용하여 계산되었습니다.
* [**Exploit Maturity**](https://snyk.io/blog/whats-so-wild-about-exploits-in-the-wild-and-how-can-we-prioritize-accordingly/): Snyk의 업계 최고의 보안 팀이 수동 및 자동화 방법을 사용하여 어떤 취약점이 악용될 수 있는지, 어느 정도까지 공격 가능한지 결정합니다.
* [**Reachability**](https://snyk.io/blog/optimizing-prioritization-with-deep-application-level-context/): Snyk은 프로젝트 내에서 호출된 코드 경로를 확인하여 코드에서 도달할 수 있는 취약점을 식별합니다.
* [**Fixability**](https://support.snyk.io/hc/en-us/articles/4405034808209) (수정 가능 여부): 업그레이드할 더 안전한 버전이나 사용 가능한 Snyk 패치가 없으면 개발자는 코드를 직접 수정하거나 대체 패키지를 사용해야 합니다. 따라서 수정 사항이 있는 취약점에 더 높은 우선순위가 부여됩니다.
* **Time**: 새로운 취약점은 위험이 증가할 가능성이 높으므로 우선순위 점수를 높입니다.
* [**Social Trends**](https://docs.snyk.io/fixing-and-prioritizing-issues/prioritizing-issues/prioritize-by-social-trends): Snyk은 Twitter의 알려진 취약점에 대한 언급을 모니터링하여 트윗 및 반응의 추세를 계산합니다.
* Malicious Packages: Snyk은 악성 패키지에서 발생하는 취약점의 우선순위 점수를 높입니다.

## Kubernetes에 대한 우선순위 계산

Kubernetes 통합에서 가져온 Kubernetes 구성 이미지에는 우선순위 점수 계산을 위한 여러 요소가 추가로 있습니다. 자세한 내용은 [Snyk 우선순위 점수 및 Kubernetes](https://support.snyk.io/hc/en-us/articles/360010906897-Snyk-Priority-Score-and-Kubernetes) 참조하십시오.

## Snyk Code에 대한 우선순위 계산

Snyk Code의 우선순위 계산에 기여하는 여러 요소들은 다음과 같습니다.

* **Severity levels**(심각도 수준)
* **Number of vulnerability occurrences**(취약점 발생 횟수)
* **Rule tags**: **beta** 태그가 발견되면 감소
* **Open community projects**: 취약점이 널리 퍼진 경우
* **Hot files**: 취약점이 소스 파일 또는 코드 흐름 내에 있는 경우
* **Fixability**: 해당 Issue에 사용할 수 있는 수정 예시가 있는 경우

자세한 내용은 [Snyk Code](https://docs.snyk.io/snyk-code) 설명서를 참조하십시오.

## 프로젝트에서 점수 보기

프로젝트 보기에서 각 Issue에 대한 점수를 볼 수 있으며, 모든 Issue는 이제 우선순위 점수별로 정렬되어 가장 시급한 Issue를 먼저 보여줍니다.

Issue는 왼쪽에서 필터링할 수 있습니다.

![](../../../.gitbook/assets/screen\_shot\_2021-07-14\_at\_1.41.24\_pm.png)

## 보고서에서 점수 보기

보고서의 **Issues** 탭에는 자체 정렬 가능한 열로 Priority Score가 포함됩니다. 기본적으로 표는 가장 시급한 Issue를 먼저 표시하기 위해 이미 점수별로 정렬되어 있습니다.

Issue는 점수로 필터링할 수도 있습니다.

![](../../../.gitbook/assets/screen\_shot\_2021-07-14\_at\_1.43.32\_pm.png)

## Snyk API에서 점수 보기

다양한 Issue 관련 API 호출은 이제 response에 점수를 포함하고 점수를 기준으로 필터링을 지원합니다.

관련 API 호출에 대해 자세히 알아보십시오.

* [https://snyk.docs.apiary.io/#reference/reporting-api/latest-issues/get-list-of-latest-issues](https://snyk.docs.apiary.io/#reference/reporting-api/latest-issues/get-list-of-latest-issues)
* [https://snyk.docs.apiary.io/#reference/reporting-api/get-list-of-issues](https://snyk.docs.apiary.io/#reference/reporting-api/get-list-of-issues)
* [https://snyk.docs.apiary.io/#reference/projects/all-projects/list-all-issues](https://snyk.docs.apiary.io/#reference/projects/all-projects/list-all-issues)

## 설정

우선순위 점수와 관련된 설정이 없습니다. 추가 메타데이터일 뿐이므로 비활성화하거나 숨길 수 없습니다.
