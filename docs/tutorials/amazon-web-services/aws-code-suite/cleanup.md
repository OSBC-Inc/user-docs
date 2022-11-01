# Cleanup

계정에 요금이 청구되지 않도록 생성된 인프라를 정리하는 것이 좋습니다. 워크샵을 좀 더 검토할 수 있도록 작업을 계속 진행하려는 경우 작업이 완료되면 정리를 수행하는 것을 잊지 마십시오. AWS 계정에서 실행 중인 작업을 그대로 두고 잊어버리고 요금이 발생하는 것은 매우 쉽습니다.

{% hint style="info" %}
CloudFormation 스택을 삭제하기 전에 일부 리소스를 수동으로 삭제해야 하므로 다음 단계를 순서대로 수행하십시오. CloudFormation 스택을 사용하여 한 번에 하나씩 삭제하고 다음 스택을 삭제하기 전에 스택이 제거되었는지 확인합니다..
{% endhint %}

```bash
# Delete S3 Bucket
aws s3 rm s3://$(aws s3api list-buckets --query 'Buckets[?starts_with(Name, `workshoppipeline-artifactbucket`) == `true` ].Name' --output text) --recursive

# Delete Log Group
aws logs delete-log-group --log-group-name ModernizationWorkshop

# Delete ECR Repository
aws ecr delete-repository --repository-name modernization-workshop --force

# Delete CloudFormation Pipeline and ECS Stacks
aws cloudformation delete-stack --stack-name WorkshopPipeline
aws cloudformation delete-stack --stack-name WorkshopECS
```

이제 WorkshopServices 스택을 제거하십시오.

```bash
aws cloudformation delete-stack --stack-name WorkshopServices
```

마지막으로 cloud9 창을 닫고 수동으로 이전 스택의 삭제를 확인하고 최종 스택을 삭제합니다. AWS 콘솔에서 CloudFormation으로 이동합니다. **WorkshopPipeline, WorkshopECS** 및 **WorkshopServices**가 모두 제거되었는지 확인합니다. 확인되면 `ModernizationWorkshop` 스택을 클릭한 다음 `Delete`를 클릭합니다.

Workshop 스택이 CloudFormation에 나열되지 않았는지 확인하고 완료했습니다.
