---
description: 이 문서를 사용하여 Eclipse 플러그인을 시작하십시오.
---

# Eclipse 플러그인

Eclipse 워크플로에 **Snyk Security - Code and Open Source Dependencies**를 설치하여 코드베이스에 병합되기 전에 IDE(통합 개발 환경) 내에서 직접 취약점 및 라이선스 문제를 노출합니다.

Eclipse 플러그인을 설치 및 구성한 후 실행할 때마다 Snyk은 프로젝트의 매니페스트 파일을 스캔하고 다음 작업을 수행합니다.

* 실행 가능한 취약점 및 라이선스 issue 세부 정보를 분석하고 제공합니다.
* 패키지당 결과 기록
* Eclipse UI에서 직접 결과 표시

Snyk Eclipse 플러그인을 사용하면 애플리케이션 보안에 위협이 되는 문제를 추적 및 식별할 수 있으며 이러한 문제가 공유 저장소에 추가되는 것을 방지할 수 있습니다.

{% hint style="info" %}
Snyk Eclipse 플러그인은 [Eclipse Marketplace](https://marketplace.eclipse.org/content/snyk-security-scanner)에서 설치할 수 있습니다.
{% endhint %}

## 지원되는 언어 및 저장소

Snyk은 Eclipse와 Snyk에서 모두 지원하는 모든 언어를 지원합니다. 또한 Snyk 플러그인은 Snyk Broker 및 온프레미스 솔루션으로 구현할 수 있습니다.

## Snyk Eclipse 플러그인 설치

1. 실행 중인 Eclipse 인스턴스 내에서 Marketplace로 이동합니다.
2. Snyk 검색하고 Install을 클릭합니다.
3. 라이센스 계약에 동의하라는 메시지가 표시되면 Snyk Security 인증서를 추가하여 설치를 완료합니다.
4. Eclipse 인스턴스를 다시 시작하고 **Eclipse Preferences**로 이동하여 이제 **Snyk Security - Code and Open Source Dependencies**가 목록에 나타나는지 확인합니다.

![Snyk 플러그인 및 설치 버튼을 보여주는 Eclipse Marketplace 검색](../../../.gitbook/assets/uuid-01198b42-f020-2cc5-c20f-93817eeb44a4-en.png)

## 구성

Snyk 사용하려면 환경 변수와 Snyk 토큰을 플러그인에 제공해야 합니다.

### API 토큰

API 토큰을 제공하려면 [account settings](https://app.snyk.io/account)에서 복사하여 Eclipse 기본 설정 Snyk API 토큰 필드에 붙여넣습니다. **적용 및 닫기**를 클릭하여 분석을 시작합니다.

![Eclipse preferences with Snyk API Token filed and Apply and Close button](../../../.gitbook/assets/uuid-928012b7-8e49-fe6f-4965-77c5db026784-en.png)

### 환경 변수

프로젝트를 분석하기 위해 플러그인은 Snyk CLI를 사용합니다. CLI에는 다음 환경 변수가 필요합니다:

* `PATH`: 필요한 바이너리(예: 메이븐)로 가는 경로입니다. `PATH` 변수는 설정 대화 상자의 `Path` 필드를 사용하여 수동으로 조정할 수도 있습니다.
* `JAVA_HOME`: Java 종속성을 분석하는 데 사용하려는 JDK의 경로
* `http_proxy`  `https_proxy`: 형식의 값을 사용하여 설정`http://username:password@proxyhost:proxyport`.\
  **Note:** 값의 선행 `http://`는 `https_proxy`의 경우 `https://`로 변경되지 않습니다.

명령행에서 Eclipse를 시작하지 않거나 쉘 환경을 사용하여 Eclipse를 시작하는 스크립트 파일을 작성하지 않는 경우 쉘 환경에서만 이러한 변수를 설정하는 것(예: **\~/.bashrc** 사용)으로는 충분하지 않습니다.

* **Windows**에서는 GUI를 사용하여 변수를 설정하거나 [setx](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/setx) 도구를 사용하여 명령줄에서 변수를 설정합니다.
* **macOS**에서 launchd 프로세스는 Finder에서 직접 Eclipse를 시작하기 위해 환경 변수를 알아야 합니다. `launchctl setenv` 명령을 사용하여 이러한 환경 변수를 설정합니다(예: 시작 시 또는 사용자 로그인 시 실행하는 스크립트 사용).\
  **Note:** macOS UI에 대한 환경 변수 제공은 운영 체제 릴리스 간에 변경될 수 있으므로 `~/.bashrc`를 통해 정의할 수 있는 셸 환경을 활용하기 위해 Eclipse 앱을 시작하는 작은 셸 스크립트를 만드는 것이 더 쉬울 수 있습니다.
* **Linux**에서는 `/etc/environment` 파일을 업데이트하여 환경 변수를 Windows 관리자 및 UI로 전파할 수 있습니다.

## Snyk 플러그인을 사용하여 Eclipse 프로젝트 보호

Snyk 결과에서 프로젝트를 스캔할 준비가 되면 녹색 화살표(![](../../../.gitbook/assets/uuid-aa090aa8-d4fe-eb5d-2505-54a0b1555be9-en.png))를 클릭합니다. 결과는 짧은 시간에 나타나고 그동안 평소와 같이 계속 작동합니다.

어떤 이유로든 빌드가 끝나기 전에 스캔을 중지해야 하는 경우 빨간색 사각형(![](../../../.gitbook/assets/uuid-29be01e6-6913-25f8-15ed-a8cf47230fa0-en.png))을 클릭합니다. 작업 공간에서 단일 프로젝트만 스캔하려면 패키지 탐색기 패널로 이동하여 테스트하려는 프로젝트의 루트를 마우스 오른쪽 버튼으로 클릭한 다음 **Snyk test**를 선택합니다.

스캔이 끝나면 Snyk 결과에서 결과 및 관련 오류 메시지가 다음과 유사한 프로젝트별로 그룹화되어 표시됩니다.

![Eclipse 플러그인으로 스캔한 결과 화면](../../../.gitbook/assets/uuid-e868f739-eb55-9bd6-be33-acbb230ec1fa-en.png)

## Eclipse 프로젝트에 대한 Snyk 결과 작업

### 상황에 맞는 메뉴

오른쪽 클릭 메뉴

옵션에는 다음이 포함됩니다:

**Ignore issue**—다음 30일 동안 무시할 특정 문제 위로 마우스를 가져간 다음 상황에 맞는 메뉴에 액세스합니다.

**Snyk test**—전체 작업 공간에 대해 Snyk 테스트를 실행합니다.

**Preferences**—오른쪽 클릭 메뉴에서 직접 Snyk Vuln 스캐너 기본 설정에 액세스하고 업데이트합니다.

### 축소 시

**Title:** 프로젝트의 이름입니다.

**Dependency:** 취약점 요약 및 각 프로젝트에 대해 발견된 영향을 받는 경로 수.

### 확장 시

**Title:** 프로젝트에 영향을 미치는 취약점의 전체 이름으로, Snyk 데이터베이스의 취약점에 대한 설명 및 전체 세부 정보와 연결되어 문제 해결을 지원합니다.

**Dependency:** 직접 또는 간접적으로 취약점의 영향을 받는 프로젝트의 직접 종속성 패키지(명시적으로 설치한 패키지)의 이름입니다.

모든 세부 정보는 단일 행에 표시되며 종속성(코드에서 명시적으로 사용된 패키지 이름) 및 패키지(실제로 취약점이 포함된 패키지 이름) 열은 모두 동일한 패키지의 이름을 표시합니다.

{% embed url="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-MdwVZ6HOZriajCf5nXH%2Fuploads%2Fgit-blob-4cdd086d6be47b598fc1a9a52c63023d59cff825%2Fuuid-e7accdc1-7495-e7a5-7a64-2403b066cb03-en.png?alt=media&token=e3bf024a-ba92-4b76-87be-b728d7edf092" %}
Eclipse 결과 세부정보
{% endembed %}

다음 예와 유사하게 모든 관련 세부 정보를 그룹화하는 화살표가 행에 나타납니다.

{% embed url="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-MdwVZ6HOZriajCf5nXH%2Fuploads%2Fgit-blob-85e429be9a965c2dc534817a648773176a724531%2Fuuid-c71f67d1-80a3-7485-b33b-e602a1a5050e-en.png?alt=media&token=99e95293-bb37-4fed-8388-d9cb56a73092" %}
행 그룹화 세부 정보의 Eclipse 결과 화살표
{% endembed %}

**프로젝트가 간접 취약점의 영향을 받는 경우의 종속성, 축소 모드:**

{% embed url="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-MdwVZ6HOZriajCf5nXH%2Fuploads%2Fgit-blob-85e429be9a965c2dc534817a648773176a724531%2Fuuid-c71f67d1-80a3-7485-b33b-e602a1a5050e-en.png?alt=media&token=99e95293-bb37-4fed-8388-d9cb56a73092" %}
축소 모드, 간접 취약성
{% endembed %}

예:

패키지 X는 패키지 Y를 사용하고 차례로 패키지 Z를 사용합니다.

패키지 Z에는 프로젝트에 간접적으로 영향을 미치는 XSS(교차 사이트 스크립팅) 취약점이 포함되어 있습니다.

종속성(코드에서 명시적으로 사용된 패키지의 이름)은 패키지 X입니다. 패키지 필드에는 패키지 Z(실제로 취약점이 포함된 패키지 이름)가 표시됩니다.

**프로젝트가 간접 취약점의 영향을 받는 경우의 종속성, 확장 모드:**

행의 화살표를 클릭하여 직접 종속성에서 취약한 패키지까지의 전체 경로를 확장하고 봅니다.

{% embed url="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-MdwVZ6HOZriajCf5nXH%2Fuploads%2Fgit-blob-992b169b89e7f3c45782fdeb47b205e3c0a95af8%2Fuuid-35658aaf-3359-80c2-c094-41a34c7863cc-en.png?alt=media&token=53c91ccc-f9bc-4ba7-a55f-8def3aa50d86" %}
Expanded mode, indierct vulnerability
{% endembed %}

이전 화면에서 전체 경로는 다음과 같이 표시됩니다:

\[패키지 X의 이름]-->\[패키지 Y의 이름]-->\[패키지 Z의 이름]

**Package:** 취약점의 직접적인 영향을 받는 프로젝트의 패키지 이름입니다. 이전 화면에서:

* 종속성은 패키지 X로 표시됩니다. 이는 개발자가 코드에서 명시적으로 사용하는 패키지입니다.
* 패키지 필드에는 취약점이 포함된 패키지인 패키지 Z가 표시됩니다.

**Fix:** 패키지 이름(있는 경우) 및 문제를 해결하기 위해 업그레이드할 수 있는 버전입니다.

## 지원 / 연락처

{% hint style="info" %}
도움이 필요하면 Snyk 지원에 요청을 [제출](https://support.snyk.io/hc/en-us/requests/new)하십시오.
{% endhint %}

## 경험을 공유하십시

Snyk Snyk 플러그인 경험을 개선하기 위해 지속적으로 노력하고 있습니다. Snyk Eclipse 플러그인에 대한 피드백을 공유하려면 [회의를 예약](https://calendly.com/snyk-georgi/45min?month=2022-09)하십시오.
