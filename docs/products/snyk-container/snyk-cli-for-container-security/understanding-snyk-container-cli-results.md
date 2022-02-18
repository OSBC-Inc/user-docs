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

Vulnerabilities appear in reverse severity order to limit scrolling to see the most important issues.

Snyk also reports the total dependencies tested for known vulnerabilities and the total number of vulnerabilities.

![Total dependencies tested and issues fount](../../../.gitbook/assets/clisummary.png)

{% hint style="info" %}
Note\
Snyk groups the same vulnerability discovered in multiple different packages together. This helps you focus on the number of vulnerabilities, not just the instances.
{% endhint %}

## 기본 이미지 권장 사항

If Snyk determines the base image used, and the image uses an [Official Docker image](https://docs.docker.com/docker-hub/official\_images/), the output includes recommendations for upgrades to resolve some of the discovered vulnerabilities.

![Recommendations for base image upgrade](../../../.gitbook/assets/clirecommendations.png)

This provides a level of situational awareness, showing the vulnerability counts in minor and major upgrades or in alternative base images which might have fewer vulnerabilities.
