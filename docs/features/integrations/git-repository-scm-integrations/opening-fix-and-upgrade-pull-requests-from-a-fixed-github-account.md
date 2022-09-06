# 고정된 GitHub 계정에서 수정 및 업그레이드 pull request 열기

Snyk에서 임의로 선택한 GitHub 사용자 계정을 사용하는 대신 특정 GitHub 계정을 설정하여 수정 사항을 열고 PR을 업그레이드할 수 있습니다.

{% hint style="info" %}
일일/주간 테스트와 같이 UI에서 수행하지 않는 다른 작업은 여전히 무작위로 선택된 Snyk에 GitHub 계정을 연결한 Snyk 조직 구성원이 수행합니다.
{% endhint %}

이 기능을 사용하려면:

1. settings ![](../../../.gitbook/assets/cog\_icon.png) 클릭 > **Integrations**.
2. GitHub 항목의 경우 **Edit Settings**를 클릭합니다.
3. **Open fix and upgrade pull requests from a fixed GitHub account** 아래에서 토글 버튼을 활성화합니다.
4. GitHub에서 개인 액세스 토큰을 생성하기 위한 페이지 내 지침을 따르십시오.
5. 새로 생성된 토큰을 Snyk에 제공하여 GitHub에서 작업(예: Fix PR 열기)을 수행하는 데 사용할 수 있습니다.

{% hint style="info" %}
토큰이 제공되는 GitHub 계정에 Snyk로 모니터링하려는 저장소에 대한 쓰기 수준 이상의 권한이 있는지 확인하십시오.
{% endhint %}

GitHub의 리포지토리 권한 수준에 대해 [자세히](github-integration.md) 알아보세요.
