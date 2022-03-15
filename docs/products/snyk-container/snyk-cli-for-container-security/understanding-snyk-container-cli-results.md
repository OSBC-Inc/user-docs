# Snyk Container CLI 결과 이해

## 취약점 정보

Snyk Container가 취약점을 탐지하면 다음과 같이 출력됩니다.

![Snyk Container로 탐지된 취약점](../../../.gitbook/assets/clivulnerabiilities.png)

각 취약점은 다음 정보와 함께 표시됩니다.

| **Field**              | **Description**                                                                   |
| ---------------------- | --------------------------------------------------------------------------------- |
| **Severity**           | 특정 취약점의 중요도입니다. 자세한 내용은 Snyk Container 심각도를 참조하십시오.                               |
| **A clear heading**    | 취약점 및 영향을 받는 패키지에 대한 요약입니다.                                                       |
| **Description**        | CVE가 있는 경우 issue 유형 또는 CVE(Common Vulnerabilities and Exposure) 참조에 대한 간단한 설명입니다. |
| **Info**               | 업스트림 소스 및 글로벌 취약점 데이터베이스에 대한 링크를 포함하여 취약점에 대한 자세한 정보의 링크입니다.                      |
| **Introduced through** | 취약점의 영향을 받는 최상위 패키지 이름입니다.                                                        |
| **From**               | 영향을 받는 패키지가 이미지에 표시되는 방식입니다.                                                      |
| **Introduced by**      | 취약점이 기본 이미지에 있는지 또는 Dockerfile의 어느 행에서 이 취약점이 발생했는지 여부입니다.                        |
| **Fixed in**           | 취약점에 대한 수정 사항이 있는 패키지 버전입니다.                                                      |

취약점은 가장 중요한 문제를 확인하기 위한 스크롤을 최소화하기 위해 심각도 역순으로 나타납니다.

또한 Snyk은 알려진 취약점에 대해 테스트된 총 디펜던시 및 취약점 수를 보고합니다.

![테스트된 총 디펜던시 및 발견된 issues](../../../.gitbook/assets/clisummary.png)

{% hint style="info" %}
**참고**\
Snyk은 서로 다른 여러 패키지에서 발견된 동일한 취약점을 함께 그룹화합니다. 이렇게 하면 인스턴스뿐만 아니라 취약점 수에도 집중할 수 있습니다.
{% endhint %}

## 기본 이미지 권장 사항

Snyk이 사용된 기본 이미지를 확인하고 [Official Docker image](https://docs.docker.com/docker-hub/official\_images/)를 사용하는 경우 출력에는 발견된 일부 취약점을 해결하기 위한 업그레이드 권장 사항이 포함됩니다.

![기본 이미지 업그레이드 권장 사항](../../../.gitbook/assets/clirecommendations.png)

이는 상황 인식 수준을 제공하여 minor 및 major 업그레이드 또는 취약점이 더 적을 수 있는 대체 기본 이미지의 취약점 수를 제공합니다.
