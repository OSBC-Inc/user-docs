# Docker Hub 통합 설정

## Docker Hub에 대한 통합 설정

Docker Hub와 Snyk 간의 통합을 활성화하고 취약점 관리를 시작합니다.

1. Snyk UI에서 계정에 로그인하고 상단의 메뉴 모음에서 Integrations로 이동합니다.
2. Integrations 페이지에서 Docker Hub를 클릭합니다.
3. Integrations 영역의 **Settings** 페이지에서 Docker Hub 사용자 이름과 액세스 토큰을 입력한 다음 **Save**를 클릭합니다.

![](<../../../.gitbook/assets/dockerhub1 (1).png>) ![](<../../../.gitbook/assets/dockerhub2 (1).png>)

__[_액세스 토큰_](https://docs.docker.com/docker-hub/access-tokens/)으로 DockerHub 암호를 사용하거나 DockerHub에서 만든 액세스 토큰을 사용할 수 있습니다. 계정에서 2FA가 활성화된 경우 액세스 토큰만 적용됩니다.

Snyk은 연결 값을 테스트하고 페이지를 다시 로드하여 이제 Docker Hub 통합 정보와 Docker Hub 이미지를 Snyk에 추가할 수 있도록 버튼이 표시됩니다.

세부 정보가 저장되었다는 확인 메시지가 화면 상단에 녹색으로 나타납니다. 또한 Docker Hub에 연결하지 못한 경우 알림이 나타납니다.
