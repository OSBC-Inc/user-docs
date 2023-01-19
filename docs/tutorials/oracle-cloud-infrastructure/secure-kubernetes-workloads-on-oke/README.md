# OKE의 보안 Kubernetes Workload

## OKE는 무엇입니까?

OKE(Oracle Container Engine for Kubernetes)는 최신 클라우드 네이티브 애플리케이션을 구축하는 데 드는 시간과 비용을 줄일 수 있는 Oracle 관리 컨테이너 오케스트레이션 서비스입니다. 대부분의 다른 공급업체와 달리 Oracle Cloud Infrastructure는 Kubernetes용 Container Engine을 고성능, 저비용 컴퓨팅 형태에서 실행되는 무료 서비스로 제공합니다. DevOps 엔지니어는 애플리케이션 Workload 이식성을 위해 수정되지 않은 오픈 소스 Kubernetes를 사용하고 자동 업데이트 및 패칭으로 운영을 단순화할 수 있습니다. [여기](https://www.oracle.com/cloud-native/container-engine-kubernetes/)에서 OKE에 대해 자세히 알아보십시오.

## 무엇을 배울 수 있습니까?

이 실습에서는 Snyk을 사용하여 OKE에서 실행되는 Kubernetes Workload를 빠르게 배포하고 스캔하여 오픈 소스 종속성, 컨테이너 이미지 및 애플리케이션 구성 오류의 취약성을 찾는 방법을 배웁니다.

### 전제 조건

* [Oracle Cloud Free Tier](https://www.oracle.com/cloud/free/?source=:ow:o:p:nav:092320ContnrKuberntsHero\&intcmp=:ow:o:p:nav:092320ContnrKuberntsHero) 계정.
* [OCI CLI](https://docs.oracle.com/en-us/iaas/Content/API/SDKDocs/cliinstall.htm) 설치.
* [Snyk](https://snyk.co/udrgA) Business 또는 Enterprise 계획.

{% hint style="danger" %}
이 기능은 모든 유료 요금제에서 사용할 수 있습니다. 자세한 내용은 [요금제](https://snyk.io/plans/)를 참조하세요.
{% endhint %}
