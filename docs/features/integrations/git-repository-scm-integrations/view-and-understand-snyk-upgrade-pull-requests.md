# Snyk 업그레이드 pull 요청 보기 및 이해

수정 조언 외에도 Snyk은 스캔 결과를 기반으로 종속성을 업그레이드하기 위해 자동으로 pull request(PR)를 생성할 수 있습니다. Snyk은 현재 GitHub, GitHub Enterprise Server, BitBucket Cloud, GitLab 및 Azure repos를 통해 npm, Yarn, Maven-Central, NuGet(C#), Pip 및 PyPI(Python), Bundler(Ruby) 프로젝트에 대해 이 기능을 지원합니다.

브로커와 함께 사용하려면 관리자가 먼저 v4.55.0 이상으로 업그레이드해야 합니다.

{% hint style="info" %}
**주의**\
관리자 및 계정 소유자는 기능이 켜져 있는지(기본적으로 활성화됨) 어떤 조건에서 Snyk이 업그레이드 pull request를을 제출해야 하는지 구성하여 조직 및 프로젝트 수준 모두에서 Snyk 웹 UI에서 Snyk 업그레이드 pull request에 대한 설정을 관리합니다.
{% endhint %}

## 병합하기 전에 pull request 세부 정보 보기

Snyk이 귀하를 대신하여 업그레이드 풀 요청을 제출하면 관련 리포지토리에서 직접 풀 요청 및 모든 관련 세부 정보를 볼 수 있습니다.

끌어오기 요청을 빠르게 검토하려면 해당 위로 마우스를 가져가면 권장 업그레이드 및 기타 끌어오기 요청 요약 세부 정보를 볼 수 있습니다:

![](../../../.gitbook/assets/uuid-3683a529-6856-d15d-c49c-ca7ed318500d-en.png)

패키지 릴리스 정보 및 권장 업그레이드에 포함된 취약점을 포함한 심층적인 세부 정보를 보려면 pull request를 엽니다.

![](../../../.gitbook/assets/uuid-508983f5-8844-c19f-a43e-5a65e4ffdae9-en.png)

테이블에서 Issue 링크를 클릭하면 데이터베이스에서 직접 지정된 취약점에 대한 모든 세부 정보를 볼 수 있습니다.

pull request를 검토한 후 병합을 승인할 수 있습니다.
