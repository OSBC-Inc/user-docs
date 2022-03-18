# Nexus 통합을 이용한 컨테이너 보안

{% hint style="info" %}
**기능 사용 여부**\
이 기능은 모든 유료 플랜에서 사용할 수 있습니다. 자세한 내용은 [pricing plans](https://snyk.io/plans/)를 참조하십시오.
{% endhint %}

Snyk은 Nexus Container Registry와 통합하여 컨테이너 이미지를 가져오고 취약점을 모니터링할 수 있습니다.

Snyk은 가져온 이미지(프로젝트)에 알려진 보안 취약점이 존재하는지 테스트하여 사용자가 제어하는 빈도로 테스트하고 새로운 이슈가 감지되면 사용자에게 알려줍니다.

Snyk에서 Nexus 통합을 설정하고 이미지 취약점 관리를 시작하려면 다음과 같이 진행합니다.

**전제 조건**

* Snyk에서 구성할 조직의 관리자여야 합니다.
* Snyk은 Nexus와 통합하려면 사용자 자격 증명이 필요하며 SSO(Single Sign-On)용으로 구성한 경우 Nexus를 지원하지 않습니다.

**통합 구성**

* Snyk 계정 상단의 메뉴 모음에서 **Integrations**로 이동합니다. **Under the Container Registries section**에서 Nexus 옵션을 찾아 클릭합니다.
* **Account credentials** 섹션에서 Nexus 사용자 이름과 암호 로그인 자격 증명을 입력합니다. **container registry name**에 통합할 레지스트리의 전체 URL을 입력합니다. 마치려면 **Save**를 클릭합니다.

![](../../../../.gitbook/assets/mceclip0-9-.png)

![](../../../../.gitbook/assets/mceclip1-20-.png)

자체 호스팅된 Nexus 레지스트리를 사용하는 경우 [당사 지원 팀](https://support.snyk.io/hc/en-us/requests/new)에 문의 바랍니다. 개인 레지스트리 통합 설정에 대한 자세한 내용은 [여기](../../integrate-self-hosted-container-registries/snyk-integration-to-self-hosted-container-registries.md)를 참조하십시오.

Snyk는 연결 값과 page reload를 테스트하여 Nexus 통합 정보를 표시하고 **Add your Nexus images to Snyk** 버튼을 사용할 수 있습니다. Nexus에 연결하지 못한 경우 **Connected to Nexus** 섹션 아래에 알림이 나타납니다.

이제 Snyk를 사용하여 Nexus에서 이미지를 스캔할 수 있습니다.
