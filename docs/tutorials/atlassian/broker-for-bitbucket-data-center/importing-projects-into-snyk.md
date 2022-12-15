---
description: Bitbucket Data Center에서 프로젝트를 가져오는 방법
---

# 프로젝트를 Snyk으로 가져오기

Bitbucket Data Center에서 프로젝트를 가져오는 방법조직의 snyk.io로 이동하고 **Add project**를 클릭합니다.

![표준 프로젝트 추가 초기 보기](../../../.gitbook/assets/broker-1-add-project.png)

브로커 통합을 활성화하면 프로젝트를 추가하는 새로운 옵션인 **Bitbucket Server**가 표시됩니다.

![Bitbucket Data Center가 활성화된 프로젝트 추가](../../../.gitbook/assets/broker-2-add-project-bbs.png)

프로젝트 가져오기 화면을 보려면 **Bitbucket Server**를 클릭하십시오. Snyk는 귀하가 제공한 로그인에 표시되는 프로젝트에 대해 Bitbucket Data Center 인스턴스를 쿼리하고 선택할 수 있도록 표시합니다. 이 예는 구성원의 저장소 중 하나와 연결된 최종 프로젝트를 보여줍니다.

![Bitbucket 서버 저장소 선택 프로세스](<../../../.gitbook/assets/broker-4-add-repository-bbs (2).png>)

이 튜토리얼에서는 프로젝트 아래에 두 저장소를 모두 가져옵니다. 필요한 경우 더 적거나 추가 파일을 선택할 수 있습니다.

![](../../../.gitbook/assets/broker-5-add-repository-bbs.png)

**Add selected repositories**를 클릭하여 모든 프로젝트를 Snyk.io로 가져오고 스캔 작업을 시작합니다.

이 스캔은 비공개로 호스팅된 저장소를 Snyk으로 가져와 출력이 다른 프라이빗 또는 퍼블릭 저장소에서 가져오기와 동일한 스타일 및 패턴을 따릅니다.

예를 들어, 다음 페이지는 Bitbucket Data Center의 저장소에서 가져온 것이지만 결과는 Bitbucket 서버가 소스로 식별된다는 점만 제외하면 유사한 솔루션과 동일합니다:

![Bitbucket 서버에서 호스팅되는 저장소의 프로젝트 요약 보기](<../../../.gitbook/assets/image (83) (1).png>)

{% hint style="info" %}
Snyk 및 다양한 데모 환경에 익숙한 사용자의 경우 위의 예에서 인기 있는 **goof** 애플리케이션을 인식해야 합니다.
{% endhint %}
