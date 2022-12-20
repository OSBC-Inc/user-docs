# 프로젝트 수정 조언

## 취약점 수정

프로젝트의 간접 의존성에 대한 Snyk 지식을 통해 Snyk이 수정 조언을 쉽게 제공할 수 있습니다. Snyk은 두 가지 방법으로 취약점을 수정할 수 있습니다. Snyk은 직접 의존성을 취약점이 없는 버전으로 업그레이드하거나 취약점을 패치할 수 있습니다.

Snyk은 다음과 같은 워크플로우를 지원하여 개발자가 취약점을 수정할 수 있도록 지원합니다.

1. Snyk은 GitHub, GitLab 또는 Bitbucket PR 워크플로우를 사용하여 자동 Git PR(pull request)을 생성합니다. Snyk은 이 워크플로우를 밤에 실행합니다.
2. Snyk 사용자는 Snyk UI에서 _**Open a fix PR**_ 기능을 사용합니다.
3. Snyk 사용자는 Snyk UI의 특정 Issue 카드에서  _**fix this vulnerability**_ 기능을 사용합니다.

{% hint style="info" %}
이 워크숍에서는 **fix this vulnerability** 옵션을 사용합니다.
{% endhint %}

## 자동 Pull Request 생성

Snyk은 조직과 연결된 소스 제어 통합을 사용하여 프로젝트에 대한 자동 Pull Request를 생성합니다. 설정을 확인하려면 Snyk UI 상단의 Integration 탭을 선택하고 소스 제어 리포지토리를 선택합니다. Source Control의 톱니바퀴 아이콘을 클릭하고 설정을 검토합니다. 이 설정은 프로젝트별로 또는 전체 조직에 대해 구성할 수 있습니다.

{% hint style="info" %}
이 설정은 GitHub의 초기 구성에서 설정해야 합니다.
{% endhint %}

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/auto\_pr\_setting.png)

Snyk은 준비가 되면 프로젝트에 대한 PR을 발행할 것입니다. Git 저장소 상단의 Pull Request 탭을 선택하여 GitHub에서 PR을 볼 수 있습니다. GitLab과 Bitbucket은 유사한 보기를 가집니다. Snyk은 하룻밤 사이에 PR을 생성하고 여러 개의 PR이 서로 다른 의존성에 대해 존재합니다.

{% hint style="info" %}
SPC는 충분한 시간이 주어지면 PR을 생성합니다.
{% endhint %}

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/github\_pull\_req\_auto.png)

## fix PR 열기

Snyk UI는 프로젝트에서 직접 Pull Request를 생성하는 기능을 제공합니다. PR을 생성하려면 프로젝트 목록에서 SPC 프로젝트를 찾고 pom.xml 파일을 선택합니다.

Open a fix PR을 선택하면 Snyk이 워크플로우를 시작하여 SPC용 PR을 생성합니다. PR을 GitHub로 보내기 전에 Snyk UI에 의해 수정될 사항, 부분적인 수정 사항 및 수정되지 않을 모든 항목을 보여줍니다. GitHub에 PR을 보내고 GitHub 저장소 Pull Request 탭을 방문하여 Pull Request를 확인할 수 있습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/open\_pr.png)

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/open\_fix\_pr\_top\_half.png)

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/open\_fix\_pr\_bottom.png)

## Fix this vulnerability

Snyk의 _**fix this vulnerability**_ 워크플로우는 _**open a PR fix**_ 워크플로우와 동일합니다. PR 생성 시 아래와 같이 지정된 취약점 Issue만 PR에서 선택됩니다. XSS(Cross-site Scripting) 취약점을 찾아 PR 워크플로우를 시작합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/screen-shot-2020-08-22-at-12.32.44-pm.png)

Issue가 선택되었는지 확인하고 PR을 완료합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/screen-shot-2020-08-22-at-12.40.36-pm.png)
