# Snyk 라이선스 컴플라이언스 관리 시작하기

{% hint style="info" %}
**기능 지원 여부**\
단일 기본 라이선스 정책에 대한 기본 라이선스 정책 구성은 비즈니스 플랜에서 사용할 수 있습니다. 엔터프라이즈 플랜에서는 전체 정책 생성 및 관리가 가능합니다. 자세한 내용은 [pricing plans](https://snyk.io/plans/)를 참조하십시오.
{% endhint %}

[Snyk Open Source](https://docs.snyk.io/snyk-open-source/open-source-basics) 솔루션의 일부분이며 Snyk 라이선스 컴플라이언스 관리를 시작하여 코드의 [오픈 소스 라이선스 컴플라이언스](https://snyk.io/learn/open-source-licenses/)를 확인하십시오.

{% hint style="info" %}
이 프로세스는 Snyk UI 및 [지원 가능한 소스 코드 관리 시스템](../../../features/integrations/git-repository-scm-integrations/) 사용에 대해서 설명합니다.\
[IDE tool](https://docs.snyk.io/integrations/ide-tools) 또는 [CI/CD integration](https://docs.snyk.io/integrations/ci-cd-integrations)을 사용하거나 [Snyk CLI tool](https://docs.snyk.io/snyk-cli/guides-for-our-cli/getting-started-with-the-cli)을 사용하여 시작할 수 있습니다.
{% endhint %}

## 전제 조건



다음 사항이 존재하는지 확인하십시오.

* Snyk [유료 요금제](https://snyk.io/plans/).
* [Snyk Open Source](https://docs.snyk.io/getting-started/getting-started-snyk-products/getting-started-snyk-open-source)가이드에 맞게 프로젝트를 통합 및 설치

## **1**단계: 정책 정의

라이선스 Issue를 기반으로 조치를 취하려면 라이선스 유형에 따른 정책을 정의해야 합니다. 정책은 조직 내에서 다양한 요구 사항을 제공합니다. 법무팀과 협력하여 회사의 특정한 정책을 만드십시오.

### 정책 규칙 만들기

각 정책에는 라이선스 위반의 심각성을 나타내는 심각도 수준과 함께 허용되는 라이선스와 사용이 금지된 라이선스를 자세히 설명하는 규칙이 포함되어 있습니다. 예를 들어 내부의 전용 라이선스 Issue의 심각도 수준은 외부에서 릴리스된 Issue보다 심각도 수준이 낮을 수 있습니다.

![](../../../.gitbook/assets/license-policy.png)

[Licenses overview](https://docs.snyk.io/snyk-open-source/licenses) 및 [Setting a license policy](https://docs.snyk.io/snyk-open-source/license-policies/setting-a-license-policy)를 참조하십시오.

## 2단계: 문제 확인

Snyk의 [Git 기반 통합](https://support.snyk.io/hc/en-us/sections/360001138098-Git-repository-SCM-integrations)은 일반 워크플로우의 일부로 라이선스 스캔을 지원합니다. 스캔을 진행하는 동안 라이선스 Issue는 **Issues** 탭에 필터링 가능한 목록으로 나타납니다.

![](<../../../.gitbook/assets/image3 (1).png>)

해당 예는 GPL-2.0 라이선스의 대한 심각도가 높은 Issue와 해당 라이선스에 대한 정책에 정의된 지침을 보여줍니다.

**snyk test**를 실행한 후 Snyk CLI를 사용하여 라이선스 Issue를 볼 수도 있습니다.

![](../../../.gitbook/assets/image2-1-.png)

**디펜던시 확인**

Snyk은 어떠한 디펜던시가 라이선스 Issue를 야기했는지 확인하기 위해 전체 디펜던시 트리에서 직접 및 전이 의존성의 라이선스 Issue를 제공합니다.

![](<../../../.gitbook/assets/image4 (1).png>)

해당 예는 다음과 같은 원인으로 인해 발생하는 두 가지 높은 심각도 라이선스 정책 위반이 존재합니다.

* **wicket@1.3.5** npm 패키지에 대한 직접적인 의존성
* **web-project-starter@0.0.3**에 의해 도입된 **flickity@2.2.1** 패키지에 대한 간접적인 의존성

**목록 및 저작권 확인**

사용 중인 라이선스의 세부 목록을 확인하고 공유할 수 있으며 모든 오픈 소스 구성 요소 및 라이선스가 저작권 정보와 함께 나열되는 보고서를 확인할 수 있습니다.

![](../../../.gitbook/assets/copyright.png)

## **3**단계: 프로세스 문제

스캔 중에 식별된 라이선스 Issue를 해결하기 위한 조치를 취하여 해결되지 않은 라이선스 Issue 없이 애플리케이션을 구축하고 배포할 수 있습니다.

수행하는 작업은 라이선스 조건과 정책에 따라 다릅니다. 예를 들어 라이선스 위반이 발견된 경우 법무팀에 연락하거나 위반이 발견된 디펜던시를 교체하여 이 Issue를 해결할 수 있습니다.

## 추가 정보

[라이선스](./)를 참조하십시오.
