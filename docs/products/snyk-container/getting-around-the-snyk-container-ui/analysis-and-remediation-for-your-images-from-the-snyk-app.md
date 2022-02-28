# Snyk 앱에서 이미지 분석 및 수정

CLI에서 snyk monitor를 사용하여 컨테이너 프로젝트를 Snyk으로 가져올 수 있습니다. 또는 UI에서 지원되는 컨테이너 레지스트리에서 직접 프로젝트를 가져올 수 있습니다.

그런 다음 프로젝트를 스캔하고 취약점을 테스트한 다음 프로젝트의 스냅샷을 가져옵니다. Snyk은 설정(매일 또는 매주)을 기준으로 정기적으로 이미지 스냅샷 디펜던시(태그 참조)를 스캔하고 새로운 취약점이 확인되면 업데이트합니다.(사용자의 설정을 기준으로 이메일 또는 Slack) 이미지의 태그가 변경되고 원래 태그가 다른 이미지에 사용되는 경우 Snyk은 원래 태그와 연결된 이미지를 계속 스캔합니다. 즉, 반복 테스트에서 새 이미지를 스캔합니다. 다른 태그를 사용하여 이미지 테스트를 계속하려면 관련 태그를 가져오십시오.

**Projects** 페이지에서 프로젝트를 레지스트리 통합에서 가져온 경우 관련 레지스트리 아이콘으로 표시되고 CLI에서 가져오면 마찬가지로 CLI 아이콘으로 표시됩니다.

다음 예와 유사하게 모든 컨테이너 프로젝트를 필터링할 수 있습니다.

![](<../../../.gitbook/assets/image (10).png>)

컨테이너 프로젝트를 열면 분석 결과 및 수정 조언이 Snyk UI에 나타납니다.

![](../../../.gitbook/assets/uuid-069520cd-66e8-9f80-5bcf-c7845009ff54-en.png)

다음과 같은 정보가 표시됩니다.

* 프로젝트 요약에는 다음과 같은 고유한 세부 정보를 포함한 일반 프로젝트 세부 정보가 표시됩니다.
  * 이미지 ID
  * 이미지 태그
  * 기본 이미지
  * 알려진 취약점이 있는 총 종속성 및 총 취약점&#x20;
* 수정 조언 – 모니터링에 Docker 파일을 포함시킨 경우 실행 가능한 모든 수정 조언이 표시됩니다. 모든 조언을 보려면 **Show more upgrade types** 링크를 클릭합니다. 제공되는 조언은 사용 가능한 수정 사항에 따라 다르며 다음 이미지와 유사하게 나타납니다.

![](../../../.gitbook/assets/uuid-431ce2b1-e5f0-0025-7932-0171b35cb9bb-en.png)

* Upgrade suggestions can include:
  * Minor upgrades—the safest and best minor upgrade available
  * Major upgrades—an option for a major upgrade which will reduce more vulnerabilities but with greater risk
  * Alternative upgrades—viable alternative image options for replacing your current base image with other, different base images that provide the least amount of vulnerabilities possible.
  * If your base image is outdated, Snyk also recommends rebuilding your image.
* Upgrade recommendations include these details:
  * the name of the recommended base image version
  * the number of vulnerabilities existent in the recommended upgrade
  * a summary of the vulnerability severities accordingly.
* Filters—in addition to the other filters available for all supported project types, when you view a container project, you can also filter by:
  * a specific binary or by OS packages (for binaries/packages containing issues)
  * Dockerfile instructions - if you attach your Dockerfile, then you can filter to view issues associated only with the base image, or to view Dockerfile-related advice (user instruction), or both

{% hint style="info" %}
**Note**\
If there is only one category of issues in your container, such as Node binary vulnerabilities only or OS packages only, this filter does not appear.\
If there is no Dockerfile attached for additional advice, the Dockerfile instruction filter does not appear
{% endhint %}

* Issues tab—List of vulnerabilities, including origins, paths, and an overview of the vulnerability
* Dependencies tab—a tree view of package hierarchy inside the image
