# GCR 통합 구성

Snyk에서 Google Container Registry와 통합하여 취약점을 스캔하고 결과에 따라 보안 및 라이선스 Issue를 수정합니다.

**전제 조건**

GCR 계정에서 새로운 서비스 계정 키를 설정합니다. (참조: [enable-permissions-to-access-gcr.md](enable-permissions-to-access-gcr.md "mention")).

**진행 단계**

1. Snyk 조직으로 이동하고 **Integrations=>GCR**로 이동합니다.
2. GCR hostname에서 스캔할 이미지의 [registry storage region](https://cloud.google.com/container-registry/docs/pushing-and-pulling)을 region.gcr.io 형식으로 입력합니다. (예: gcr.io, asia.gcr.io)
3. 아래 스크린샷처럼 Google에서 만든 JSON 키 파일의 전체 내용을 Snyk 계정의 JSON key file 필드에 붙여넣습니다.
4.  **Save**를 클릭합니다.

    Snyk이 인증 정보를 확인하고 성공하면 연결이 성공했다는 알림과 함께 페이지가 새로고침됩니다.

![GCR\_configur.png](../../../../.gitbook/assets/uuid-47cf04cb-248e-5d0f-d35a-f36fbb624614-en.png)

