# Dockerfile 추가 및 기본 이미지 테스트

major, minor 및 대체 업그레이드를 포함한 기본 이미지 수정 조언과 이미지를 다시 빌드해야 할 때를 알려면 원하는 Git 저장소와 통합한 후 관련 Dockerfile이 포함된 저장소를 가져오십시오.

가져온 각 이미지에 하나의 Dockerfile을 추가할 수 있습니다.

**추가적인 수정 조언을 위해 Dockerfile을 추가하려면 아래와 같은 전제 조건이 있습니다.**

* 관련 Git 저장소가 구성되었는지 확인합니다.
* 먼저 레지스트리에서 관련 이미지를 가져옵니다.

**단계:**

1. **Project** 탭에서 프로젝트를 필터링한 다음 톱니바퀴 모양의 설정을 클릭하여 Dockerfile을 추가할 설정에 액세스합니다.
2. **Project** 설정 페이지에서 **Configure Dockerfile**을 클릭한 후 관련 Git을 선택합니다.
3. **Add Projects** 화면이 나타나고 통합한 Git 계정의 모든 저장소를 조직 및 개인 계정별로 표시됩니다.
4. Dockerfile을 가져올 관련 저장소를 선택합니다.
5. ~~Step 2 loads.(?)~~
6. **Path to your Dockerfile** 필드에 /path/dockerfile 형식으로 상대 경로를 입력합니다.
7. **Save**를 클릭합니다.

![](<../../../.gitbook/assets/image (45).png>)

Snyk은 프로젝트를 다시 테스트하여 다음 예와 같은 관련 기본 이미지 수정 조언을 생성합니다.

![](../../../.gitbook/assets/mceclip1-2-.png)
