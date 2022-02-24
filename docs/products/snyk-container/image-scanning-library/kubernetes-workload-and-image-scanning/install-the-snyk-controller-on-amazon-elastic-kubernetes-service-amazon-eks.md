# Amazon Elastic Kubernetes Service (Amazon EKS)에 Snyk 컨트롤러 설치

Snyk 컨트롤러를 설치하면 실행 중인 EKS 워크로드를 가져오고 테스트할 수 있으며, 관련 이미지 및 구성에서 이러한 워크로드의 보안을 떨어뜨릴 수 있는 취약성을 식별할 수 있습니다. 가져온 후에도 Snyk는 이러한 워크로드를 계속 모니터링하여 새로운 이미지가 배포되고 워크로드 구성이 변경됨에 따라 추가적인 보안 문제를 파악합니다.

### [Open the AWS Quick Start Guide](https://aws.amazon.com/quickstart/architecture/eks-snyk/)

Amazon EKS용 Snyk 컨트롤러를 [AWS Quick Start](https://aws.amazon.com/quickstart/architecture/eks-snyk/)로 배포할 수 있습니다. 이 옵션을 사용하면 수동으로 구성할 필요가 없습니다. 기본 파라미터를 사용하여 Quick Start를 기존 Amazon EKS 클러스터에 배포하면 다음과 같은 환경이 구축됩니다.

![](<../../../../.gitbook/assets/architecture (1).png>)

일반적으로 사용하는 세 가지 배포 옵션은 다음과 같습니다.

**1.** AWS계정에서 Amazon EKS 클러스터를 이미 실행중인 경우

[![cloudformation-launch-stack.png - REPLACE THIS IMAGE - ZENDESK IMAGE - UPDATE ME!](../../../../.gitbook/assets/cloudformation-launch-stack.png)](https://us-east-2.console.aws.amazon.com/cloudformation/home?region=us-east-2#/stacks/create/template?stackName=Snyk-EKS\&templateURL=https://aws-quickstart.s3.us-east-1.amazonaws.com/quickstart-amazon-eks/submodules/quickstart-eks-snyk/templates/eks-snyk.template.yaml)

**2.** Amazon VPC(Amazon Virtual Private Cloud)가 이미 존재하지만 클러스터에 Snyk 컨트롤러가 배포된 Amazon EKS 클러스터가 필요한 경우

[![cloudformation-launch-stack.png - REPLACE THIS IMAGE - ZENDESK IMAGE - UPDATE ME!](../../../../.gitbook/assets/cloudformation-launch-stack.png)](https://us-east-2.console.aws.amazon.com/cloudformation/home?region=us-east-2#/stacks/create/template?stackName=Amazon-EKS-with-Snyk\&templateURL=https://aws-quickstart.s3.us-east-1.amazonaws.com/quickstart-amazon-eks/templates/amazon-eks-master-existing-vpc.template.yaml)

**3.** Amazon VPC 또는 Amazon EKS 클러스터가 없고 클러스터에 Snyk 컨트롤러가 배포된 모든 서비스가 필요한 경우

[![cloudformation-launch-stack.png - REPLACE THIS IMAGE - ZENDESK IMAGE - UPDATE ME!](../../../../.gitbook/assets/cloudformation-launch-stack.png)](https://us-east-2.console.aws.amazon.com/cloudformation/home?region=us-east-2#/stacks/create/template?stackName=Amazon-EKS-with-Snyk\&templateURL=https://aws-quickstart.s3.us-east-1.amazonaws.com/quickstart-amazon-eks/templates/amazon-eks-master-existing-vpc.template.yaml)

## 전제 조건

{% hint style="info" %}
**기능 사용 여부**\
이 기능은 모든 유료 플랜에서 사용할 수 있습니다. 자세한 내용은 [pricing plans](https://snyk.io/plans/)를 참조하세요.
{% endhint %}

* Snyk 조직의 관리자 계정이여야 합니다.
* 최소 50GB의 스토리지를 클러스터에서 [emptyDir](https://kubernetes.io/docs/concepts/storage/volumes/#emptydir) 형식으로 사용할 수 있어야 합니다.
* Kubernetes 클러스터는 HTTPS를 통해 Snyk outbound와 통신할 수 있어야 합니다.
* EKS(Amazon Elastic Kubernetes Services) 클러스터에 통합하도록 Snyk을 구성할 때 ECR(Amazon Elastic Container Registry)에 호스팅된 이미지를 검색하려는 경우 Quick Start, [Snyk Security on AWS](https://aws.amazon.com/quickstart/architecture/snyk-security/)를 배포하여 이 통합을 사용하도록 설정할 수 있습니다.

![](../../../../.gitbook/assets/snyk\_rocket.png)

## [Deployment Guide](https://aws-quickstart.github.io/quickstart-eks-snyk/)

## ECR에서 이미지를 가져오고 스캔하는 snyk-monitor 구성

위의 모든 옵션에 대해 [여기](https://docs.aws.amazon.com/AmazonECR/latest/userguide/ECR\_on\_EKS.html)서 확인할 수 있는 **IAM 정책을 EKS 작업자 노드에 추가**하여 해당 작업자 노드에서 실행할 때 snyk-monitor가 개인 이미지를 가져올 수 있도록 합니다.

IAM 역할을 노드 그룹에 할당하지 않으려면 서비스 계정에 IAM 역할을 사용하고 다음과 같이 snyk-monitor를 구성할 수 있습니다.

* 서비스 계정의 IAM 역할을 설정합니다. [IAM role for a Service Accounts](https://docs.aws.amazon.com/eks/latest/userguide/iam-roles-for-service-accounts.html)
* snyk-monitor에 마운트된 EKS 자격 증명의 `fsGroup`을 `nobody` (uid `65534`)사용자로 수정합니다.
* IAM 역할로 snyk-monitor 서비스 계정에 주석을 입력합니다.

```
helm upgrade --install snyk-monitor snyk-charts/snyk-monitor \
             --namespace snyk-monitor \
             --set securityContext.fsGroup=65534 \
             --set rbac.serviceAccount.annotations."eks.amazonaws.com/role-arn"="<iam role name>" \
             --set volumes.projected.serviceAccountToken=true
```

**NOTE:** 배포하기 전에 [_parameter reference_](https://github.com/aws-quickstart/quickstart-eks-snyk#parameter-reference)를 검토하세요.
