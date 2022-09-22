# Jira

{% hint style="info" %}
**기능 가용성**

기능 가용성 이 기능은 모든 유료 플랜에서 사용할 수 있습니다. 자세한 내용은 [pricing plans](https://snyk.io/plans/)를 참조하세요. Snyk Infrastructure as Code에 대한 이 기능의 가용성은 \
[jira-integration.md](../../../products/snyk-infrastructure-as-code/jira-integration.md "mention")를 참조하십시오.
{% endhint %}

## Jira 통합 설정

Jira 통합을 통해 Snyk UI에서 취약성 또는 라이선스 문제에 대한 Jira 문제를 수동으로 제기할 수 있으며 API도 포함됩니다. ([API 문서 참조](https://snyk.docs.apiary.io/#reference/projects/project-jira-issues)).

{% hint style="info" %}
주의\
Jira 인스턴스가 비공개인 경우 Snyk Broker로 설정한 다음 중개된 Jira 설정 지침을 따라야 합니다.
{% endhint %}

## 전제 조건

Snyk에는 Jira 버전 5 이상이 필요합니다.\
["Browse Projects"  "Create Issues"](https://community.atlassian.com/t5/Answers-Developer-Questions/Projects-are-not-being-returned-by-a-REST-API-call-to-createmeta/qaq-p/522042#M59700) 권한이 필요합니다.

## Jira 통합을 설정하는 방법

Snyk 계정을 Jira 계정에 연결하려면 조직 설정의 통합 페이지로 이동하여 자격 증명을 입력합니다. 이를 위해 기존 자격 증명을 사용하는 것보다 Jira에서 새 사용자를 설정하는 것이 좋습니다. 사용자 이름과 비밀번호로 인증할 수 있지만 [Atlassian API tokens](https://id.atlassian.com/manage/api-tokens)에서 생성할 수 있는 API 토큰으로 인증하는 것이 좋습니다.

## **Jira Issue 만들기**

연결을 설정했으면 Snyk 프로젝트 중 하나를 방문하십시오. 이제 각 취약점 및 라이선스 발급 카드 하단에 Jira Issue를 생성할 수 있는 새로운 버튼이 표시됩니다.

![](../../../.gitbook/assets/uuid-07abf9db-45cb-cdcd-537b-328a0c4b891e-en.png)

이것을 클릭하면 관련 필드에 복사된 Snyk 문제 세부 정보와 함께 Jira Issue 생성 양식이 나타납니다. Issue를 만들기 전에 이를 검토하고 편집할 수 있습니다.

Issue를 보낼 Jira 프로젝트를 선택합니다. 아래에 표시되는 필드는 프로젝트에 있는 필드를 기반으로 하므로 프로젝트 간에 전환하면 다른 옵션이 표시될 수 있습니다.

**Note**\
Snyk은 현재 non-Epic Jira 티켓 생성을 지원합니다. Epic은 일단 생성되면 티켓에 수동으로 추가해야 합니다.

![](../../../.gitbook/assets/uuid-67202f8e-7f70-1e84-6044-f65ec36138b3-en.png)

Jira Issue를 생성하면 링크가 있는 Jira 키가 Issue 카드에 표시됩니다. Jira API를 사용하는 경우 Snyk에서 동일한 Issue에 대해 여러 Jira Issue를 생성할 수 있습니다.

![](../../../.gitbook/assets/uuid-5283ddbe-913b-1aa1-ec74-e384b0e2929b-en.png)

보고서의 Issue 보기에서 생성된 Jira Issue도 확인할 수 있습니다.

![](../../../.gitbook/assets/uuid-cd4e8cae-2528-a922-5a03-5f23c42d4ac2-en.png)

## 또한 참조하십시오:

[Enable permissions for Snyk Broker from your third-party tool](https://docs.snyk.io/integrations/snyk-broker/enable-permissions-for-snyk-broker-from-your-third-party-tool)
