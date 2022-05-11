# AWS CodePipeline 통합

Snyk은 AWS CodePipeline과 원활하게 통합되어 애플리케이션에 오픈 소스 보안 취약점이 있는지 검색하고 지속적인 전송 서비스를 통해 안전한 애플리케이션을 제공할 수 있도록 지원합니다. 이러한 통합을 통해 CodePipeline 사용자는 보안을 빌드, 테스트 및 배포 단계의 자동화된 부분으로 만들 수 있습니다.

{% hint style="info" %}
Snyk 통합은 현재 AWS `sa-east-1` | `ca-central-1` | ap-`southeast-1` | `ap-southeast-2` | `ap-south-1` | `ap-northeast-2` | `ap-northeast-1` | `eu-west-3` | `eu-west-1` | `eu-north-1` | `us-east-1` | `us-west-2` | `eu-west-2` | `eu-central-1` 지역에서 사용할 수 있습니다. Snyk은 추가로 확장하기 위해 적극적으로 노력하고 있습니다.
{% endhint %}

## 개발 언어 지원

다음 개발 언어에서 AWS CodePipeline과의 Snyk 통합이 지원됩니다.

* JavaScript
* Java
* .NET
* Python
* Ruby
* PHP
* Scala
* Swift/Objective-C
* Go

## 설정

AWS CodePipeline 콘솔에서 직접 Snyk AWS CodePipeline 통합을 시작할 수 있습니다.

다음 단계를 사용하여 새 파이프라인 또는 기존 파이프라인에 Snyk을 추가합니다.

### 요구 사항

CodePipeline에서 스캔하기 전에 프로젝트를 빌드해야 하는지 확인합니다. 프로젝트를 빌드해야 하는 경우 Snyk 단계 전에 CodeBuild 단계를 추가해야 합니다.

|      Language     | Project Type | Build Required |                                  Notes                                 |
| :---------------: | :----------: | -------------- | :--------------------------------------------------------------------: |
|     Javascript    |      npm     | No\*           |   `package-lock.json` 파일이 없는 경우에만 빌드해야 합니다. npm install을 실행하여 생성하십시오.  |
|     Javascript    |     Yarn     | No\*           |       `yarn.lock` 파일이 없는 경우에만 빌드 필요. 생성하기 위해yarn install을 실행합니다.       |
|        Java       |     Maven    | Yes            |                     테스트하기 전에 `mvn install`을 실행합니다.                     |
|        Java       |    Gradle    | No             |                                                                        |
|        .NET       |     Nuget    | No\*           |                 `packages.config` 파일이 없는 경우에만 빌드해야 합니다.                |
|       Python      |      Pip     | No\*           |              언어 설정 파라미터가 있는 Snyk 구성 파일이 없는 경우에만 빌드해야 합니다.              |
|       Python      |   Setup.py   | Yes            |                  테스트하기 전에 `pip install -e .` 를 실행하십시오.                 |
|       Python      |    Poetry    | No\*           |    `poetry.lock` 파일이 없는 경우에만 빌드해야 합니다. `poetry lock` 을 실행하여 생성하십시오.    |
|        Ruby       |    Bundler   | No\*           |   `Gemfile.lock` 파일이 없는 경우에만 빌드해야 합니다.`bundle install` 을 실행하여 생성하십시오.  |
|        PHP        |   Composer   | No\*           | `composer.lock` 파일이 없는 경우에만 빌드해야 합니다.`composer install` 을 실행하여 생성하십시오. |
|       Scala       |      SBT     | No             |                                                                        |
|         Go        |  Go Modules  | No             |                                                                        |
| Swift/Objective-C |   Cocoapods  | No\*           |     `Podfile.lock` 파일이 없는 경우에만 빌드해야 합니다. pod install을 실행하여 생성하십시오.     |

### CodeBuild 단계 Example

Note the Scan's input artifact must be provided with the build's output artifact as shown in the configuration구성에 표시된 대로 스캔의 입력 아티팩트와 빌드의 출력 아티팩트가 함께 제공되어야 합니다.

Javascript CodeBuild (`buildspec.yml`) 예시:

```
version: 0.2
phases:
  build:
    commands:
      - npm install
artifacts:
  files:
    - '**/*'
```

Maven CodeBuild (`buildspec.yml`) 예시:

```
version: 0.2
phases:
  build:
    commands:
      - mvn install
artifacts:
  files:
    - '**/*'
```

### 1단계: 단계 추가

Source 단계 이후 언제든지 Snyk 검색 단계를 추가하여 CI/CD 파이프라인의 다른 단계에서 애플리케이션을 테스트할 수 있습니다.

**Edit**을 클릭하여 **Scan 단계**를 추가합니다.

![Add scan stage](../../../.gitbook/assets/aws-cp-add-stage.png)

### 2단계: 작업 그룹 추가

**Add an Action Group**을 클릭하여 **Edit Action** 화면을 엽니다.

![Edit action window](../../../.gitbook/assets/aws-cp-edit-action.png)

액션의 이름을 지정한 다음 **Snyk**을 **Action Provider**로 선택합니다.

연결 프로세스를 시작하려면 **Connect with Snyk**을 클릭합니다.

### 3단계: Snyk에 연결

오픈 소스 코드 검색을 시작할 수 있는 AWS CodePipeline 권한을 부여하려면 Snyk 인증 방법을 선택하십시오.

![Snyk log in screen](../../../.gitbook/assets/snyk-cp-int-config.png)

### 4단계: 설정 구성

다음과 같은 옵션을 구성할 수 있습니다.

![Snyk AWS CodePipeline 구성 옵션](../../../.gitbook/assets/spaces\_-MdwVZ6HOZriajCf5nXH\_uploads\_git-blob-be8913b4d2111a85ddddb099a6a4c8bb87918632\_Snyk\_AWS\_CodePipeline\_Config\_y\_CodePipeline\_-\_AWS\_Developer\_Tools\_png.png)

* **Snyk organization:** 소견 보고서를 저장할 Snyk 조직을 선택합니다.
* **Vulnerability handling**: 취약성이 발견된 경우 파이프라인 동작을 정의합니다. `Block deployment when Snyk finds an error` 확인란을 선택하면 파이프라인이 실패하고 CodePipeline의 다음 단계로 진행되지 않습니다.
* **Block deployment for vulnerabilities with a minimum severity of**: **low**|**medium**|**high**|**critical**: 지정된 수준 이상의 취약만 보고합니다.
*   **Monitoring behavior on build**: AWS CodePipeline에서 프로젝트를 모니터링하는 기준을 설정합니다. 사용 가능한 옵션은 다음과 같습니다.

    * **Always monitor**: 프로젝트 스냅샷은 테스트 결과와 독립적으로 생성됩니다.
    * **When test fails**: 테스트에 실패한 경우에만 프로젝트 스냅샷이 생성됩니다.
    * **When test passes**: 테스트에 성공한 경우에만 프로젝트 스냅샷이 생성됩니다.
    * **Never monitor**: 프로젝트 스냅샷이 생성되지 않습니다.

    **Never monitor** 옵션을 선택하지 않은 경우 **Project to monitor** 필드는 필수입니다. 이는 이름 지정 충돌로 인한 의도하지 않은 프로젝트 재정의를 방지하기 위한 것입니다. 선택한 **Snyk organization**과 연결된 보고서가 생성됩니다.
* **Project to monitor**: 프로젝트의 프로젝트 그룹 이름을 지정하십시오. 이는 CLI에서 [remote-repo-url](https://support.snyk.io/hc/en-us/articles/360000910677-Snyk-CLI-monitored-projects-are-created-with-IDs-in-the-project-name) 옵션을 사용하는 것과 같습니다. 필드에는 이름에 공백을 사용할 수 없습니다. **Never monitor** 옵션을 선택한 경우를 제외하고 이 필드는 필수입니다.
* **Auto-detect all projects in the working directory**: AWS CodePipeline의 모든 프로젝트를 자동으로 검색하려면 이 확인란을 선택합니다. 이 옵션을 선택하지 않으면 플러그인은 `--all-projects` 옵션을 사용하여 모든 프로젝트를 검색하기 때문에 발견된 첫 번째 프로젝트를 테스트합니다.
* **Advanced options** (선택 사항):
  * **Excluded directories**: 이 옵션은 **Auto-detect all projects**를 선택한 경우에만 나타납니다. 제외할 하위 디렉터리를 지정하십시오. 디렉터리는 쉼표로 구분해야 합니다.
  * **Custom path to manifest file to test**: 이 옵션은 **Auto-detect all projects**를 선택하지 않은 경우에만 나타납니다. Snyk가 검색할 매니페스트 파일의 파일 경로를 지정할 수 있습니다. 이 옵션을 생략하면 Snyk은 프로젝트의 매니페스트 파일을 자동으로 탐지하려고 합니다.
  * **Additional arguments:** 테스트 및 모니터링에 적용할 수 있는 여러 추가 옵션이 허용됩니다. 옵션은 `--dev`, `--detection-depth`, `--prune-repeated-subdependencies`, `--strict-out-of-sync`, `--yarn-workspaces`, `--skip-unresolved`입니다. 이러한 옵션에 대한 자세한 내용은 [CLI reference](https://docs.snyk.io/features/snyk-cli/cli-reference)를 참조하십시오.

{% hint style="info" %}
이전에 구성된 단계의 구성 설정을 변경하려면 **Snyk** 링크를 클릭합니다.
{% endhint %}

메시지가 나타나면 Snyk에 대한 연결을 확인합니다.

![Confirm connection with OAuth](../../../.gitbook/assets/aws-cp-confirm-oauth.png)

Snyk에 성공적으로 연결한 후 파이프라인을 저장합니다.

CodePipeline에서 Snyk 단계가 구성되어 응용프로그램을 테스트할 수 있습니다. 최신 변경사항을 적용하려면 CodePipeline 옵션을 통해 최신 변경사항을 릴리스하십시오.

## 검색 결과 확인

AWS CodePipeline 콘솔에서 스캔 단계에서 **Details**를 클릭하여 스캔 결과를 확인할 수 있습니다.

![Details in the Scan stage](../../../.gitbook/assets/aws-cp-findings-report.png)

자세한 취약점 보고서를 확인하려면 **link to execution details** 링크를 클릭합니다.

![Link to execution details](../../../.gitbook/assets/image4-2-.png)

## Test 보고서 세부 정보

Snyk은 애플리케이션의 매니페스트 파일을 분석하고 디펜던시 목록을 Snyk 취약점 데이터베이스와 연관시킵니다. Snyk은 [오픈 소스 코드에 대한 자세한 보고서를 제공합니다](../../reports/reports-overview.md). 매니페스트 파일을 분석함으로써 Snyk은 완전한 디펜던시 트리를 구축하여 직접적인 의존성과 전이적 의존성을 모두 정확하게 식별한다(과도적 의존성은 Snyk에 의해 감지된 취약점의 78%를 차지한다). 이를 통해 Snyk은 취약점이 애플리케이션에 어떻게 도입되었는지 정확하게 확인할 수 있습니다.

![Snyk test report](../../../.gitbook/assets/prototype.png)

{% hint style="info" %}
보고서는 만료되기 전에 14일 동안 저장됩니다. 이후의 파이프라인 실행은 보고서를 업데이트하고 보존 기간을 재설정합니다.
{% endhint %}
