# Kubernetes 구성 파일의 보안 문제 스캔 및 수정

Snyk Infrastructure as Code는 매니페스트 파일에서 보안 취약점을 스캔하고 Kubernetes 구성 파일에서 잘못된 구성 및 보안 문제를 스캔합니다. 구성 파일의 경우, 일단 스캔되면 Snyk은 관리자가 구현한 설정에 따라 잘못된 구성에 대해 보고하고 그에 따라 수정하기 위한 권장 사항을 제공합니다.

## 전제 조건

* 관리자는 조직을 선호하는 Git 저장소와 통합하고 [문서](configure-integration-for-security-issues-in-kubernetes-configuration-files.md)에 설명한 대로 구성 파일 감지를 활성화해야 합니다.
* Snyk 계정이 있어야 하며 Kubernetes 구성 파일의 형식은 다음과 같습니다. `JSON`, `YAML`.

Snyk Infrastructure as Code는 다음 항목을 지원합니다.

* Deployments, Pods 및 Services.
* CronJobs, Jobs, StatefulSet, ReplicaSet, DaemonSet 및 ReplicationController.

## 구성 파일 스캔 및 수정

1. 계정에 로그인하고 관리하려는 관련 그룹 및 조직으로 이동합니다.
2. 관리자가 클라우드 구성 파일 감지를 활성화하기 전에 테스트를 위해 이미 저장소를 가져온 경우 관련 JSON 또는 YAML 구성 파일을 가져오기 위해 해당 저장소를 다시 가져와야 합니다.
3. 저장소를 스캔할 때마다 다음과 같이 진행합니다.
   1. 지원하는 모든 매니페스트 파일과 지원하는 모든 구성 파일은 다음 예시와 같이 저장소별로 그룹화된 별도의 프로젝트로 가져옵니다.
   2. 클라우드 구성 파일을 가져오기 위해 저장소를 다시 가져온 경우 Snyk은 구성 파일을 가져와 테스트하고 이미 가져온 애플리케이션 매니페스트 파일도 다시 테스트하여 테스트 시간을 "now"로 표시합니다.
4. 관심 있는 프로젝트 링크를 클릭하여 스캔 결과를 확인하고 이에 따라 구성 파일을 수정합니다.

![4.png](../../../.gitbook/assets/4.png)
