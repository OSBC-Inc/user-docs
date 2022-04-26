# CloudFormation 파일의 보안 문제 스캔 및 수정

Snyk은 CloudFormation 코드를 스캔하여 잘못된 구성과 보안 문제를 확인합니다. 구성 파일의 경우, 일단 스캔되면 Snyk은 관리자가 구현하는 설정에 따라 잘못된 구성에 대해 보고하고 그에 따라 수정 권장 사항을 제공합니다.

## 전제 조건

* 관리자는 조직을 선호하는 Git 저장소와 통합하고 [문서](configure-your-integration-to-find-security-issues-in-your-cloudformation-files.md)에 설명한 대로 구성 파일 감지를 활성화해야 합니다.
* Snyk 계정이 있어야 하며 CloudFormation 파일의 형식은 다음과 같습니다. `JSON`, `YAML`.

## 구성 파일 스캔 및 수정

* 계정에 로그인하여 해당 그룹 및 조직으로 이동합니다.

![](<../../../.gitbook/assets/screenshot-2020-07-09-at-12.43.02-2- (3) (4) (4) (4) (1) (3).png>)

* CloudFormation 코드를 감지하기 위해 infrastructure as code 기능이 활성화되기 전에 테스트가 수행된 경우 저장소를 다시 가져옵니다.

![](<../../../.gitbook/assets/screenshot\_2020-07-09\_at\_12.44.03 (1) (1) (3) (3) (2) (1) (3).png>)

* 저장소를 스캔할 때마다 다음과 같이 진행합니다.
  * 모든 CloudFormation 파일은 다음 예제와 같이 저장소별로 그룹화된 별도의 프로젝트로 가져옵니다.

![](../../../.gitbook/assets/screen\_shot\_2021-06-23\_at\_10.16.38.png)

* 저장소를 다시 가져온 경우 CloudFormation 파일을 가져오기 위해 Snyk은 기존 애플리케이션 매니페스트 파일을 가져와 다시 테스트합니다. 테스트 시간은 "now"로 표시됩니다.
  * 스캔 결과를 보고 CloudFormation 코드에 대한 세부 정보를 확인하려면 프로젝트 링크를 클릭하십시오.

![Screen\_Shot\_2021-06-23\_at\_10.18.49.png](../../../.gitbook/assets/screen\_shot\_2021-06-23\_at\_10.18.49.png)
