# Reachable vulnerabilities

## 소개

앱에서 오픈 소스 취약점을 검사하는 첫 번째 단계는 앱에서 사용하는 패키지를 식별하는 것입니다.

다음 단계는 취약점이 앱의 코드에 영향을 미치는지 여부와 상관없이 식별된 패키지 중 어떤 패키지에 취약점이 있는지 확인하는 것입니다. 이는 조직 수준에서 볼 때 수천 개의 취약점으로 쉽게 이어질 수 있으므로 어디서부터 시작해야 하는지 식별해야 합니다.

패키지의 취약한 부분을 사용하지 않을 수 있으므로 많은 취약점이 코드에 영향을 미치지 않을 수 있습니다:

* **도달 가능**한 취약점에는 코드에서 취약한 기능까지의 경로가 있습니다.
* 연결할 수 없는 취약점에는 이 경로가 없습니다.

앱이 오픈 소스 종속성을 사용하는 방법과 오픈 소스 종속성이 서로 상호 작용하는 방식을 더 자세히 살펴봄으로써 발견된 취약점에 필요한 컨텍스트를 추가할 수 있습니다. 이 접근성은 수정할 취약점의 우선 순위를 결정하는 데 도움이 됩니다.

### 작동 방식

가능한 한 정확한 결과를 제공하기 위해 여러 알고리즘을 사용하여 앱에서 사용하는 오픈 소스 종속성에 대한 호출 그래프를 작성합니다. 호출 그래프가 있으면 앱의 코드에서 취약한 기능이나 패키지로 이어지는 경로가 있는 취약점을 식별할 수 있습니다.

우리는 결과를 다음 영역으로 나눕니다:

1. **Reachable** - 코드에서 취약한 기능으로 가는 명확한 경로가 발견되었습니다. 이러한 취약점을 먼저 수정하는 것이 좋습니다.
2. **Potentially reachable** - 취약점에 접근할 수 있다는 표시가 발견되었습니다. 추가 검토가 권장됩니다.
3. **No path found** - 취약한 기능에 대한 코드의 직접 호출을 찾을 수 없습니다.

### 지원되는 언어 및 전제 조건

Snyk CLI를 사용하여 Java(Maven 및 Gradle) 앱에 대해 **Reachable vulnerabilities analysis**를 사용할 수 있습니다. 또한 Snyk UI를 사용하여 Java Maven GitHub 프로젝트가 지원됩니다.

#### Java 지원

* Java 8 to 13.
* Maven 3.6.\*
* Gradle (아래 매트릭스 참조)

![](../../../.gitbook/assets/image1-1-.png)

### 사용 방법

도달 가능한 취약점 분석을 수행하려면 다음을 수행할 수 있습니다:

* Git 통합을 사용하여 Git에서 Snyk으로 가져온 저장소의 연결 가능성 문제에 대해 앱을 테스트합니다. 연결 가능성은 Snyk에서 수행하는 검사의 일부로 수행됩니다(현재 GitHub 지원). \
  _**NOTE**_: 이 방법을 사용하면 저장소를 Snyk에 복제하여 분석을 실행합니다. 저장소는 분석이 완료된 후 서버에서 삭제됩니다.
* Snyk CLI를 사용하여 연결 가능성 문제에 대해 코드를 분석합니다. Snyk CLI를 사용하여 실행하려면 앱이 이미 빌드(컴파일)되어 있어야 하고 앱의 바이트 코드를 사용할 수 있어야 합니다.

### Snyk CLI를 사용하여 **Reachable vulnerabilities** 검색

1. 최신 버전의 [CLI](https://www.npmjs.com/package/snyk)를 사용하고 있는지 확인하십시오.
2. 관련 매니페스트 파일이 있는 앱의 폴더로 이동합니다(또는 `--file` 매개변수를 사용하여 올바른 경로를 가리킴).
3. `snyk test --reachable` 실행

{% hint style="info" %}
**NOTE: **_****_ `--reachable` 매개변수는 `--all-projects` 또는 `--all-sub-projects`와 동시에 사용할 수 없습니다.
{% endhint %}

### Git 통합을 사용하여 **Reachable vulnerabilities** 검색

{% hint style="info" %}
이 기능을 제공하기 위해 Snyk는 Git 저장소 콘텐츠의 임시 복사본을 가져옵니다. 자세한 내용은 [how-snyk-handles-your-data.md](../../../more-info/how-snyk-handles-your-data.md "mention")을 참조하십시오.
{% endhint %}

1. [GitHub 통합](../../integrations/git-repository-scm-integrations/github-integration.md)을 설정합니다.
2. &#x20;설정.
   * **Organization** 설정에서 **Languages** 섹션으로 이동합니다.
   * **Reachable vulnerabilities analysis** 섹션으로 이동합니다.
   * **Reachable vulnerabilities analysis**을 선택하고 변경 사항을 저장하십시오.
3. **import projects** 페이지로 이동하여 Snyk으로 가져올 저장를 선택합니다.
4. 선택한 프로젝트를 가져와서 **Reachable vulnerabilities** Issue에 대해 분석합니다.

### 결과 보기

### CLI

`snyk test --reachable`을 실행할 때 CLI 출력에는 다음이 포함됩니다.

1. 테스트된 종속성 수, 발견된 취약점 수 및 Reachable vulnerabilities 수.
2. 해당 취약점 옆에 reachability 수준이 표시되고, 앱 코드에서 취약한 기능까지의 경로가 아래에 나타납니다.

### 프로젝트 페이지

CLI에서 `snyk monitor`를 실행하거나 Snyk UI를 통해 프로젝트를 가져온 후 Snyk에서 프로젝트를 모니터링하고 Reachable Vulnerabilities analysis 결과가 프로젝트 페이지의 다음 위치에 나타납니다.

1. **Filters** - 도달 가능성을 기반으로 결과를 필터링하여 먼저 eachable vulnerabilities에 집중할 수 있습니다..
2. **Reachability badge** - 취약성의 reachability 수준을 빠르게 이해할 수 있습니다.
3. **Call path** - 결과를 검증하기 위해 코드에서 취약한 기능까지의 경로를 볼 수 있습니다.

![](../../../.gitbook/assets/project.png)

### 보고서

연결 가능성 정보는 보고서 **Issues** 탭(그룹 해제 보기)에서 각 **Issue** 옆에 검토할 수 있습니다.

reachability 상태로 필터링하여 reachable Issue를 빠르게 표시할 수 있습니다.

![](../../../.gitbook/assets/blobid0.png)
