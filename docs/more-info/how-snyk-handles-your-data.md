# Snyk이 데이터를 처리하는 방법

## Snyk 보안 및 컴플라이언스: Snyk은 데이터를 어떻게 처리합니까?

Snyk은 개발자 보안 플랫폼이므로 데이터 보안을 가장 중요하게 생각합니다. **귀하의 개인 정보 보호 및 보안 요구 사항을 완전히 이해한 이 문서의 목표는 Snyk에 의해 어떤 데이터가 어떤 방식으로 액세스, 전송 및 저장되는지 투명하게 제공하는 것입니다.**

Snyk에서 처리하는 데이터는 사용 중인 제품, Snyk과 통합하는 방법 및 Snyk 배포에 따라 달라집니다. Snyk은 빠르게 변화하는 제품이기 때문에 액세스 및 저장하는 데이터의 유형은 새로운 기능이 도입되거나 기존 기능이 변경되면 함께 변경될 수 있습니다.

### 유연한 배포 옵션

Snyk은 최신 소프트웨어 개발 방식과 기술을 활용하여 고객에게 비즈니스 요구에 가장 적합한 방식으로 Snyk의 개발자 보안 플랫폼을 사용할 수 있는 유연성을 제공합니다.

Snyk의 클라우드 우선 배포 옵션은 사용 편의성과 확장성을 제공하는 동시에 미국과 EU에서 지원되는 다중 및 단일 테넌시(Multi-Single Tenancy) 옵션을 통해 필요한 수준의 데이터 보호 기능을 제공합니다. (향후 추가 지역 지원 예정)

* **Multi-Tenant SaaS**: Snyk의 개발자 보안 플랫폼을 사용하는 가장 간단하고, 일반적이며, 비용 효율적인 방법
* **Single-Tenant SaaS:** 프라이빗 클라우드 - AWS에서 Snyk 개발자 보안 플랫폼의 격리된 완전 관리형 인스턴스입니다.
* **Snyk Broker**: Snyk 개발자 보안 플랫폼(Multi 또는 Single Tenant)과 사내 코드베이스 사이에서 프록시 역할을 하는 사설 인프라에 설치되는 클라이언트 서비스입니다. Snyk Broker는 인바운드 및 아웃바운드 연결을 안전하게 처리하고 전송 중에 데이터를 암호화하며 Snyk이 데이터에 액세스하는 것을 의도적으로 제어합니다. 민감한 인증 정보는 방화벽 뒤에 있습니다.

**이러한 다양한 옵션을 활용하여 요구사항을 충족할 수 있는 방법에 대한 자세한 내용은 Snyk 담당자에게 문의하십시오.**

### Snyk 전반의 고객 데이터 흐름

Snyk은 다양한 유형의 데이터가 필요하고 다양한 데이터 상호 작용을 수반하는 광범위한 개발 도구 및 통합을 제공합니다. 아래 섹션에서는 Snyk이 액세스하고 저장하는 일반적인 데이터 유형과 제품 및 통합별 유형에 대한 개요를 제공합니다. 이 정보는 최소 연 2회 또는 제품 운영에 중대한 변경이 발생할 때 검토됩니다.

### 공통 데이터 유형

* **Vulnerability data** - Snyk은 고객 애플리케이션 및 관련 수정 컨텍스트에서 확인된 취약점에 대한 정보를 저장합니다.
* **Vulnerability source** - Snyk은 취약점이 확인된 위치에 대한 정보를 저장합니다. 예: 소스코드 저장소/레지스트리, 파일명 및 위치, 디펜던시 트리, 취약점 경로
* **Integration-related data** - Snyk은 Snyk과의 통합을 설정하는 데 필요한 정보를 저장합니다. 예: 토큰 및 구성
* **User data** - Snyk은 기본 사용자 정보를 저장합니다. 예: 사용자명, ID, 이메일 주소
* **User list** - 정확한 기여자 계산을 위해 Snyk은 모니터링되는 저장소에 대한 지난 90일 동안의 커밋에 액세스합니다. 요청 시 해시되지 않은 버전의 사용자 이메일이 생성됩니다.
* **Billing data** - Snyk은 Snyk 계정 청구에 필요한 정보를 저장합니다.
* **User behavior analytics** - Snyk은 사용 패턴과 관련된 다양한 유형의 정보를 저장합니다. 예: 웹사이트 방문, 실행된 CLI 명령

### 제품별 데이터 유형

데이터를 보호하는 것이 얼마나 중요한지 알고 있습니다. 당사 제품은 정확한 분석을 위해 필요한 정보만 액세스하고 저장합니다.

{% tabs %}
{% tab title="Snyk Open Source" %}
**Snyk Open Source**

![](https://snyk.io/wp-content/uploads/shield-snyk-open-source.svg)

* Snyk은 오픈소스 디펜던시를 식별하기 위해 매니페스트 및 빌드 구성 파일에 액세스합니다.
* `--unmanaged` 옵션을 사용하는 테스트의 경우 소스코드 파일에 액세스하여 파일 서명(해시)으로 변환하고 파일 서명 및 파일 이름을 저장합니다. 다른 Snyk 오픈소스 스캔은 소스코드에 액세스하지 않습니다.
* SCA 스캔의 경우 Snyk이 소스코드에 액세스하지 않습니다.
* Snyk은 의존성의 이름과 버전 번호에 액세스하고 저장합니다.&#x20;
* Snyk은 저작권 및 속성 정보를 포함하여 관련 라이선스의 이름을 저장합니다.&#x20;
* Snyk은 저장소별 정보에 액세스하고 저장합니다.
* Snyk은 Git 공급자의 push 및 pull 특정 정보에 액세스하고 저장합니다. 예: 기여자 이름, 파일명, 타임스탬프

**Optional ADD-ONS (**옵션**)**

* Reachable Vulnerabilities 계산 - Snyk은 소스코드를 저장하여 호출 그래프 구축을 용이하게 합니다. 분석이 완료되면 Snyk 시스템에서 코드가 제거됩니다. 호출 그래프와 함수 이름만 유지됩니다.
* Lambda 통합의 경우 - Snyk은 단기 복사본을 가져온 다음 분석의 일부로 해당 복사본을 삭제합니다.
{% endtab %}

{% tab title="Snyk Code" %}
**Snyk Code**

![](https://snyk.io/wp-content/uploads/shield-snyk-code.svg)

* Snyk은 일회성 분석을 위해 저장소 코드에 액세스하여 최대 24시간 동안 캐싱합니다. 이 기간이 지나면 발견된 Issue의 위치(파일 경로, 줄 및 열)와 Issue ID 및 설명만 유지됩니다. 귀하의 코드는 제거되고 Snyk 네트워크 또는 로그에 저장되지 않습니다.
* 결과는 데이터베이스에 저장되고 Snyk에 의해 분석 및 모니터링 목적으로 사용됩니다.
* Snyk Code는 엔진 교육 목적으로 고객 코드를 사용하지 않으며, 가능한 수정 사항을 보여주기 위한 예제를 추출합니다.
* 스캔 결과에는 원본 소스코드가 아니라 위치(예: 파일, 줄 및 열 번호)에 대한 포인터와 올바른 버전의 소스코드를 사용하여 결과가 표시되도록 식별 메타 정보가 포함됩니다.
* Snyk은 저장소 관련 정보를 저장합니다. 예: Git 저장소명, 파일명
* 서버 인프라는 인증 및 권한 부여를 사용하여 고객을 분리합니다. Snyk Code는 소프트웨어 제어를 사용하여 고객 데이터 분리를 보장합니다. 모든 통신은 고급 산업 표준 프로토콜을 사용하여 암호화됩니다.
{% endtab %}

{% tab title="Snyk Container" %}
**Snyk Container**

![](https://snyk.io/wp-content/uploads/shield-snyk-container.svg)

* Snyk은 패키지 버전, 실행 가능한 해시/버전, 운영체제, 컨테이너 이미지 메타데이터(예: rootfs 해시, 기록), 이미지 ID에 엑세스하고 저장합니다.
* Snyk은 상위 이미지(이름/버전/태그)와 관련된 정보에 액세스하고 저장합니다.
* Snyk은 Dockerfile에서 RUN 명령에 액세스하고 저장합니다.
* Kubernetes 구성 - Snyk은 워크로드 보안 설정(예: 'run as root')에 액세스합니다. 이것은 Snyk의 Kubernetes 통합을 사용하는 경우에만 액세스됩니다.
* 컨테이너 레지스트리 통합 - Snyk은 컨테이너 이미지의 단기 복사본을 액세스한 다음 저장합니다(브로커가 사용되지 않는 경우). 이 복사본은 분석 후 Snyk 네트워크에서 제거됩니다.
{% endtab %}

{% tab title="Snyk IaC" %}
**Snyk Infrastructure as Code**

![](https://snyk.io/wp-content/uploads/shield-snyk-iac.svg)

* CLI 스캔은 로컬에서 수행됩니다. 파일 내용은 Snyk에 의해 공유되거나 저장되지 않습니다.
* Git 기반 스캔에는 Infrastructure as Code 파일에 대한 액세스가 필요합니다. Snyk은 분석 기간 동안 데이터를 저장한 후 시스템에서 삭제합니다. IaC 파일은 Snyk에 의해 저장되지 않습니다.
* Snyk UI의 강조 표시된 코드 스니펫은 제공된 소스코드 저장소 통합에서 git 기반 스캔을 활용하여 동적으로 생성됩니다. 귀하의 코드 스니펫과 IaC 파일은 Snyk에 의해 저장되지 않습니다.
* Drift 감지 스캔은 최소 권한 원칙에 의존합니다.
  * Snyk은 애플리케이션에 대한 승인된 액세스 권한을 요구하지 않습니다. 또한 클라우드 인증 정보를 수집하거나 저장하지 않습니다.
  * Snyk에는 로컬 읽기 전용 Terafform 상태 액세스 권한이 필요합니다. 상태는 Snyk에 전송되거나 분석되지 않습니다.
{% endtab %}
{% endtabs %}

### Snyk 인증

![](../.gitbook/assets/Soc2.png)

Snyk은 ISO 27017:2015의 추가적인 객관적 통제를 통해 ISO 27001:2013 인증을 받았습니다.

![](../.gitbook/assets/Coalfire.png)

### Snyk 정책:

* [Privacy](https://snyk.io/policies/privacy/)
* [Snyk Sub-processing](https://snyk.io/policies/sub-processors/)
* [Data processing](https://snyk.io/policies/dpa/)
* [Tracking & analytics](https://snyk.io/policies/tracking-and-analytics/)
