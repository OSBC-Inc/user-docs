# Docker Hub 통합 구성

Docker Hub와 Snyk 간의 통합을 활성화하고 취약점 관리를 시작합니다.

1. **Integrations**로 이동합니다.
2. **Docker Hub**를 클릭합니다.
3. Docker Hub 사용자 이름과 액세스 토큰을 입력하세요(토큰을 생성하려면 아래 참조).
4. **Save**를 클릭하면 페이지가 새로운 선택사항과 함께 다시 로드되고 액세스토큰 필드가 공백으로 표시됩니다. 이는 정상적인 상황입니다.
5. 세부 정보가 저장되었다는 확인 메시지도 화면 상단에 녹색으로 표시됩니다.

![성공적인 연결 예시](<../../../../.gitbook/assets/Configure integration for Docker Hub-1.png>)

#### 연결 실패

Docker Hub에 연결하지 못한 경우 오류 알림이 나타납니다.

![실패한 연결 예시: "Could not connect to Docker Hub".](<../../../../.gitbook/assets/Configure integration for Docker Hub-2.png>)

### Docker Hub 통합 문제 해결

프로젝트 가져오기 실패, 연결 실패, 오류 표시 누락 등 Docker Hub 통합 문제를 해결 하는 첫번째 방법은 새로운 액세스 토큰을 생성하고 Snyk 설정 페이지에서 Docker Hub 통합을 다시 설정합니다.

Docker Hub 액세스 토큰을 다시 생성하려면 다음과 같이 진행합니다.

1. [https://hub.docker.com/settings/security](https://hub.docker.com/settings/security)로 이동합니다.
2. 새로운 액세스 토큰을 선택하십시오.
3. 액세스 토큰 설명을 입력하고 권한을 설정한 다음 Generate를 클릭합니다.액세스 토큰을 복사하고 위 1단계에서 사용자 이름과 함께 사용합니다.
4. 액세스 토큰은 복사합니다. 위의 1단계에서 사용자 이름과 함께 사용합니다.

DockerHub 액세스 토큰에 대한 자세한 내용은 [Docker Hub Access Tokens](https://docs.docker.com/docker-hub/access-tokens/)를 참조하십시오.
