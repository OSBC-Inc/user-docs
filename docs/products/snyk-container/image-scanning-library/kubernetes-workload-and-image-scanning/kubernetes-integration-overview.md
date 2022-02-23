# Kubernetes 통합 개요

Snyk은 Kubernetes와 통합하여 실행중인 워크로드를 가져오고 테스트하며 관련 이미지 및 구성에서 워크로드의 보안을 떨어뜨릴 수 있는 취약점을 식별할 수 있습니다. 가져온 후에도 Snyk은 워크로드를 계속 모니터링하여 새로운 이미지가 배포되고 워크로드 구성이 변경됨에 따라 추가적인 보안 문제를 파악합니다.

{% hint style="info" %}
**기능 사용 여부**\
이 기능은 Business 및 Enterprise plan에서 사용할 수 있습니다. 자세한 내용은 [pricing plans](https://snyk.io/plans/)를 참조하세요.
{% endhint %}

**How it works**

1. 관리자가 클러스터에 컨트롤러를 설치하여 Snyk 계정에서 생성된 고유한 ID로 통합을 인증합니다. 다음 옵션 중 하나를 사용하여 컨트롤러를 설치합니다.
   * [Install the Snyk controller with Helm](install-the-snyk-controller-with-helm.md)
   * [Install the Snyk controller with OpenShift and OperatorHub](install-the-snyk-controller-with-openshift-4-and-operatorhub.md)
   * [Install the Snyk controller on Amazon Elastic Kubernetes Service (Amazon EKS)](install-the-snyk-controller-on-amazon-elastic-kubernetes-service-amazon-eks.md)
2. 컨트롤러는 Kubernetes API와 통신하여 클러스터에서 실행 중인 워크로드(Deployment, ReplicationController, CronJob 등)를 확인하고관련 이미지를 찾아 클러스터에서 직접 취약점을 스캔합니다.
3. 공동작업자는 Snyk에서 가져올 워크로드를 선택하거나 주석을 이용하여 워크로드를 자동으로 가져올 수 있습니다. 이러한 옵션은 [Adding Kubernetes workloads for security scanning](adding-kubernetes-workloads-for-security-scanning.md)에 설명되어 있습니다.
4. 공동작업자가 가져오는 각 워크로드에 대해 Snyk은 각 이미지에 발견된 취약점과 워크로드에서 식별된 구성 문제의 요약을 표시합니다.
5. Snyk은 가져온 워크로드를 지속적으로 모니터링하여 프로젝트에 영향을 미칠 때마다 새로운 취약점이 공개될 때 보고합니다.
6. 취약점이 발견되면 즉시 조치를 취할 수 있도록 Snyk은 email 또는 Slack을 통해 사용자에게 알립니다.

{% hint style="warning" %}
데이터베이스의 상태를 유지하기 위해 **4일동안 변경 또는 업데이트**되지 않은 작업 부하와 관련된 모든 정보가 제거됩니다. 이로 인해 워크로드를 **다시 테스트하지 못할 수 있습니다**.
{% endhint %}

**Terms and conditions**

_The Snyk Container Kubernetes integration uses Red Hat UBI (Universal Base Image)._

_Before downloading or using this application, you must agree to the Red Hat subscription agreement located at redhat.com/licenses. If you do not agree with these terms, do not download or use the application. If you have an existing Red Hat Enterprise Agreement (or other negotiated agreement with Red Hat) with terms that govern subscription services associated with Containers, then your existing agreement will control._
