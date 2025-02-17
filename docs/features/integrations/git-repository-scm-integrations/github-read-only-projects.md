# GitHub 읽기 전용 프로젝트

Snyk는 자신의 Snyk 계정을 통해 권한을 부여하지 않고 공개 GitHub 저장소를 모니터링하는 기능을 제공합니다.

## 작동 방식:

이를 통해 종속성으로 사용하려는 프로젝트의 취약점을 추적하거나, 비즈니스 내에서 독립 실행형 독립 도구로 사용하거나, Snyk의 도구를 사용하여 문제를 적극적으로 예방하거나 수정할 필요가 없는 기타 공개 저장소를 추적할 수 있습니다. .

저장소는 Snyk의 자체 GitHub 자격 증명을 사용하여 매일 자동으로 테스트되며 테스트는 테스트 제한에 포함되지 않습니다.

이러한 방식으로 가져온 공개 프로젝트는 "귀하의" 것으로 간주되지 않으므로 [Snyk's Reports section](https://app.snyk.io/reports)에 나타나지 않습니다.

Snyk GitHub 통합을 통해 가져온 프로젝트와 달리 이러한 방식으로 가져오기/모니터링되는 프로젝트는 다음 항목에 적합하지 않습니다:

* pull request이 merge될 때 자동 재테스트
* 제기된 모든 PR에 대한 테스트를 커밋하여 새로운 취약점이 도입되는 것을 감지(및 선택적으로 차단)
* 취약점 수정을 위한 최소한의 변경을 권장하는 자동화된 수정 PR - 자세히 알아보기
* 종속성을 최신 상태로 유지하고 새로운 취약점을 방지하고 발견된 취약점을 간단하게 수정하는 데 도움이 되는 자동화된 종속성 업그레이드 PR.
* 사용자가 선택한 특정 문제를 해결하기 위해 Snyk을 통해 생성된 수동 수정 PR

프로젝트는 [Snyk에 온보딩 중](github-read-only-projects.md#snyk)이거나 [온보딩 후](github-read-only-projects.md#undefined-1)(일반적으로 계속 사용하는 동안) 이러한 방식으로 가져올 수 있습니다.

## Snyk에 온보딩하는 동안:

온보딩 중에 프로젝트를 가져올 소스로 GitHub를 선택하면 전체 GitHub 통합을 설정하거나(사용 가능한 취약점 방지 및 수정 기능 활용) 하단의 링크를 통해 Snyk 권한을 부여하지 않고 계속 진행할 수 있습니다.

![](../../../.gitbook/assets/screenshot\_2020-07-03\_at\_08.02.29.png)

모니터링할 저장소를 "owner/repository" 형식으로 입력합니다:

![](../../../.gitbook/assets/screenshot\_2020-07-03\_at\_08.01.41.png)

유효한 저장소 이름을 입력한 후 "+ Add repo"를 클릭하면 저장소가 지원되는 매니페스트 파일에 대해 빠르게 테스트됩니다.

필요한 만큼 저장소를 입력하고 "Import X repository/ies"를 클릭합니다.

![](../../../.gitbook/assets/screenshot\_2020-07-03\_at\_08.01.52.png)

## 온보딩 후

읽기 전용 프로젝트는 GitHub 권한에 의존하지 않으므로 전체 GitHub 통합이 설정되었는지 여부에 관계없이 가져올 수 있습니다.

이는 대시보드의 "프로젝트 추가" 드롭다운을 통해 또는 [https://app.snyk.io/add/github-readonly](https://app.snyk.io/add/github-readonly)로 이동하여 수행할 수 있습니다.

![](../../../.gitbook/assets/screen\_shot\_2020-06-09\_at\_14.27.40.png)

모니터링할 저장소를 "owner/repository" 형식으로 입력합니다:

![](../../../.gitbook/assets/screenshot\_2020-07-03\_at\_08.01.41.png)

유효한 저장소 이름을 입력한 후 "+ Add repo"를 클릭하면 저장소가 지원되는 매니페스트 파일에 대해 빠르게 테스트됩니다.

필요한 만큼 저장소를 입력하고 "Import X repository/ies"를 클릭합니다.

![](../../../.gitbook/assets/screenshot\_2020-07-03\_at\_08.01.52.png)
