# GCR 액세스 권한 설정

**전제 조건**

Snyk과 통합하려는 Google 계정에 대해 [Cloud Resources Manager API](https://console.cloud.google.com/apis/library/cloudresourcemanager.googleapis.com?q=cloud%20resource%20manager\&id=16f5d23e-c895-4b9d-88e4-864c1766636f\&project=next-for-integration-testing)를 사용하도록 설정합니다.

Google의 관련 프로젝트에서 Snyk 통합을 위한 서비스 계정을 생성했는지 확인하십시오.

**진행 단계**

1. Google Cloud Platform Console [Credentials](https://console.cloud.google.com/apis/credentials) 페이지로 이동하여 통합할 프로젝트를 선택한 다음 새로운 서비스 계정 키 설정을 선택하십시오.
2. 로드되는 보기에서 이 통합을 위해 생성한 드롭다운 목록에서 서비스 계정을 선택하고 다음 값을 사용하여 해당 계정에 대한 새로운 키를 구성합니다.
   * **Service account name** - 나중에 기억할 수 있도록 계정에 고유한 이름을 할당합니다.
   * **Role** - 스토리지 오브젝트 뷰어(roles/storage.objectViewer)
   * **Service account ID** - 비워 두십시오.
   * **Key type** - JSON
3. **Create**를 클릭하세요. 프로젝트에 대한 키가 생성됩니다.
4. 다음과 유사한 JSON 파일의 전체 내용을 복사합니다.

![GCR\_key\_file\_contents.png](../../../../.gitbook/assets/uuid-c4e3b781-e575-5ab8-6cea-b0a8654068c4-en.png)

복사한 데이터는 저장하여 Snyk과 통합을 구성할 때 붙여넣습니다.

**다음 단계**

이제 [GCR 통합을 구성](configure-integration-for-gcr.md)합니다.
