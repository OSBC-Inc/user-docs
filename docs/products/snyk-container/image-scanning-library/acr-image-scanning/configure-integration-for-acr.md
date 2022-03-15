# ACR 통합 구성

ACR 레지스트리와 Snyk 조직 간의 통합을 활성화하고 취약점 관리를 시작합니다. 여러 레지스트리와 통합하려면 각 레지스트리에 대해 고유한 조직을 만듭니다.

**Steps:**

1. ACR 계정에 액세스하고 AcrPull 역할과 함께 Snyk에서 사용할 수 있는 고유한 서비스 주체 자격 증명을 검색합니다. 이 작업에 대한 도움말은 [ACR documentation](https://docs.microsoft.com/en-us/azure/container-registry/container-registry-auth-service-principal)을 참조하십시오.
2. Snyk 계정에 로그인합니다.
3. 상단의 메뉴 모음에서 **Integrations**로 이동하여 **ACR** 옵션을 찾아 클릭합니다.
4. **Settings** 영역의 ACR 구성 페이지가 나타납니다.
5. 통합에 대한 서비스 주체를 생성할 때 받은 사용자 이름, 암호 및 컨테이너 레지스트리 이름(myregistry.azurecr.io)을 입력하십시오.
6.  **Save**를 클릭합니다.

    Snyk는 연결 값과 page reload를 테스트하여 ACR 통합 정보를 표시합니다. 세부 정보가 저장되었다는 확인 메시지도 화면 상단에 녹색으로 나타납니다. 또한 Azure에 연결하지 못한 경우 Connected to ACR 섹션 아래에 알림이 나타납니다.

![](<../../../../.gitbook/assets/image (9).png>)
