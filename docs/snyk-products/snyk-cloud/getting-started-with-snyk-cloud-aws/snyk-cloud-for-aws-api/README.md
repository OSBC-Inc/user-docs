# AWS용 Snyk Cloud: API

API를 통해 AWS 계정을 Snyk Cloud에 온보딩하기 전에 읽기 전용 IAM(Identity & Access Management) 역할을 생성할 수 있는 권한이 있는 AWS 계정 및 연결된 자격 증명에 액세스해야 합니다. 모든 [전제 조건](../#prerequisites) 확인해보십시오.

API를 통해 AWS 계정을 Snyk Cloud에 온보딩하려면:

1. [코드형 인프라(IaC) 템플릿 다운로드](step-1-download-iam-role-iac-template.md): 계정을 스캔하기 위한 Snyk Cloud 권한을 부여합니다.
2. [AWS IAM 역할 생성](step-2-create-the-snyk-iam-role-api.md): 다운로드한 템플릿을 사용합니다.
3. [Snyk Cloud 환경 생성 및 스캔](step-3-create-and-scan-a-snyk-cloud-environment.md)

이제 Snyk Cloud에서 찾은 문제를 볼 수 있습니다. [Snyk Cloud 이슈](../../snyk-cloud-issues/) 참조하십시오.
