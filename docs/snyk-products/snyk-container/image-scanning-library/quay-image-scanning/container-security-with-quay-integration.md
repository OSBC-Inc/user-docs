# Quay 통합을 이용한 컨테이너 보안

Snyk은 Quay Container Registry와 통합하여 컨테이너 이미지를 가져오고 취약점을 모니터링할 수 있습니다.

Snyk은 가져온 이미지(프로젝트)에 알려진 보안 취약점이 존재하는지 테스트하여 사용자가 설정한 빈도로 테스트하고 새로운 Issue가 감지되면 사용자에게 알려줍니다.

Quay 통합은 모든 Snyk 사용자가 사용할 수 있습니다.

Snyk에서 Quay 통합을 설정하고 이미지 취약점 관리를 시작하려면 다음과 같이 진행합니다.

**전제 조건**

* Snyk에서 구성할 조직의 관리자여야 합니다.
* Snyk은 Quay와 통합하려면 사용자 인증 정보가 필요하며 SSO(Single Sign-On)용으로 구성한 경우 Quay를 지원하지 않습니다.

**통합 구성**

1. Snyk 계정 상단에 있는 메뉴 모음에서 **Integrations** 으로 이동합니다. **Container Registries** 섹션에 **Quay** 옵션을 찾아 클릭합니다.
2. **Account credentials** 섹션에서 Quay 사용자 이름과 암호 로그인 자격 증명을 입력합니다. **container registry name**에 통합할 레지스트리의 전체 URL을 입력합니다. 클라우드 기반 Quay 또는 개인 호스트일 수 있습니다. 마치려면 **Save**를 클릭하세요.

![](../../../../.gitbook/assets/mceclip1-10-.png)

자체 호스팅된 Quay 레지스트리를 사용하는 경우 [당사 지원 팀](https://support.snyk.io/hc/en-us/requests/new)에 문의 바랍니다. 개인 레지스트리 통합 설정에 대한 자세한 내용은 [여기](../../integrate-self-hosted-container-registries/snyk-integration-to-self-hosted-container-registries.md)를 참조하십시오.

{% hint style="info" %}
**Note**\
[Quay.io](http://quay.io)는 2021년 6월까지 Quay 사용을 [중지](https://access.redhat.com/articles/5925591)하고 있습니다. 자격 증명은 더이상 Quay 사용자 이름과 비밀번호가 아니라 원하는 repo\*\*.\*\*에 대해 'read' 권한이 있는 Quay 로봇 계정 자격 증명(사용자 이름 및 토큰)이 될수 있습니다.
{% endhint %}

Snyk은 연결 값과 page reload를 테스트하여 Quay 통합 정보를 표시하고 **Add your Quay images to Snyk** 버튼을 사용할 수 있습니다. Quay와의 연결에 실패한 경우 **Connected to Quay** 섹션 아래에 알림이 나타납니다. 이제 Snyk을 사용하여 Quay에서 이미지를 스캔할 수 있습니다.
