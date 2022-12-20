# 사용 페이지 세부정보

settings ![](../../../.gitbook/assets/cog\_icon.png) > **Usage**를 클릭하여 다음을 포함한 Snyk 사용 세부 정보를 봅니다:

* 사용된 테스트 수입니다.
* 프로젝트에 기여한 개발자의 수입니다.
* 프로젝트 테스트 사용 설정.

### 테스트 사용

**Test Usage** 섹션은 현재 청구 기간 동안 사용 중인 테스트 수를 보여줍니다:

![](../../../.gitbook/assets/test-usage.png)

{% hint style="info" %}
테스트 제한은 Snyk 제품 및 계획에 따라 다릅니다. 자세한 내용은 [요금제 페이지](https://snyk.io/plans/)를 참조하십시오.
{% endhint %}

{% hint style="info" %}
Snyk이 테스트를 계산하는 방법에 대한 자세한 내용은 [테스트로 간주되는 항목](https://support.snyk.io/hc/en-us/articles/360000925418-What-counts-as-a-test-)을 참조하세요.
{% endhint %}

### 기여하는 개발자

{% hint style="info" %}
현재 개발자 수가 있는 통합은 GitHub, GitHub Enterprise, GitLab 및 Snyk CLI입니다.
{% endhint %}

Snyk은 기여 개발자를 지난 90일 동안 Snyk이 모니터링하는 비공개 저장소에 커밋한 개발자로 정의합니다.

**Contributing developers for Git and CLI integrations** 섹션은 조직 수준과 그룹 수준 모두에서 기여하는 개발자 수를 보여줍니다.

개수는 통합과 연결된 개인 저장소의 기본 분기에 기여하는 개발자의 수를 나타냅니다.

가격 모델이 비공개 리포지토리에 기여하는 개발자 수를 기반으로 하기 때문에 현재 공개(오픈 소스) 리포지토리에 대한 기여를 계산하지 않습니다.

예를 들어:

![](../../../.gitbook/assets/image\_\_10\_.png)

**모든 통합 수의 총 고유 기여자는 Snyk 계정의 모든 통합에 대한 기여자** 수를 보여줍니다. 기여한 개발자는 여러 통합 또는 여러 저장소에 기여한 경우에도 한 번만 계산됩니다.

**Breakdown by integration** 섹션에는 해당 통합의 기여자, 조직 및 저장소 수가 표시됩니다.

#### **기여자 이메일**

각 기여자는 개발자 컴퓨터의 로컬 git 구성 내에서 설정된 작성자 이메일 필드로 계산됩니다.

### 프로젝트

**Projects** 섹션에는 프로젝트에 대한 테스트 사용 설정이 표시됩니다.

**일괄 작업**

**일괄 작업**의 경우 관련 프로젝트를 선택한 다음 선택한 프로젝트를 **Delete**, **Activate** 또는 **Deactivate**하도록 선택합니다.

![](../../../.gitbook/assets/usage-projects-bulk-actions.png)

**테스트 빈도 설정**

각 프로젝트에 대한 테스트 빈도를 설정할 수 있습니다.

각 항목에 대해 해당 프로젝트의 테스트 빈도를 선택할 수 있습니다(안함, 매일 또는 매주).

![](../../../.gitbook/assets/usage-projects-single.png)

테스트하지 않으려면 **Deactivate**를 클릭하고 웹훅을 제거하고 보고에 프로젝트 결과 표시를 중지합니다.
