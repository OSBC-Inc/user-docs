# 취약점 수정

Snyk은 직접 의존성을 취약점이 없는 버전으로 업그레이드하거나 취약점을 패치하여 취약점을 수정하는 데 도움을 줍니다.

Snyk으로 취약점을 수정하는 방법은 다음과 같습니다.

* 관련 프로젝트 페이지의 특정 [Issue 카드](../../../getting-started/introduction-to-snyk-projects/issue-card-information.md)에서 Fix this vulnerability를 클릭합니다.
* [소스코드 통합을 사용](../../integrations/git-repository-scm-integrations/)하는 경우
  * 프로젝트 페이지에서 **Open a fix PR**을 클릭하십시오.
  * 취약점을 수정하는 데 도움이 되는 새로운 수정 사항이 있으면 [자동 pull requests](../../../products/snyk-open-source/open-source-basics/fix-pull-requests-for-new-vulnerabilities.md)를 사용하십시오.

### 작동 방식

새로운 수정 가능한 취약점이 발견되면 Snyk은 사용자 대신(자동 수정 PR을 지원하는 저장소에서) 새 PR을 생성하려고 시도하거나 설정에 따라 수동으로 생성할 것을 권장합니다.

Snyk이 수정을 자동화할 때, 정확한 수정에 대한 기존 브랜치 및 pull request가 있는지 확인합니다. 이미 존재하는 경우, 이미 닫힌 기존 pull request를 다시 open합니다.

Issue에 대한 기존 브랜치 및 pull request가 없는 경우 새 브랜치 및 pull request가 생성됩니다.

### 수정 조언

Snyk이 수정을 자동화할 때, 정확한 수정에 대한 기존 브랜치 및 pull request가 있는지 확인합니다. 이미 존재하는 경우, 이미 닫힌 기존 pull request를 다시 open합니다.

Snyk은 다음 솔루션 중 하나를 제공합니다.

* **upgrade** - 원래 패키지로 업그레이드
* **Pinning** a package - 패키지를 최상위 디펜던시로 설치합니다. 즉, 간접 의존성의 특정 버전입니다. 이렇게 하면 취약한 버전을 끌어오는 직접 의존성을 피할 수 있습니다.
* a Snyk precision **patch** - 패키지의 취약점을 수정하기 위한 업그레이드가 현재 제공되지 않는 경우 Snyk은 Issue를 수정하기 위한 패치를 제공합니다.

Summary 영역은 패키지별로 조언을 그룹화하며 사용 가능한 최상의 수정 사항을 기준으로 표시됩니다. 이러한 Summary 목록의 조언에는 패키지별로 다음과 같은 상세 내역이 포함됩니다.

* 해당 패키지에 영향을 미치는 모든 취약점 이름 및 심각도 세부 정보
* 권장 수정 – 이 패키지에 대한 권장 수정 링크 및 나열된 취약점(업그레이드할 특정 버전 또는 패치 이름)

### 앱에서 실행 가능한 조언

Snyk 앱에서 프로젝트 세부 정보의 수정 조언 영역에 있는 각 탭(업그레이드 및 패치)에 대해 다음과 같은 결과가 표시됩니다.

* 수정할 수 있는 총 패키지 수가 탭 제목에 표시됩니다.
* 권장되는 업그레이드 또는 수정 사항에 따라 자격이 부여된 패키지별 취약점 그룹
* 패키지에 영향을 미치는 전체 취약점 목록을 보기 위해 패키지를 확장할 수 있습니다.
* 디펜던시에서 발견된 모든 취약점은 Issue의 우선순위를 지정하고 필요한 경우 수정을 시작하는 데 도움이 되는 컨텍스트 정보와 함께 아래에 추가로 표시됩니다.

Fix Advice 영역은 다음 예와 유사하게 상단 근처의 프로젝트 세부 정보 페이지에 나타납니다.

![Upgrade issues 탭](<../../../.gitbook/assets/Screenshot 2021-10-12 at 14.08.13.png>)

![Patchable issues 탭](<../../../.gitbook/assets/Screenshot 2021-10-12 at 14.10.00.png>)

프로젝트 세부 정보 페이지에서도 추가 조언과 세부 정보를 찾을 수 있습니다.

* **Issues** 탭에서 취약점별 전체 설명
* from the **Dependencies** tab, the entire tree of your project dependencies, enabling you to clearly visualize affected paths

### CLI 도구의 실행 가능한 조언

From the CLI, for each list (upgrade and patch), results are displayed in groups based on the packages we recommend that you fix, and including:

* details for all vulnerabilities introduced per package; to view all dependency paths affected, use `--show-vulnerable-paths=all` when running `snyk test` or `snyk monitor`
* links to full descriptions of each vulnerability

Upgrade and patch results appear similar to the following:

![](<../../../.gitbook/assets/image (17) (1).png>)

![](<../../../.gitbook/assets/image (49).png>)

Patch recommendations with some and with all paths:

![](../../../.gitbook/assets/uuid-1afca091-a9a5-d42c-40b6-f48aa0e72584-en.png)

![](<../../../.gitbook/assets/image (3) (1).png>)
