---
title: Cleanup
chapter: true
weight: 100
---

# 깔끔하게 정리

## AWS Cleanup

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/hardhat.png)

{% hint style="danger" %}
귀하의 계정에 요금이 부과되지 않도록 생성된 인프라를 정리하는 것이 좋습니다. 작업장을 좀 더 조사할 수 있도록 작업을 계속 실행하려는 경우 작업이 완료되면 정리 작업을 수행하는 것을 잊지 마십시오. AWS 계정에서 실행 중인 항목을 그대로 두고 잊은 다음 요금이 발생하기가 매우 쉽습니다.
{% endhint %}

AWS 콘솔에서 [**CloudFormation**](https://us-west-2.console.aws.amazon.com/cloudformation/home?region=us-west-2)으로 이동하고 다음을 클릭합니다:

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/aws-account-cleanup.png)

1. `Snyk-Security-ECR` 스택을 누른 다음 `Delete`합니다.
2. `Amazon-EKS-with-Snyk` 스택 및 `Delete`.

**Nested** 태그가 있는 워크샵용 스택을 선택할 필요가 없으며 `Amazon-EKS-with-Snyk` 스택과 함께 자동으로 삭제됩니다.

{% hint style="warning" %}
이 프로세스는 `Amazon-EKS-with-Snyk` 또는 `Snyk-Security-ECR` 스택이 CloudFormation에 나열되어 있지 않은지 확인하기 위해 15-30분이 소요되며 작업이 완료됩니다.
{% endhint %}
