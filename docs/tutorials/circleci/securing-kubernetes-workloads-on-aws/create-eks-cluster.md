# EKS Cluster 생성

AWS에서 [Amazon EKS (Amazon Elastic Kubernetes Service)](https://aws.amazon.com/eks/) 클러스터를 생성하는 데 사용할 수 있는 몇 가지 옵션이 있습니다. 그 중에는 다음이 있습니다:

* [모듈식 및 확장 가능한 Amazon EKS 아키텍처](https://aws.amazon.com/quickstart/architecture/amazon-eks/) 참조 배포는 AWS 솔루션 설계자가 개발했습니다.
* CircleCI [`aws-eks`](https://circleci.com/orbs/registry/orb/circleci/aws-eks#jobs-create-cluster) 의Orb.
* `eksctl` 명령줄 도구.

이러한 연습의 목적을 위해 `eksctl`로 충분합니다. 클러스터를 만들려면 다음 명령을 실행합니다:

```bash
eksctl create cluster \
--name snyk-circleci-eks \
--version 1.16 \
--region us-west-2
```

{% hint style="info" %}
us-west-2를 모든 [Amazon EKS Fargate 지원 리전](https://docs.aws.amazon.com/eks/latest/userguide/fargate.html)으로 교체할 수 있습니다. 그러나 후속 지침에서 참조할 이름을 바꾸지 마십시오.
{% endhint %}

클러스터가 프로비저닝되는 데 약 15분이 걸릴 수 있습니다. 클러스터가 준비되면 `kubectl get svc`를 실행하고 결과를 볼 수 있습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/kubectl\_get\_svc.gif)
