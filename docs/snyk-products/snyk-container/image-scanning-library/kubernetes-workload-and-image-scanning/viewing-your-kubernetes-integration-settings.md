# Kubernetes 통합 설정 확인

## 관련 조직

1. settings ![](../../../../.gitbook/assets/cog\_icon.png) > **Integrations**를 클릭합니다.
2. Kubernetes로 이동하여 **Edit** **Settings**를 클릭합니다.
3. **Integration ID** 및 기타 통합 설정으로 이동합니다.

![](../../../../.gitbook/assets/uuid-03a03790-d87e-6260-4ffc-dc474ce014fa-en.gif)

이 화면에서 다음 항목에 액세스하고 작업할 수 있습니다.

| Part                       | Description                                                                                                                                                                                                                                                                                                                                                     |
| -------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Connected to Kubernetes    | 통합이 아직 설정되지 않은 경우 연결 버튼과 함께 이 창에 나타나는 유일한 섹션입니다 (다음 지침과 통합: ([Kubernetes integration overview](kubernetes-integration-overview.md)). Connect button을 클릭하고 성공적으로 연결되었을 때 이 영역이 이미지와 같이 표시됩니다.                                                                                                                                                                    |
| Integration ID             | T통합 ID는 UUID이며`abcd1234-abcd-1234-abcd-1234abcd1234`와 유사합니다. 아직 구성을 설정하지 않은 경우 Connect를 누르고 이 ID를 사용하여 구성을 설정합니다. 구성을 이미 설정한 경우 이 페이지로 이동하여 이동할 때 이 창과 창의 나머지 데이터가 즉시 표시됩니다. 이제 여기서 대시보드, 프로젝트 페이지에서 워크로드를 추가하거나 클러스터에서 자동 가져오기를 설정할 수 있습니다. [Adding Kubernetes workloads for security scanning](adding-kubernetes-workloads-for-security-scanning.md)을 참조하십시오. |
| Snyk controller versions   | 이 영역에서 클러스터에 설치한 Snyk 컨트롤러 버전을 확인하십시오.                                                                                                                                                                                                                                                                                                                          |
| Disconnect from Kubernetes | 이 조직에서 이 통합을 제거하려면 Disconnect를 클릭하십시오.                                                                                                                                                                                                                                                                                                                          |
