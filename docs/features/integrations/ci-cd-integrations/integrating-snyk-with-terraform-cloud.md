# Terraform Cloud 통합

## Terraform Cloud 개요

[Terraform Cloud](https://www.terraform.io/cloud) (TFC)는 HashiCorp가 제공하는 SaaS 유료 플랫폼으로, Terraform을 사용하는 팀에게 프로덕션 준비 상태 관리 및 지속적인 제공을 제공합니다. Terraform을 통해 클라우드 인프라를 관리하는 팀은 다음과 같은 이점을 얻을 수 있습니다.

* 바로 사용할 수 있는 버전 관리 기능을 통해 클라우드에서 Terraform 상태를 관리할 수 있습니다.
* 팀이 인프라에서 협업하고 인프라 변경 사항을 검토 및 승인할 수 있는 중앙 집중식 장소를 확보합니다.
* Terraform Cloud에서 CI/CD 파이프라인과 유사한 방식으로 클라우드 공급자에 대한 원격 운영을 자동으로 관리하여 Terraform을 사용하여 클라우드 인프라에 변경 사항을 적용합니다.

{% hint style="info" %}
이 기능은 Hashicorp **Business tier** plan\*\*.\*\*의 사용자에게 제공됩니다. 더 낮은 Hashicorp plan에 있는 경우 [**Terraform Cloud Beta Sign Up form**](http://hashi.co/tfc-beta)의 개인 베타 기능 플래그에 액세스하려면 등록해야 합니다.
{% endhint %}

## **Snyk integration**과 **Terraform Cloud**의 통합 개요

Terraform Cloud는 Run Check라고 불리는 새로운 기능을 도입했습니다. TFC의 “Run”은 TFC의 실행 단위를 나타냅니다. TFC는 최종적으로 검토, 승인 및 적용될 Terraform plan을 생성합니다.

Run Check 베타 기능을 사용하면 외부 통합이 “Run” 이벤트에 연결하고 이벤트와 상호 작용하여 이 실행이 성공할지 실패할지 결정하는 상태를 제공할 수 있습니다.

Snyk [introduced support in May 2021](https://snyk.io/blog/prevent-cloud-misconfigurations-hashicorp-terraform-snyk-iac/)에 Terraform 사용자가 모든 주요 클라우드 공급자를 위한 Snyk 보안 정책과 비교하여 Terraform 계획 json 출력을 스캔할 수 있는 지원을 도입했습니다.

Snyk 통합은 Terraform Cloud의 “Run” 워크플로우를 Snyk Terraform plan scanning과 연결합니다. 즉, 생성된 각 "실행"에 대해 Snyk는 잘못된 구성이 있는지 Terraform plan 아티팩트를 스캔합니다.

Terraform Cloud 사용자라면 Snyk에 가입해 통합을 설정하고 Terraform Cloud의 작업 공간과 연결할 수 있습니다. 그러면 Terraform Cloud를 통해 소프트웨어 개발 라이프사이클의 일부로 보안 오류 구성을 추적, 관리 및 해결할 수 있습니다.

## Snyk과 Terraform Cloud 간의 통합 설정 및 사용

{% hint style="warning" %}
Terraform Cloud 통합을 구성하려면 Snyk 조직의 관리자여야 합니다.
{% endhint %}

Snyk Web UI의 **Integrations** 페이지에서 Terraform Cloud integration settings 페이지로 이동 후 다음 단계를 수행합니다.

### Terraform plan scanning 설정

1. Snyk의 integration setting 페이지에서 제공된 URL 및 HMAC 키를 복사합니다.
2. [Terraform Cloud](https://app.terraform.io)로 이동하여 조직의 global settings로 이동합니다.
3. Tasks settings으로 이동하십시오. 예를 들어 다음과 같이 접속합니다.\
   `https://app.terraform.io/app/{YOUR_TFC_ORG}/settings/tasks`
4. HMAC 키는 Terraform Cloud에서 옵션으로 식별되더라도 Snyk 통합이 작동하기 위한 필수 사항입니다.
5. 이 실행 작업을 Terraform Cloud의 작업 공간에 연결하려면 특정 작업 공간의 실행 작업 설정으로 이동하고 Snyk에 대해 새로 만든 실행 작업을 추가하십시오. 예를 들어 다음과 같습니다.\
   `https://app.terraform.io/app/{YOUR_TFC_ORG}/workspaces/{YOUR_WORKSPACE}/settings/tasks`
6. enforcement level(Advisory 또는 Mandatory)을 선택하고 Create를 클릭합니다.

통합이 설정되면 Snyk은 작업 공간에서 트리거된 각 실행에 대한Terraform plan을 스캔합니다.

### Terraform plan scanning 결과 확인

1. Terraform Cloud 작업 공간에서 트리거된 각 실행의 경우, Snyk이 Terraform plan scanning의 결과가  완료된 후 트리거되는 'Run tasks' 단계 아래에 나타납니다.
2. 검색 결과 \`passed\` 또는 \`failed\`상태가 됩니다. Snyk finds issues in your Terraform plan file에서 문제를 발견하면 scan이 실패합니다.
3. Snyk에서 자세한 내용을 확인하려면 Terraform Cloud에서 실행 작업 결과의 Details 링크를 클릭합니다.
   1. 또한 Snyk의 Projects 탭에서`{YOUR_TFC_ORG_NAME}/{YOUR_TFC_WORKSPACE_NAME}`이라는 이름의 대상 아래에 있는 terraform-plan.json을 검색하여 결과를 찾을 수 있습니다.
   2. 왼쪽 창의 필터를 사용하여 Terraform Cloud 프로젝트만 표시할 수도 있습니다.
4. Snyk 통합을 사용하는 작업 공간당 단일 프로젝트(`terraform-plan.json`)가 생성됩니다. 모든 프로젝트 페이지에는 최신 검색 결과가 표시됩니다.
5. 기록 검색 결과를 확인하려면 관련 프로젝트 아래의 History 탭으로 이동하여 확인하려는 기록 스냅샷을 선택하십시오.

### Terraform plan scanning 사용자 정의

Snyk Terraform Cloud 통합은 다음과 같은 수준의 사용자 지정을 제공합니다.

* Severity Threshold: 오류에 대한 최소 심각도 수준을 설정합니다. 이것은 Snyk의 통합 페이지에서 설정할 수 있습니다.
* Custom Severities: 기본값을 덮어쓰는 문제에 대한 사용자 지정 심각도를 설정합니다 (예: [SNYK-CC-TF-63](https://snyk.io/security-rules/SNYK-CC-TF-63)).
* Enforcement Level: 장애로 인해 적용이 차단되는지 여부를 결정합니다. 이 설정은 Terraform Cloud를 통해 제어됩니다. 예를 들어 Snyk이 최소 심각도 임계값 내에서 문제를 발견하더라도 `Advisory` level은 적용을 차단하지 않습니다.

### 참고 및 제한 사항

* Snyk는 Terraform Cloud의 최신 실행 내에서 완료된 각 "plan" 단계에 대해 Terraform Cloud로부터 이벤트를 받습니다.
* 검색을 트리거하는 유일한 방법은 새로운 "Run"을 트리거하여 Terraform Cloud를 통과하는 것입니다.
* Snyk UI를 통해 Terraform plan 파일의 재스캔을 트리거할 수 없습니다.
* Snyk 통합을 사용자 정의하는 경우(예: 심각도 임계값 변경 또는 정책 심각도 사용자 지정) 변경 사항을 Snyk에 적용하려면 Terraform Cloud에서 새 run을 트리거해야 합니다.
