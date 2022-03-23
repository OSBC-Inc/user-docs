# Snyk의 GitHub container registry에서 컨테이너 이미지 스캔

Snyk은 저장소에 있는 GitHub 컨테이너 이미지를 평가하고 모니터링 합니다. Snyk으로 가져오면 이미지 취약점이 노출되어 쉽게 분류할 수 있습니다.

GitHub container registry에서 Snyk으로 이미지를 가져오려면 다음과 같이 진행하십시오.

**전제 조건**

* 관련 조직에 액세스할 수 있는 Snyk 계정을 가지고 있어야 합니다(관리자에게 부여됨).
* GitHub container registry 통합이 구성 되어있어야 합니다. 자세한 내용은 [GitHub container registry 통합을 이용한 컨테이너 보안](container-security-with-github-container-registry-integration.md)을 참조하여 진행하십시오.

**진행 단계**

1. 계정에 로그인하고 관리하려는 관련 그룹 및 조직으로 이동합니다.
2. **Projects** 탭에서 **Add project**를 클릭합니다. 계정에 이미 구성된 통합 목록이 열립니다. **GitHub container registry** 옵션을 선택하거나 **GitHub container registry**가 나타나지 않으면 **Other**를 선택하십시오.
3. **Which images do you want to test?**가 나타나고 연결된 레지스트리에 사용 가능한 모든 이미지가 각 저장소별로 그룹화되어 표시됩니다. **Note**: GitHub container registry는 Docker v2 API를 따르지 않으므로 저장소에 이미지를 나열할 수 없습니다. 따라서 스캔하려는 이미지를 수동으로 지정해야 합니다.
4. Snyk으로 가져올 단일 또는 여러 이미지를 선택합니다. 특정 이미지를 선택하거나 전체 저장소를 선택할 수 있습니다. 이미지 이름으로 검색하여 가져올 특정 이미지를 찾을 수도 있습니다. 마치려면 오른쪽 상단의 **Add selected repositories**를 클릭합니다.
5. 이미지를 가져오면 페이지 상단에 상태 표시줄이 나타납니다. 진행되는 동안 다른 작업을 진행할 수 있습니다.
6. 가져오기가 끝나면 다음과 같이 진행합니다.
   * 새로 가져온 이미지는 **Projects** 페이지(**NEW** 태그로 표시)에서 확인할 수 있습니다. 이미지는 저장소별로 그룹화되며 각각 자세한 **Project** 페이지에 개별적으로 연결됩니다.
     * **import log**를 사용할 수 있게 되어 프로젝트 목록의 상단에서 접근할 수 있습니다.
   * 데이터를 보강하고 기본 이미지에 대한 권장 사항을 확인하려면 **Settings**에서 이미지 프로젝트에 Dockerfile을 연결할 수 있습니다. 자세한 내용은 [Dockerfile 추가 및 기본 이미지 테스트](../../scan-your-dockerfile/adding-your-dockerfile-and-test-your-base-image.md)를 참조하십시오.

GitHub container registry 가져오기는 특정 아이콘으로 표시되며 **projects**에서 필터링하여 GitHub container registry 프로젝트만 확인할 수 있습니다.

![](../../../../.gitbook/assets/mceclip1-5-.png)
