# npm Teams & npm Enterprise

## **Overview**

{% hint style="info" %}
**기능 가용성**

이 기능은 엔터프라이즈 플랜에서 사용할 수 있습니다. 자세한 내용은 [요금제](https://snyk.io/plans/)를 참조하세요.
{% endhint %}

Snyk은 npm 및 Yarn 프로젝트와 함께 사용자 지정 npm Teams 및 npm Enterprise 리포지토리를 사용할 수 있습니다.

이를 통해 Snyk은 사용자 지정 레지스트리에서 호스팅되는 패키지의 모든 직접적 및 전이적 종속성을 해결하고 보다 완전하고 정확한 종속성 그래프 및 관련 취약성을 계산할 수 있습니다.

구성되면 Snyk은 이 정보를 사용하여 풀/병합 요청을 생성할 때 **,** npm 및 yarn이 잠금 파일을 재생성하기 위해 해당 dep에 도달하도록 허용하여 개인 종속성에 액세스합니다.

개인 npm Teams 및 npm Enterprise Node.js 패키지가 호스팅되는 위치와 해당 패키지의 범위를 Snyk에 알려주는 구성을 추가할 수 있습니다.

이것은 일반적으로 `.yarnrc` 또는 `.npmrc`에 추가하는 것과 동일한 정보입니다.

{% hint style="info" %}
**Note**\
이 가이드는 Snyk UI 통합에만 해당되며 CLI는 이미 private npm Teams 및 npm Enterprise 레지스트리가 있는 yarn 및 npm 프로젝트를 지원합니다.
{% endhint %}

## JavaScript 언어 설정

1. settings ![](../../../.gitbook/assets/cog\_icon.png) **> Languages > JavaScript**로 이동하고 프로젝트 유형에 따라 npm 또는 yarn 설정(아래 스크린샷에 표시된 yarn)으로 이동합니다.
2. 이전에 npm Teams 또는 npm Enterprise에 연결하지 않은 경우 먼저 통합을 구성하라는 메시지가 표시됩니다. 아래의 [npm Teams 및 npm Enterprise Registry 설정](npm-teams-and-npm-enterprise-for-npms.md#npm-teams-and-npm-enterprise-registry-settings)을 참조하세요.
3. 통합을 설정했으면 **Add registry configuration**를 선택합니다.
   1. 패키지 소스로 "npm"을 선택하십시오.
   2. 이 레지스트리를 **기본 레지스트리 URL**로 구성하려면 범위를 비워 둡니다.
   3. **범위가 지정된 패키지만** 이 레지스트리를 사용하도록 구성하려면 범위를 추가하십시오.
   4. **기본 레지스트리 URL**과 **범위가 지정된 패키지**를 혼합하여 추가하려면 기본 및 범위당 하나씩 여러 구성을 추가하십시오.
4. 원하는 레지스트리와 범위를 모두 추가했으면 **Update settings**를 클릭합니다.
5. 이제 테스트해 보세요. 비공개 종속성이 포함된 프로젝트에서 끌어오기/병합 요청을 열어 잠금 파일이 업데이트되고 이전에 생성되지 않은 Snyk 수정 끌어오기 요청에 포함되었는지 확인합니다.

![](<../../../.gitbook/assets/image (34) (1).png>)

## npm Teams & npm Enterprise Registry 설정

npm Teams 및 npm Enterprise 통합에 대한 토큰 기반 인증을 구성할 수 있습니다.

## 시작하기

1. settings ![](../../../.gitbook/assets/cog\_icon.png) > **Integrations > Package Repositories > npm**로 이동합니다.
2. 처음에 **Credentials** 화면이 표시되어야 합니다(아래 참조).
3. **Public URL** 및 **Token** 값을 입력합니다.
4. **Save**를 클릭합니다.

![](<../../../.gitbook/assets/image (35).png>)
