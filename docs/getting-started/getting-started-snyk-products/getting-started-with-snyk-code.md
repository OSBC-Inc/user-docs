# Snyk Code 사용하기

[Snyk Code](https://snyk.io/product/snyk-code/)를 사용하여 코드에서 잠재적인 취약점을 찾아 우선순위를 지정하고 수정할 수 있습니다.

{% hint style="info" %}
이 문서에는 웹 UI와 함께 Snyk Code를 사용하는 방법에 대해 설명합니다. Snyk Code를 JetBrains IDE 플러그인으로도 사용할 수 있습니다. 자세한 내용은 [JetBrains IDE Plugins](https://docs.snyk.io/integrations/ide-tools/jetbrains-plugins)를 참조하세요.
{% endhint %}

## 전제 조건

* Snyk 계정
* [Snyk Open Source](https://docs.snyk.io/snyk-open-source) 또는 [Snyk Container](https://docs.snyk.io/snyk-container) 설치(현재 Snyk Code는 애드온으로 배포).
* [지원되는 언어](../../products/snyk-code/snyk-code-language-and-framework-support.md)로 된 코드를 포함하는 프로젝트.
* 지원되는 소스 코드 관리 시스템(SCMs) 중 하나 필요: GitHub, GitHub Enterprise, Bitbucket Cloud, Bitbucket Server, GitLab Cloud, Azure Repos.

## 1단계: Snyk Code 활성화

Snyk Code는 기본적으로 비활성화되어 있으므로 각 조직 설정에서 활성화해야 합니다.

1. [Snyk.io](http://snyk.io)에 로그인합니다.
2. settings ![](../../.gitbook/assets/cog\_icon.png) > **Snyk Code** 클릭
3. **Enable Snyk Code**에서 **Disabled**를 **Enabled**로 변경합니다.
4. **Save changes**를 클릭 합니다.

## 2단계: 소스 제어 통합 추가

{% hint style="info" %}
이미 설정을 완료한 경우 해당 단계를 건너뛸 수 있습니다.
{% endhint %}

Snyk에서 프로젝트를 작업할 수 있도록 소스 코드 통합을 진행합니다.

1. [Snyk.io](http://snyk.io)에 로그인 합니다.
2. **Integrations > Source control**을 선택 합니다.
3. Snyk과 통합할 소스 제어 시스템(예: Github)을 클릭합니다.
4. Snyk 액세스 권한을 부여하려면 계정 자격 증명을 진행하거나 Github에서 인증을 진행합니다.

Snyk Code는 코드 분석을 위해 임시로 저장소를 복제합니다. 이를 위해서는 SCM에 대한 적절한 권한과 HTTPS 액세스가 필요합니다.

데이터 저장 방법에 대한 자세한 내용은 [How Snyk handles your data](../../more-info/how-snyk-handles-your-data.md)를 참조하세요. 통합에 대한 자세한 내용은 [DevOps integrations & languages](https://docs.snyk.io/introducing-snyk/introduction-to-snyk/integrations-and-languages)를 참조하세요.

## 3단계: 프로젝트 추가

{% hint style="info" %}
이미 추가된 프로젝트가 있는 경우 이 단계를 건너뛸 수 있습니다.
{% endhint %}

Snyk이 테스트하고 모니터링할 저장소를 선택하여 프로젝트를 추가합니다.

1. [snyk.io](http://snyk.io)에서 **Projects**를 선택합니다.
2. 프로젝트를 추가할 도구를 선택하세요(예: Github).
3. **Personal and Organization repositories**에서 사용할 저장소를 선택합니다.
4. **Add selected repositories**를 클릭하여 선택한 저장소의 프로젝트를 추가합니다. 이 경우 Snyk이 코드 취약점에 대한 정기 검사를 실행하도록 설정합니다.
5. 진행률이 표시됩니다. 로그 결과를 보려면 **View log**를 클릭하세요.
6. 프로젝트 추가가 완료됩니다.

{% hint style="info" %}
현재 Snyk Code는 **폴더 제외 옵션**을 지원하지 않습니다. 더 많은 정보가 필요하면 저희에게 연락 부탁 드립니다.
{% endhint %}

자세한 내용은 [Snyk projects](https://support.snyk.io/hc/en-us/sections/360004724958-Snyk-projects)를 참조하세요.

## 4단계: 취약점 확인

추가된 프로젝트에 대한 취약점 결과를 확인할 수 있습니다. **Projects** 탭은 추가 후에 기본적으로 나타나며 해당 프로젝트에 대한 취약점 정보를 제공합니다.

1. 추가된 프로젝트를 클릭하면 발견된 취약점 수를 포함하여 해당 프로젝트에 대한 취약점 정보를 심각도별로 그룹화 하여 볼 수 있습니다.
2. 항목을 클릭하여 해당 항목에 대한 취약점을 확인할 수 있습니다. 각 취약점에 대해 악용 가능한 코드와 수정하지 않을 경우 취약점으로 이어질 수 있는 코드에 대한 설명을 제공합니다.

![](../../.gitbook/assets/view-vulns2.png)

자세한 내용은 [View project information](https://docs.snyk.io/getting-started/introduction-to-snyk-projects/view-project-information)을 참조하세요.

## 5단계: 취약점 세부 정보 확인

취약점에 대한 자세한 내용을 확인하려면 **Full Details**를 클릭합니다.

* **Data Flow**: 소스(사용자 입력)에서 싱크(정확한 입력을 수신해야 하며 그렇지 않으면 악용될 수 있는 작업)로의 흐름을 나타냅니다.
* **Fix Strategy**: 취약점에 대한 자세한 내용, 참조 및 코드 샘플을 제공하여 취약점을 수정하는 방법을 제공합니다.

## 추가 내용

* [Snyk Code](https://docs.snyk.io/snyk-code)
* [Developer-first SAST with Snyk Code](https://snyk.io/blog/developer-first-sast-with-snyk-code/)
* [SAST vs DAST](https://snyk.io/learn/sast-vs-dast/)
