# Kubernetes 구성 파일에서 보안 문제를 찾기 위한 통합 구성

Snyk은 소스 코드 저장소에 저장된 Kubernetes 구성을 테스트하고 모니터링하며 Kubernetes 환경을 보다 안전하게 보호하기 위한 정보를 제공하여 잘못된 구성을 프로덕션으로 전송하기 전에 포착하고 취약점에 대한 수정을 제공합니다.

## 지원하는 Git 저장소 및 파일 형식

Snyk은 현재 통합 Git 저장소에서 가져올 때 JSON 및 YAML 형식의 Kubernetes 구성 파일을 검색합니다.

## Kubernetes 구성 파일을 스캔하는 Snyk 설정

**전제 조건**

* Snyk에서 구성하려는 조직의 관리자여야 합니다.
* 이미 Git 저장소를 통합했는지 확인하십시오. 아직 수행하지 않았다면 [Git 저장소(SCM) 통합](../../../features/integrations/git-repository-scm-integrations/)을 확인하십시오.

**Snyk 설정**

계정에 로그인하고 관리하려는 관련 그룹 및 조직으로 이동합니다.

![](<../../../.gitbook/assets/add-artifactory-images (1) (2) (46).gif>)

{% hint style="info" %}
**Note**\
통합은 조직별로 관리합니다.
{% endhint %}

다음과 같이 진행합니다.

1. 설정에서 플래그를 활성화하여 Kubernetes 구성 파일을 감지하도록 Snyk을 활성화 합니다. ![cog\_icon.png](../../../.gitbook/assets/cog\_icon.png) > **Infrastructure as code**
2. 필요한 경우 **Infrastructure as code** 설정 영역에서 설정을 조정합니다.

![Configure-Policies.png](../../../.gitbook/assets/uuid-34af73f5-ffde-39bb-ffa4-364884089b2e-en.png)

제품당 테스트 횟수는 요금제에 따라 다릅니다. 테스트 제한에 대한 정보는 [요금제](https://snyk.io/plans/)를 참조하십시오.
