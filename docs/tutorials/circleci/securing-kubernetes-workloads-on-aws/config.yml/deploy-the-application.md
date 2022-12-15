# 애플리케이션 배포

이제 애플리케이션을 푸시할 준비가 되었습니다. 여기에서 작업 단계가 실행될 환경을 정의할 `aws-eks/python3` [실행기](https://circleci.com/docs/2.0/configuration-reference/#executors-requires-version-21)를 호출합니다.

```yaml
  deploy_app:
    executor: aws-eks/python3
    parameters:
      cluster-name:
        type: string
      docker-image-name:
        type: string
      version-info:
        type: string
      aws-region:
        type: string
        default: ""
    steps:
      - checkout
      - run:
          name: Create deployment manifest
          command: |
            BUILD_DATE=$(date '+%Y%m%d%H%M%S')
            cat deployment/goof-deployment-template.yaml |\
               sed "s|DOCKER_IMAGE_NAME|<< parameters.docker-image-name >>|g"\
                 > deployment/goof-deployment.yaml
      - aws-eks/update-kubeconfig-with-authenticator:
          cluster-name: << parameters.cluster-name >>
          install-kubectl: true
          aws-region: << parameters.aws-region >>
      - kubernetes/create-or-update-resource:
          resource-file-path: "deployment/goof-deployment.yaml"
          get-rollout-status: true
          resource-name: deployment/goof
      - kubernetes/create-or-update-resource:
          resource-file-path: "deployment/goof-service.yaml"
```

이 작업에서는 최근에 만든 이미지를 참조하는 Kubernetes `cluster-name` 및 `docker-image-name`과 같은 몇 가지 [매개 변수](https://circleci.com/docs/2.0/configuration-reference/#parameters-requires-version-21)를 전달합니다. 이 값을 사용하여 Kubernetes 클러스터에 인증하고 Kubernetes 매니페스트의 이미지 값을 [Amazon ECR 저장소 URL](https://docs.aws.amazon.com/AmazonECR/latest/userguide/docker-pull-ecr-image.html) 및 태그로 바꿉니다. 그런 다음 `kubernetes/create-or-update-resources` 명령을 호출하여 배포 및 서비스에 대한 Kubernetes 매니페스트를 적용합니다.
