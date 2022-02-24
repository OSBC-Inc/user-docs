# DigitalOcean 통합을 이용한 컨테이너 보안

Snyk은 DigitalOcean과 통합하여 컨테이너 이미지를 가져와 취약점을 모니터링할 수 있습니다.

Snyk은 알려진 보안 취약점에 대해가져온 이미지(프로젝트)를 테스트하고 사용자가 제어하는 빈도로 테스트하고 새로운 문제를 감지하면 경고합니다.

DigitalOcean과의 통합은 모든 Snyk 사용자가 사용할 수 있습니다.

Snyk에서 DigitalOcean 통합을 설정하고 이미지 취약점 관리를 시작하려면 다음과 같이 진행합니다.

**전제 조건**

* Snyk에서 구성하려는 조직의 관리자여야 합니다.
* Snyk은 DigitalOcean과 통합하기 위해 사용자 자격 증명이 필요하며 SSO(Single Sign-On)용으로 구성한 경우 DigitalOcean을 지원하지 않습니다.

**통합 구성**

1. Snyk 계정 상단의 메뉴에서 Integrations로 이동합니다. 컨테이너 레지스트리 섹션에서 **DigitalOcean**을 찾아 클릭합니다.
2. **Account credentials** 섹션에서 DigitalOcean 개인 액세스 토큰을 로그인 자격 증명으로 입력하세요. 액세스 토큰을 만드는 자세한 사항은 Integrations 페이지에서 찾을 수 있습니다. 완료하려면 **Save**를 클릭하세요.

![](../../../../.gitbook/assets/mceclip0-10-.png)

자체 호스팅 DigitalOcean을 사용하는 경우 당사에 연락하여 토큰을 제공하세요. [이곳](../../integrate-self-hosted-container-registries/snyk-integration-to-self-hosted-container-registries.md)에서 비공개 레지스트리 통합 설정에 대한 자세한 내용을 찾을 수 있습니다.

{% hint style="info" %}
**Note**\
연결에 성공하려면 DigitalOcean에 저장소가 있는지 확인하세요.
{% endhint %}

Snyk은 연결 값을 테스트하고 페이지를 다시 로드하여 이제 DigitalOcean 통합 정보를 표시하고 **Add your DigitalOcean images to Snyk** 버튼을 사용할 수 있습니다. DigitalOcenan 연결에 실패한 경우 **Connected to DigitalOcean** 섹션 아래에 알림이 나타납니다.\
이제 Snyk을 사용하여 DigitalOcean에서 이미지를 스캔할 수 있습니다.
