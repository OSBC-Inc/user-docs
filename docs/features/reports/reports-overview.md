# Reports 개요

{% hint style="info" %}
**기능 지원 여부**\
이 기능은 Enterprise 및 Business 요금제에서 사용할 수 있습니다. 자세한 내용은 [pricing plans](https://snyk.io/plans/) 참조하십시오.
{% endhint %}

**Reports** 영역에는 projects, issues, dependencies 및 licenses에 대한 과거 및 집계 데이터가 표시되며 모든 프로젝트에 대한 데이터 및 분석이 제공됩니다. 네 개의 각 탭(아래 참조)의 데이터는 작업 중인 조직을 기준으로 표시되며, 보고 있는 탭에 다른 파라미터로 이 데이터를 필터링할 수 있습니다.

또한 계정을 그룹으로 관리하는 경우 **Group** 수준에서 **Reports**로 이동할 때 모든 조직에 대해 집계된 데이터가 표시됩니다.

**Group** 수준에서 여러 조직에 대한 데이터를 필터링하여 다음과 같이 볼 수 있습니다.

![](../../.gitbook/assets/mceclip0-28-.png)

또한 **Organization Filters**를 사용하여 선택한 조직 그룹에 대해 미리 필터링된 Report를 생성하고 저장할 수도 있습니다. 자세한 내용은 [Snyk 그룹 개요](../user-and-group-management/managing-groups-and-organizations/snyk-groups-overview.md)를 참조하십시오.

또한 Organization 수준에서 필터링할 [일반 작업](general-actions.md)을 참조하십시오.

* 프로젝트 이름
* 프로젝트 유형
* 취약점 심각도
* 특정 기간

Reports 영역은 다음 탭으로 구성됩니다.

* [Summary](summary-tab.md)—기본 대시보드는 모든 프로젝트에 걸쳐 모든 Issue(취약점 및 라이선스)를 한눈에 볼 수 있도록 표시합니다.
* [Issues](issues-tab.md)—심각도, 사용 가능한 수정 사항 등을 포함하여 모든 프로젝트의 모든 Issue(취약점 및 라이선스)를 해결할 수 있습니다.
* [Dependencies](dependencies-tab.md)—프로젝트 및 해당 상태의 패키지 디펜던시를 확인할 수 있습니다.
* [Licenses](licenses-tab.md)—모든 프로젝트 및 해당 상태의 라이선스를 확인할 수 있습니다.

Report 데이터는 API를 사용하여 생성 및 검색할 수도 있습니다. 자세한 내용은 [API 설명서](https://snyk.docs.apiary.io/#introduction)를 참조하십시오.

{% hint style="warning" %}
프로젝트가 테스트되고 해당 데이터가 Reports 영역에 나타날 때까지 지연이 있을 수 있습니다. 9시간 이상 지연되는 경우 [Support 팀에 문의하십시오.](https://support.snyk.io/hc/en-us/requests/new)
{% endhint %}

{% hint style="danger" %}
읽기 전용 프로젝트와 해당 결과는 Reports 영역에 나타나지 않습니다.
{% endhint %}
