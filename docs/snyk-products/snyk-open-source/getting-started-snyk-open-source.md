# Snyk Open Source 시작하기

Snyk Open Source를 이용하여 애플리케이션의 오픈 소스 라이브러리 취약점을 스캔하고 수정할 수 있습니다.

{% hint style="info" %}
이 프로세스는 Snyk.io UI 및 SCM(Source Code Management) 시스템을 사용하여 시작하는 방법을 설명합니다.

* [IDE 도구](https://docs.snyk.io/integrations/ide-tools) 또는 [CI/CD 통합](https://docs.snyk.io/integrations/ci-cd-integrations)을 사용할 수도 있습니다. [통합](https://docs.snyk.io/integrations)을 참조하십시오.
* [Snyk CLI](broken-reference)를 사용할 수도 있습니다. [Snyk CLI 시작하기](broken-reference)를 참조하십시오.
{% endhint %}

### 전제 조건

다음 사항이 존재하는지 확인하십시오.

* Snyk 계정 ([https://snyk.io/](https://snyk.io)로 이동하여 가입 - 자세한 내용은 [시작하기](../../getting-started/) 참조)
* GitHub와 같은 지원되는 [소스 코드 관리 시스템](../../features/integrations/git-repository-scm-integrations/)에서 오픈소스 패키지를 사용하는 프로젝트
* Java와 같은 지원되는 [언어 및 패키지 매니저](language-and-package-manager-support/)

### 1단계: **Source control** 통합 추가

{% hint style="info" %}
이미 통합을 설정한 경우 3단계로 이동하십시오.
{% endhint %}

Snyk에서 프로젝트를 작업할 수 있도록 Source control \*\*\*\* 통합을 진행합니다.

1. Snyk.io에 로그인합니다.
2. **Integrations > Source control**을 선택합니다.
3. Snyk과 통합할 소스 제어 시스템(예: Github)을 클릭합니다.
4. Snyk 액세스 권한을 부여하기 위해 계정 인증 정보를 입력하거나 Github 계정으로 인증을 진행합니다.

### 2단계: 프로젝트 추가

Snyk에서 테스트하고 모니터링할 저장소를 선택하여 Snyk으로 테스트할 프로젝트를 추가합니다.

1. Snyk.io에서 **Projects**를 선택합니다.
2. 프로젝트를 추가할 도구(예: Github)를 선택합니다.
3. **Personal and Organization repositories**에서 사용할 저장소를 선택합니다.
4. **Add selected repositories**를 클릭하여 선택한 저장소를 프로젝트로 가져옵니다. 해당 저장소는 다음과 같이 설정합니다.
   1. 취약점에 대한 정기적인 검사(기본적으로 매일)를 실행하도록 설정합니다.
   2. Webhook을 생성하므로 코드를 변경할 때 Snyk은 pull / merge requests를 테스트하여 새로운 디펜던시가 더 많은 취약점을 유발하지 않는지 확인합니다.
5. 진행률이 표시되며 로그 결과를 보려면 **View log**를 클릭하십시오.
6. 프로젝트 추가가 완료됩니다.

{% hint style="info" %}
프로젝트 추가 중 오류가 발생하면 [Project import errors](https://support.snyk.io/hc/en-us/articles/360001373118)를 참조하십시오.
{% endhint %}

### 3단계: 취약점 보기

이제 프로젝트에 대한 취약점 결과를 확인할 수 있습니다. **Projects** 탭은 프로젝트 추가 후 기본적으로 나타나며 가져온 프로젝트의 취약점 정보를 표시합니다.

가져온 프로젝트를 확장하면 발견된 Issue 수와 심각도 수준별로 그룹화된 해당 프로젝트의 취약점 정보를 볼 수 있습니다.

![](<../../.gitbook/assets/view\_vulns\_\_overview (1).png>)

![](<../../.gitbook/assets/detailed-vuln-information (3) (4) (4) (4) (6) (7) (5) (1) (1) (1).png>)

자세한 내용은 [프로젝트 정보 보기](../../getting-started/introduction-to-snyk-projects/view-project-information/)를 참조하십시오.

### 4단계: 취약점 수정

Snyk은 일부 언어의 경우 pull/merge requests를 사용하여 취약점을 수정할 수 있습니다.

프로젝트의 **Issues**로 이동합니다.

![Screenshot\_2021-04-09\_at\_17.35.25.png](<../../.gitbook/assets/screenshot\_2021-04-09\_at\_17.35.25 (1).png>)

취약점을 수정하기 위해 다음과 같이 진행합니다.

1. **Fix this vulnerability**를 클릭하여 업그레이드(또는 패치)하여 개별 Issue를 해결하거나 **Fix these vulnerabilities**를 클릭하여 여러 Issue를 일괄 수정합니다.
2. **Open a Fix PR**이 나타나고 선택한 취약점이 표시됩니다.
3. 수정하려는 추가적인 Issue를 선택하거나 항목을 취소하여 수정 사항에서 제거할 수 있습니다.
4. 화면 하단의 **Open a Fix PR**을 클릭합니다.
5. Snyk이 PR을 실행하면 결과 화면이 나타납니다.
6. 추가적으로 **Files changed** 탭에서 변경 사항에 대한 세부 정보를 확인합니다.

![](<../../.gitbook/assets/screenshot\_2021-04-09\_at\_17.46.22 (1).png>)

자세한 내용은 [취약점 수정](broken-reference)을 참조하십시오.
