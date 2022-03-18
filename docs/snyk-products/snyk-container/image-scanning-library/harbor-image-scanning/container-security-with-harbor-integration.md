# Harbor 통합을 이용한 컨테이너 보안

{% hint style="info" %}
**사용 가능 여부**\
이 기능은 Enterprise Plan에서 사용할 수 있습니다. 자세한 내용은 [pricing plans](https://snyk.io/plans/)을 참조하십시오.
{% endhint %}

Snyk은 Harbor Container Registry와 통합하여 컨테이너 이미지를 가져오고 취약점을 모니터링할 수 있습니다.

Snyk은 가져온 이미지(프로젝트)에 알려진 보안 취약점이 존재하는지 테스트하여 사용자가 제어하는 빈도로 테스트하고 새로운 이슈가 감지되면 사용자에게 알려줍니다.

Snyk에서 Harbor 통합을 설정하고 이미지 취약점 관리를 시작하려면 다음과 같이 진행합니다.

**전제 조건**

* Snyk에서 구성할 조직의 관리자여야 합니다.
* Snyk은 Harbor와 통합하려면 사용자 자격 증명이 필요하며 SSO(Single Sign-On)용으로 구성된 경우 Harbor를 지원하지 않습니다.

**통합 구성**

1. Snyk 계정으로 로그인한 후 상단의 메뉴 모음에서 **Integrations** 으로 이동합니다. **Container Registries** 섹션에서 Harbor 옵션을 찾아 클릭합니다.
2. **Account credentials** 섹션에서 Harbor 사용자 이름 및 암호 로그인 자격 증명을 입력합니다. **container registry name** 에 통합할 레지스트리의 전체 URL을 입력합니다. 마치려면 **Save**를 클릭하세요.

자체 호스팅된 Harbor Registry를 사용하는 경우 [당사 지원 팀](https://support.snyk.io/hc/en-us/requests/new)에 문의 바랍니다. 개인 레지스트리 통합 설정에 대한 자세한 내용은 [문서](../../integrate-self-hosted-container-registries/snyk-integration-to-self-hosted-container-registries.md)를 참조하십시오.

![](../../../../.gitbook/assets/mceclip2-1-.png)

{% hint style="info" %}
**Note**\
통합을 설정하려면 Harbor 사용자가 관리자여야 합니다. 현재 /v2/\_catalog endpoint를 사용하여 저장소를 나열합니다. 관리자 권한을 가진 사용자만 이 엔드포인트를 사용할 수 있는 [해결되지 않은 문제가 Harbor에 있습니다.](https://github.com/goharbor/harbor/issues/6784)
{% endhint %}

![](../../../../.gitbook/assets/mceclip1-8-.png)

Snyk은 연결 값과 page reload를 테스트하여 Harbor 통합 정보를 표시하고 **Add your Harbor images to Snyk** 버튼을 사용할 수 있습니다. Harbor에 연결하지 못한 경우 **Connected to Harbor** 섹션 아래에 알림이 나타납니다.\
이제 Snyk을 사용하여 Harbor에서 이미지를 스캔할 수 있습니다.
