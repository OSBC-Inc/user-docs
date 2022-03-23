# JFrog Artifactory container registry 통합 구성

컨테이너 레지스트리로 하나의 Artifactory 인스턴스와 Snyk 조직 간의 통합을 활성화하여 이미지 보안 관리를 시작합니다.

## 전제 조건

* Snyk에서 구성할 조직의 관리자여야 합니다.
* Snyk은 Artifactory와 통합하려면 사용자 인증 정보가 필요하며 SSO(Single Sign-On)용으로 구성된 경우 Artifactory를 지원하지 않습니다.
* 자체 호스팅된 Artifactory를 사용하는 경우 [broker configuration](../../integrate-self-hosted-container-registries/snyk-integration-to-self-hosted-container-registries.md)에 대해 설명하는 설명서를 참조하십시오.

## 통합 구성

1. Snyk 계정으로 [로그인](https://app.snyk.io)합니다.
2.  상단의 메뉴 모음에서 **Integrations**로 이동하여 Artifactory 옵션을 찾아 클릭합니다.

    ![](<../../../../.gitbook/assets/image (57).png>)
3. **Settings** 영역의 구성 페이지가 나타납니다.
4. 다음과 같이 인증 정보를 입력합니다.
   1. **Username과 Password -** Artifactory 로그인 인증 정보를 사용합니다.
   2. **Container registry name -** `<org>.jfrog.io/artifactory/api/docker/<repo-name>`형식의 전체 레지스트리 URL입니다.
5. **Save Changes**를 클릭합니다.

![Screenshot 2021-12-06 at 16 37 12](https://user-images.githubusercontent.com/112600/144875482-078b715e-2834-469b-9983-7e88a65f175e.png)

![](../../../../.gitbook/assets/uuid-3b329a90-394f-5ab3-af84-658b41a1edc0-en.png)

Snyk은 연결 값을 테스트하고 페이지를 다시 로드하여 이제 입력한 통합 세부 정보를 표시합니다. 세부 정보가 저장되었다는 확인 메시지도 화면 맨 위에 녹색으로 표시됩니다. 또한 연결에 실패한 경우 알림이 나타납니다.
