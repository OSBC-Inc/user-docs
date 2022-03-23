# Snyk에서 DigitalOcean 컨테이너 이미지 스캔

Snyk은 저장소에서 해당 태그를 평가하여 DigitalOcean 컨테이너 이미지를 테스트하고 모니터링합니다. Snyk으로 가져오면 이미지 취약점이 노출되어 쉽게 분류할 수 있습니다.

DigitalOcean에서 Snyk으로 이미지를 추가하려면 다음과 같이 진행합니다.

**전제 조건**

* 관련 조직에 대한 액세스 권한이 있는 Snyk 계정이 존재해야 합니다(관리자가 부여).
* DigitalOcean 통합이 구성되어 있는 상태여야 합니다. 이에 대한 자세한 내용은 [문서](container-security-with-digitalocean-integration.md)를 참조하십시오.

**진행 단계**

1. 계정에 로그인하고 관리하려는 관련 그룹 및 조직으로 이동합니다.
2. **Projects** 탭에서 **Add Project**를 클릭합니다. 계정에는 이미 구성된 통합 목록이 열립니다. **DigitalOcean** 옵션을 선택하거나 **DigitalOcean**이 나타나지 않으면 **Other**를 선택합니다.
3. **Which images do you want to test?** 보기가 나타나고 연결된 레지스트리에 사용 가능한 모든 이미지가 다음과 비슷하게 각 저장소별로 그룹화되어 표시합니다.
4. Snyk으로 가져올 단일 또는 여러 이미지를 선택합니다. 특정 이미지를 선택하거나 전체 저장소를 선택하여 진행할 수 있습니다. 이미지 이름으로 검색하여 가져올 특정 이미지를 찾을 수도 있습니다. 마치려면 오른쪽 상단에 있는 **Add selected repositories**를 클릭합니다.
5. 이미지를 가져오면 페이지 맨 위에 상태 표시줄이 나타납니다. 그동안 다른 작업을 계속할 수 있습니다.
6. 가져오기가 끝나면 다음을 수행합니다.
   1. 새로 가져온 이미지는 **Projects** 페이지(**NEW** 태그로 표시)에서 확인할 수 있습니다. 이미지는 저장소별로 그룹화되며 각각 자세한 프로젝트 페이지에 개별적으로 연결합니다.
   2. **import log**를 사용할 수 있고 프로젝트 목록 상단에서 접근할 수 있습니다.
   3. 데이터를 풍부하게 만들고 기본 이미지에 대한 권장 사항을 얻으려면 **Settings**에서 이미지 프로젝트에 Dockerfile을 연결할 수 있습니다. 자세한 내용은 [Dockerfile 추가 및 기본 이미지 테스트](../../scan-your-dockerfile/adding-your-dockerfile-and-test-your-base-image.md)를 참조하세요.

DigitalOcean은 특정 아이콘으로 표시되며 **projects** view에서 통합을 필터링하여 DigitalOcean 프로젝트만 확인할 수 있습니다.

![](../../../../.gitbook/assets/mceclip0-11-.png)
