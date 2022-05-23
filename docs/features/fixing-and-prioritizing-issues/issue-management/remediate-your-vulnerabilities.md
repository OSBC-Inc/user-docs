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
* **Pinning** a package - installing a package as a top-level dependency; that is, a specific version of an indirect dependency. This avoids a direct dependency pulling in a vulnerable version
* a Snyk precision **patch** - if an upgrade to fix any of the vulnerabilities in the package is not currently available, Snyk offers patches to fix the issues

The summary area groups advice per package, and is displayed based on the best available fix. Advice in these summary lists includes these details per package:

* All vulnerability names and severity details affecting that package
* The recommended fix - a link to the recommended fix for this package and its listed vulnerabilities: either the specific version to which to upgrade or the name of the patch

### 앱에서 실행 가능한 조언

From our app, for each tab (upgrade and patch) in the fix advice area of your project details, results are displayed as follows:

* the total number of packages that can be fixed is displayed on the tab title
* in groups of vulnerabilities by package, entitled by the upgrade or fix that’s recommended
* packages can be expanded in order to view the full list of vulnerabilities affecting the package
* All the vulnerabilities found in your dependencies are displayed further below, together with contextual information that can help you prioritize the issues and start fixing them if required.

The Fix Advice area appears in the project details page near the top, similar to the following examples:

![Upgrade issues tabs](<../../../.gitbook/assets/Screenshot 2021-10-12 at 14.08.13.png>)

![Patchable issues tabs](<../../../.gitbook/assets/Screenshot 2021-10-12 at 14.10.00.png>)

You can also find additional advice and details further down on the Project details page:

* from the **Issues**, tab, a full description per vulnerability
* from the **Dependencies** tab, the entire tree of your project dependencies, enabling you to clearly visualize affected paths

### CLI 도구의 실행 가능한 조언

From the CLI, for each list (upgrade and patch), results are displayed in groups based on the packages we recommend that you fix, and including:

* details for all vulnerabilities introduced per package; to view all dependency paths affected, use `--show-vulnerable-paths=all` when running `snyk test` or `snyk monitor`
* links to full descriptions of each vulnerability

Upgrade and patch results appear similar to the following:

![](<../../../.gitbook/assets/image (17).png>)

![](<../../../.gitbook/assets/image (49).png>)

Patch recommendations with some and with all paths:

![](../../../.gitbook/assets/uuid-1afca091-a9a5-d42c-40b6-f48aa0e72584-en.png)

![](<../../../.gitbook/assets/image (3).png>)
