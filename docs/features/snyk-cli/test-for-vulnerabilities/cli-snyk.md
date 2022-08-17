# CLI에서 Snyk 오픈 소스 사용

프로젝트에서 알려진 취약성을 테스트하려면:

* 프로젝트가 들어 있는 폴더로 이동합니다`(cd ~/projects/myproj/)`.
* `$ snyk test`를 실행합니.

`snyk test` 명령은 모든 로컬 종속성을 식별하고 알려진 취약성에 대해 Snyk 서비스를 쿼리합니다. `synk test`는 발견된 문제를 추가 정보와 함께 표시합니다.

{% hint style="info" %}
Node.js, Ruby 및 Java 프로젝트의 경우 `synk test`에서 수정할 단계도 제안합니다.
{% endhint %}

### 작동 방식

Snyk Open Source는 매니페스트 파일을 검색합니다. 스캔을 기반으로, Snyk 매니페스트 파일에 표현된 구조의 계층 트리를 만듭니다. 즉, 직접 및 간접(과도적) 종속성 및 다른 패키지가 도입된 지점입니다.

이 트리를 만든 후 Snyk은 취약성 데이터베이스를 사용하여 종속성 트리의 모든 패키지에서 취약성을 찾습니다. Snyk 사용하면 프로젝트를 원본에서 수정하는 것보다 쉽게 분석할 수 있습니다. 지정된 취약한 패키지가 도입된 지점을 빠르게 식별할 수 있습니다.

#### Snyk 오픈 소스 파일 형식

snyk 테스트가 실행될 때 다음 파일을 찾고 찾은 파일 중 첫 번째 파일을 검색하여 프로젝트 유형을 자동으로 탐지하려고 합니다(여러 매니페스트 파일을 분석하려면 [scan multiple manifest files](cli-snyk.md#monorepos-and-projects-with-multiple-manifest-files)을 참조하십시오).

Snyk가 프로젝트 유형을 자동 검색하는 데 사용하는 파일에는 다음이 포함되지만 이에 국한되지는 않습니다.

* yarn.lock
* package-lock.json
* package.json
* Gemfile.lock
* pom.xml
* build.gradle
* build.sbt
* Pipfile
* requirements.txt
* Gopkg.lock
* vendor/vendor.json
* obj/project.assets.json
* packages.config
* composer.lock
* build.gradle.kts
* go.mod

Snyk 파일을 분석하고 트리를 만드는 방법은 다음과 같습니다.

* 사용하는 [language and package manager](broken-reference)(매니페스트 파일 유형에 따라 결정됨)
* 검색 방법([Snyk CLI](broken-reference)를 사용하거나 Snyk [Git repository integration](broken-reference)에서 가져오기)

### 여러 매니페스트 파일 스캔

매니페스트 파일이 여러 개인 프로젝트의 경우 `--file` 옵션을 사용하여 Snyk에서 패키지 정보를 검사할 파일을 지정하십시오.

`$ snyk test --file=package.json`

모든 파일을 식별하려면 **--all-projects** 옵션을 사용합니다.

`$ snyk test --all-projects`

### Custom name이 있는 매니페스트 파일

매니페스트 파일이 지원되는 언어에서 사용자 정의 이름을 가진 경우 file 옵션과 package-manager 옵션의 조합을 사용하여 사용자 정의 이름을 Snyk에 전달할 수 있습니다.

`$ snyk test --file=req.txt --package-manager=pip`

### 개발 의존성 테스트

많은 패키지 관리자들은 개발 또는 테스트 컨텍스트에서만(즉, 결국 생산으로 배송되지 않음) 별도로 종속성을 호출하는 것을 허용합니. 기본적으로 Snyk 이러한 종속성을 검색하지 않습니다. 개발 종속성을 검색에 포함하려면 `--dev` 옵션을 사용하십시오.

`$ snyk test --dev`

지원되는 언어에 대한 자세한 내용은 [Open Source language and package manager support](broken-reference) 참조하십시오.
