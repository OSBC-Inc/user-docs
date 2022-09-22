# Visual Studio 확장

Visual Studio 확장([Snyk Security - Code and Open Source Dependencies](https://marketplace.visualstudio.com/items?itemName=snyk-security.snyk-vulnerability-scanner-vs))은 프로젝트의 보안 취약성을 찾고 수정하는 데 도움이 됩니다. 몇 초 내에 확장 프로그램은 실행 가능한 수정 조언과 함께 식별된 다양한 유형의 보안 취약점 목록을 제공합니다. 이 확장은 Snyk 오픈 소스와 Snyk 코드라는 두 가지 Snyk 제품의 기능을 결합합니다.

1. Snyk Open Source는 프로젝트에 포함된 직접 및 간접(전이적) 오픈 소스 종속성 모두에서 알려진 취약점을 찾습니다.
2. Snyk Code는 귀하와 귀하의 팀이 작성한 코드를 보고 알려진 보안 취약점과 코드 품질 Issue를 놀라운 속도로 찾아냅니다.

## 소프트웨어 요구 사항

* 운영 체제 - Windows
* 지원되는 Visual Studio 버전: 2015, 2017, 2019, 2022. Community, Professional 및 Enterprise와 호환 가능

## 지원되는 언어, 패키지 관리자 및 프레임워크

* Snyk Open Source의 경우: Visual Studio 확장은 Snyk Open Source 및 CLI에서 지원하는 모든 언어 및 패키지 관리자를 지원합니다. [문서의 전체 목록](../../../snyk-products/snyk-open-source/language-and-package-manager-support/)을 참조하세요.
* Snyk 코드의 경우: Visual Studio 확장은 Snyk 코드에서 지원하는 [모든 언어와 프레임워크](../../../snyk-products/snyk-code/snyk-code-language-and-framework-support.md)를 지원합니다.

## 확장 프로그램 설치

IDE에서 직접 Snyk 확장을 설치할 수 있습니다. **Extensions > Manage Extensions**를 엽니다.

![확장 메뉴 관리](../../../.gitbook/assets/readme\_image\_2\_1\_1.png)

Snyk을 검색하고 **Download**를 선택하여 Snyk Security - Code and Open Source Dependencies extension을 다운로드합니다.

설치가 완료되면 **Extensions > Snyk** 메뉴를 통해 Snyk를 사용합니다(Visual Studio 2019 이전 버전에서는 Snyk가 상단 메뉴 모음의 일부임).

![](<../../../.gitbook/assets/image (76).png>)

You can also open the Snyk tool window using **View > Other Windows > Snyk**_._

**View > Other Windows > Snyk**을 사용하여 Snyk 도구 창을 열 수도 있습니다.

도구 창이 열리면 Snyk 확장이 최신 Snyk CLI 버전을 다운로드하는 동안 기다립니다.

![Snyk 도구 창, CLI 다운로드](../../../.gitbook/assets/readme\_image\_2\_3.png)

확장 및 CLI를 설치한 후 인증해야 합니다. **Visual Studio를 Snyk에 연결** 링크를 사용할 수 있습니다. 자세한 내용은 [인증](visual-studio-extension.md#authentication)을 참조하십시오.

## 구성

프로젝트를 분석하기 위해 플러그인은 환경 변수가 필요한 Snyk CLI를 사용합니다:

* `PATH`: 필요한 바이너리의 경로를 지정하십시오(예: Maven).
* `JAVA_HOME`: Java 종속성 분석에 사용할 JDK의 경로를 지정하십시오.
* `http_proxy` 와 `https_proxy`: `http://username:password@proxyhost:proxyport` 형식의 값을 사용하여 프록시 서버 뒤에 있는 경우 설정합니다.\
  **Note:** 값의 선행 `http://`는 `https_proxy`의 경우 `https://`로 변경되지 않습니다.

GUI를 사용하거나 `setx` 도구를 사용하여 명령줄에서 변수를 설정할 수 있습니다.

## 인증

개요 페이지의 **Snyk에 Visual Studio 연결 링크**를 사용하여 인증합니다.

![Visual Studio를 Snyk에 연결](../../../.gitbook/assets/readme\_image\_2\_4.png)

옵션을 사용하여 인증할 수도 있습니다. Visual Studio **Options**를 열고 Snyk extension의 **General Settings**으로 이동하거나 도구 모음에서 **Settings** 버튼을 사용합니다.

![옵션 및 설정 버튼](../../../.gitbook/assets/readme\_image\_2\_5.png)

자동화된 방법이 작동하지 않는 경우 **Authenticate** 버튼을 눌러 인증을 트리거하거나 사용자 API 토큰을 수동으로 입력할 수 있습니다.  [Snyk support](https://snyk.zendesk.com/agent/dashboard)에 요청을 제출할 수도 있습니다.

![토큰 필드 및 인증 버튼](../../../.gitbook/assets/readme\_image\_2\_6.png)

![인증 버튼을 클릭하거나 API 토큰을 입력하세요.](../../../.gitbook/assets/install-5-a.png)

Snyk 웹 사이트에서 신원을 확인하고 IDE 확장에 연결합니다. **Authenticate** 버튼을 클릭합니다.

![](../../../.gitbook/assets/install-6.png)

인증이 확인되면 브라우저를 닫고 IDE 확장으로 돌아갑니다. 토큰 필드가 인증 토큰으로 채워지고 인증이 완료됩니다.

![인증 토큰으로 채워진 토큰 필드](../../../.gitbook/assets/readme\_image\_2\_8.png)

## 분석 실행

솔루션을 열고 Snyk 스캔을 실행하십시오. 솔루션의 크기와 종속성 그래프를 작성하는 데 필요한 시간에 따라 취약점을 얻는 데 1분에서 2분 미만이 소요됩니다.

확장은 사용자에게 두 가지 종류의 결과를 제공합니다:

* 오픈 소스 취약점
* Snyk 코드 issues

### Open Source 취약점

* CLI가 종속성을 선택하고 취약점을 찾을 수 있도록 하려면 솔루션을 성공적으로 빌드해야 합니다.
* C#/.NET 프로젝트와 관련이 없는 npm 취약점 또는 취약점만 보이는 경우 프로젝트가 성공적으로 빌드되지 않았고 CLI에서 감지하지 못했음을 의미할 수 있습니다. 어려움이나 질문이 있는 경우 [Snyk support](https://snyk.zendesk.com/agent/dashboard)에 요청을 제출하십시오.

![스캔 실행](../../../.gitbook/assets/readme\_image\_3\_1\_1.png)

![Open Source 취약점](../../../.gitbook/assets/readme\_image\_3\_1\_2.png)

### Snyk 코드 Issues

Snyk 코드 분석은 애플리케이션 코드에서 발견된 보안 취약점 및 코드 Issue 목록을 보여줍니다. 다른 사람들이 Issue를 해결한 방법에 대한 자세한 내용과 예를 보려면 보안 취약성 또는 코드 보안 Issue를 선택하고 패널에서 Snyk 제안 정보를 검토하십시오.

<figure><img src="../../../.gitbook/assets/spaces_-MdwVZ6HOZriajCf5nXH_uploads_git-blob-05b86ea86ef80da4a7669fe4ea2958bbbcd5e008_readme_image_3_1_3.png" alt=""><figcaption><p>Snyk 제안 패널</p></figcaption></figure>

Snyk 제안 패널은 예를 들어 코드의 변수 이름과 빨간색 줄 번호를 사용하여 Snyk 엔진의 인수를 보여줍니다. 다음을 볼 수도 있습니다.

* 버그 패턴을 더 자세히 설명하기 위해 외부 리소스에 대한 링크를 제공합니다.
* Security(발견된 Issue는 보안 Issue임), Database(Issue는 데이터베이스 상호 작용과 관련됨) 또는 In Test(Issue는 테스트 코드 내에 있음)와 같이 Snyk에서 할당한 태그입니다.
* 다른 사람들이 Issue를 해결한 방법을 확인하는 데 도움이 될 수 있는 오픈 소스 리포지토리의 코드입니다.

## 분석 결과 보기

이름 또는 심각도별로 취약점을 필터링할 수 있습니다.

검색 창에 취약점 이름을 입력하여 이름으로 필터링합니다.

![이름으로 필터링](../../../.gitbook/assets/readme\_image\_3\_2\_1.png)

검색 창 필터를 열 때 하나 이상의 심각도를 선택하여 심각도별로 필터링합니다.

![심각도별로 필터링](../../../.gitbook/assets/readme\_image\_3\_2\_2.png)

사용자는 **Project settings**로 Snyk 확장을 구성할 수 있습니다.

**Note**: "Scan all projects" 옵션은 기본적으로 활성화되어 있습니다. Snyk CLI에 대한 `--all-projects` 옵션을 추가합니다. 이 옵션은 기본적으로 모든 프로젝트를 스캔합니다.

![Scan all projects 활성화](../../../.gitbook/assets/readme\_image\_3\_3.png)

## 확장 구성

플러그인이 설치된 후 확장에 대해 다음 구성을 설정할 수 있습니다:

* **Token**: 확장 프로그램이 Snyk에 연결하는 데 사용하는 토큰을 입력하십시오. 다른 계정으로 전환해야 하는 경우 수동으로 바꿀 수 있습니다.
* **Custom endpoint**: 조직에 대한 사용자 지정 Snyk API 끝점을 지정합니다.
* **Ignore unknown CA**: 알 수 없는 인증 기관을 무시합니다.
* **Organization**: 특정 조직에 연결된 Snyk 명령을 실행하려면 ORG\_NAME을 지정하십시오. 이 설정을 사용하면 해당 조직에 대한 테스트를 실행할 조직 슬러그 이름을 지정할 수 있습니다. 값은 Snyk UI에서 조직의 URL(`https://app.snyk.io/org/[orgslugname]`)에 표시된 URL 슬러그와 일치해야 합니다. 지정하지 않으면 [web account settings](https://app.snyk.io/account)에 정의된 기본 조직이 테스트를 실행하는 데 사용됩니다.
* **Send usage analytics**: Snyk이 확장을 개선하는 데 도움이 되도록 Visual Studio에서 확장이 작동하는 방식에 대한 정보를 Snyk에 보내도록 합니다.
* **Project settings**: 추가 Snyk CLI 매개변수를 지정하십시오.
* **Scan all projects**: 기본적으로 활성화되어 있는 작업 디렉토리의 모든 프로젝트를 자동 감지합니다.

설정에서 받고 싶은 결과를 선택할 수도 있습니다.

* Open Source 취약
* Snyk Code 보안 취약점
* Snyk Code 품질 Issues

## 알려진 issue

**지원되는 대상 파일을 감지할 수 없습니다.**

**솔루션** Visual Studio 옵션을 열어 Snyk 확장의 프로젝트 설정으로 이동하고 모든 프로젝트 스캔을 선택하십시오.

![](../../../.gitbook/assets/readme\_image\_4\_1.png)

## 방법

### 로그 파일을 찾는 방법

로그는 사용자 AppData 디렉터리에서 찾을 수 있습니다:

```
%HOMEPATH%\AppData\Local\Snyk\snyk-extension.log
```

### 빌드 프로세스

이 저장소를 로컬로 복제:

```
git clone https://github.com/snyk/snyk-visual-studio-plugin.git
```

Nuget 패키지 복원:

```
nuget restore
```

빌드 실행:

```
msbuild -t:Build
```

## 유용한 링크

* 이 플러그인은 .NET, Java, JavaScript 및 더 많은 언어로 작성된 프로젝트에서 작동합니다.\
  [Snyk가 지원하는 언어 및 패키지 관리자의 전체 목록 보기](https://support.snyk.io/hc/en-us/sections/360001087857-Language-package-manager-support)
* [Bug tracker](https://github.com/snyk/snyk-visual-studio-plugin/issues)
* [Github repository](https://github.com/snyk/snyk-visual-studio-plugin)

## 지원 및 연락처 정보

{% hint style="info" %}
도움이 더 필요하세요? [Snyk support](https://snyk.zendesk.com/agent/dashboard)에 요청을 제출하십시오.
{% endhint %}

**경험을 공유하세요.**

Snyk는 Snyk 플러그인 경험을 개선하기 위해 지속적으로 노력하고 있습니다. Snyk Visual Studio 확장에 대한 피드백을 공유하시겠습니까? [미팅 잡기](https://calendly.com/snyk-georgi/45min?month=2022-01).
