# 시작하기

## Red Hat OpenShift Workload 보안

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/redhat-snyk-pipeline%20\(1\).png)

### 환영합니다!

이 실습에서는 Snyk를 Red Hat Workflow에 통합하여 애플리케이션의 잠재적인 취약점을 식별하고 수정하는 방법을 보여주는 실습 예제를 제공한다는 한 가지 목적을 염두에 두고 만든 일련의 연습을 안내합니다.

### 전제 조건

이 모듈에 제시된 예에는 일부 지원 인프라가 배포되어 사용할 수 있어야 합니다. 이는 [Red Hat OpenShift](http://try.openshift.com/) 클러스터, [Red Hat Quay.io](https://quay.io/) 프라이빗 레지스트리, [Snyk 계정](https://app.snyk.io/login) 및 [GitHub 저장소](https://github.com/snyk-partners/patterns-library-redhat)에서 사용할 수 있는 일부 지원 샘플 코드로 구성됩니다.

{% hint style="danger" %}
이 실습에 프로덕션 시스템을 사용하는 것은 **권장되지 않습니다**.
{% endhint %}

#### Red Hat OpenShift 클러스터

이 워크숍에 권장되는 배포 방법은 지원되는 퍼블릭 클라우드 공급자의 계정에 Red Hat OpenShift 4를 설치하는 것입니다. 이를 수행하는 데 필요한 단계에 대한 자세한 지침은 [Red Hat의 Get started with OpenShift](https://www.openshift.com/try) 사이트에서 확인할 수 있습니다.

#### Red Hat Quay.io 프라이빗 컨테이너 레지스트리

[Quay](https://quay.io/)를 배포하는 몇 가지 방법이 있습니다. 기능적으로 이러한 모듈에 포함된 단계는 이 레지스트리를 배포하는 방법에 관계없이 동일하지만 클라우드를 선택했습니다.

#### OpenShift 4가 포함된 Snyk 컨트롤러

OpenShift에서 실행되는 Kubernetes 워크로드에 대한 취약성 세부 정보를 얻으려면 먼저 클러스터에 Snyk 컨트롤러를 설치해야 합니다. Snyk 모니터가 올바르게 작동하려면 몇 가지 최소한의 구성 항목이 필요합니다. 필요한 단계는 [Snyk's Knowledge Center](https://support.snyk.io/hc/en-us/articles/360006548317#UUID-7b1c8c43-51a6-d807-5623-e2338f830623)에 자세히 설명되어 있습니다.

#### 종속성 분석 확장이 포함된 Microsoft Visual Studio Code

아직 VSCode가 없다면 무료로 [다운로드](https://code.visualstudio.com/download)해야 합니다. Visual Studio Marketplace에서 사용할 수 있는 [Red Hat Dependency Analytics](https://marketplace.visualstudio.com/items?itemName=redhat.fabric8-analytics) 확장을 활용할 것입니다. 종속성 분석은 업계에서 가장 진보되고 정확한 오픈 소스 취약성 데이터베이스인 [Snyk Intel Vulnerability DB](https://snyk.io/product/vulnerability-database/)로 구동됩니다. 이는 수많은 소스에서 파생된 최신의 가장 빠르고 더 많은 수의 취약점으로 가치를 더합니다.

#### 샘플 애플리케이션 및 추가 자료

예제에서는 Snyk의 취약한 데모 앱인 Goof에 대한 컨테이너 이미지를 빌드합니다. 이 연습을 완료하려면 저장소를 [`git clone`](https://github.com/snyk-partners/patterns-library-redhat.git)해야 합니다.
