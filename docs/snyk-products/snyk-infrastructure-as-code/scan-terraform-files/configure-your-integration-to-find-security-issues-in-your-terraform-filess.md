# Terraform 파일에서 보안 문제를 찾기 위한 통합 구성

Snyk은 소스 코드 저장소에서 Terraform 파일을 테스트 및 모니터링하여 클라우드 환경을 보다 안전하게 보호하는 방법에 대한 조언을 제공합니다. 운영 환경으로 push하기 전에 잘못된 구성을 포착하여 수정할 수 있도록 지원합니다.

## 지원하는 Git 저장소 및 파일 형식

Snyk은 현재 통합 Git 저장소에서 가져올 때 Terraform(`.tf`) 파일을 스캔합니다. Terraform 모듈 저장소 스캔은 SCM에서 모듈을 보유하고 있는 저장소를 가져오거나 `snyk iac test` 명령을 사용하여 디렉토리 자체를 스캔하여 수행합니다.

Terraform을 스캔하면 모듈에 정적으로 구성된 모든 항목에 대한 보안 피드백을 제공합니다. 반복/예약 테스트를 통해 이점을 얻으려면 SCM에서 직접 사용자 정의 모듈을 가져오는 것을 권장합니다.

변수 보간 기능에 대한 블로그 게시물을 참조하십시오. [Snyk IaC public beta는 Terraform plan 분석](https://snyk.io/blog/snyk-iac-public-beta-introduces-terraform-plan-analysis/)을 도입하고 Terraform 모듈을 스캔합니다. 이렇게 하면 CLI를 통해 Terraform Plan 출력을 스캔할 수 있습니다. 배포를 생성하는 데 사용된 모듈의 출력을 포함하도록 전체 Terraform 배포 스캔을 활성화합니다.

## Terraform 구성 파일을 스캔하도록 Snyk 설정

**전제 조건**

* Snyk에서 구성하려는 조직의 관리자여야 합니다.
* 이미 Git 저장소를 통합했는지 확인하십시오. 아직 수행하지 않았다면 [Git 저장소(SCM) 통합](../../../features/integrations/git-repository-scm-integrations/)을 확인하십시오.

**Snyk 설정**

* 계정에 로그인하고 관리하려는 관련 그룹 및 조직으로 이동합니다. **Note:** 통합은 조직별로 관리합니다.
* 다음과 같이 Infrastructure as code 파일을 감지하도록 Snyk을 활성화합니다.

![Enable\_Snyk\_to\_detect\_Kubernetes\_configuration\_files.gif](../../../.gitbook/assets/enable\_snyk\_to\_detect\_kubernetes\_configuration\_files.gif)

* 필요한 경우 **Infrastructure as code** 설정 영역에서 설정을 조정합니다.

![](../../../.gitbook/assets/screen\_shot\_2021-06-22\_at\_11.43.49.png)
