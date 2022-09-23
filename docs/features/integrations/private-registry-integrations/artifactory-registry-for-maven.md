# Maven용 Artifactory Registry

{% hint style="info" %}
**기능 가용성**

이 기능은 엔터프라이즈 플랜에서 사용할 수 있습니다. 자세한 내용은 [요금제](https://snyk.io/plans/)를 참조하세요.
{% endhint %}

Snyk은 Maven 프로젝트에서 커스텀 Artifactory Package Repositories를 사용할 수 있습니다.

이를 통해 Snyk는 사용자 지정 레지스트리에서 호스팅되는 패키지의 모든 직접적 및 전이적 종속성을 해결하고 보다 완전하고 정확한 종속성 그래프 및 관련 취약성을 계산할 수 있습니다.

Maven 프로젝트는 사용자 정의 패키지 저장소를 통해 모든 요청을 미러링하도록 구성하거나 Maven Central과 함께 사용할 추가 저장소를 지정할 수 있습니다.

## 사용자 정의 Maven 패키지 레지스트리 설정

사용자 지정 레지스트리에 액세스하는 데 인증이 필요한 경우 먼저 Artifactory 패키지 저장소 통합을 구성해야 합니다. [Artifactory Registry 설정](artifactory-registry-setup.md)을 참조하십시오.

통합이 설정되면 settings ![](../../../.gitbook/assets/cog\_icon.png) **> Languages > Java**로 이동하여 Maven 설정을 구성할 수 있습니다.

Artifactory를 미러로 사용할지 아니면 아티팩트가 상주할 추가 저장소로 사용할지 선택할 수 있습니다. 이 설정은 `~/.m2/settings.xml`에 있는 것과 매우 유사합니다.

### **Mirrors**

**Direct** 또는 인증 **통합**을 사용하는 경우 유형 값을 선택합니다.

**Direct**를 사용하는 경우 **URL**, **저장소 이름** 및 **Mirror off**를 완료해야 합니다.

**Mirror of** 값은 `*`가 되어 모든 것을 미러링하거나 `central`과 같은 값을 입력할 수 있습니다.

![](../../../.gitbook/assets/uuid-fd027725-33b3-7f12-a921-d7fba9cedad8-en.png)

Type **Integration**을 사용하는 경우 통합 유형을 선택하고 **Repository Name** 및 **Mirror of**의 세부 정보를 제공해야 합니다.

**Repository Name**은 내부 저장소 URL에서 `artifactory/` 뒤에 오는 대로 설정해야 합니다.

예를 들어 URL이 `http://artifactory.company.io/artifactory/libs-release`인 경우 **Repository Name**은 `libs-release`로 설정해야 합니다.

![](../../../.gitbook/assets/uuid-293cfd2b-2cd5-b8a3-0671-bf6d2798a3bc-en.png)

### **저장소**

또는 아티팩트를 확인하기 위한 추가 위치로 사용할 저장소를 구성할 수 있습니다.

저장소는 [미러](artifactory-registry-for-maven.md#mirrors)와 동일한 방식으로 구성되지만 미러 대상은 필요하지 않습니다.
