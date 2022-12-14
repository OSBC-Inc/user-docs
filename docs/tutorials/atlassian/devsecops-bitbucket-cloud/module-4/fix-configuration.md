# 구성 수정

Snyk 앱에서 각 통합을 확장하고 프로젝트를 전체적으로 볼 수 있는 **Projects** 메뉴로 이동합니다. 여기서는 Amazon EKS 클러스터에서 _**Kubernetes deployment**_를 선택합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-projects-03.png)

여기에서 애플리케이션이 클러스터에 배포되었지만 여러 _보안 컨텍스트_ 속성이 잘못 구성되었거나 전혀 구성되지 않았음을 알 수 있습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-eks-integration-03.png)

가져온 Bitbucket 프로젝트로 돌아가서 `goof-deployment-template.yaml` 파일 결과를 검토하면 이러한 Issues에 대한 추가 컨텍스트를 볼 수 있습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-k8s-report.png)

이 문제를 해결하려면 매니페스트에 `securityContext`를 추가하고 이러한 속성을 명시적으로 정의하면 됩니다. 다음 블록을 매니페스트 파일에 복사합니다.

```yaml
          securityContext:
            allowPrivilegeEscalation: false
            readOnlyRootFilesystem: true
            runAsNonRoot: true
            capabilities:
              drop:
                - all
```

다시 한 번 Bitbucket 리포지토리로 이동하고 Bitbucket의 기본 제공 편집기로 `./deployment/goof-deployment-template.yaml`을 편집하여 다음과 같이 표시해 보겠습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/bitbucket-edit-manifest.png)

**Commit**을 클릭합니다.
