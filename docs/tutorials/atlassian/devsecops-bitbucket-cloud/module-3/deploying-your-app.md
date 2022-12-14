# 앱 배포

샘플 [bitbucket-pipelines.yml](https://bitbucket.org/snyk/patterns-library-atlassian-aws/src/08298e9b6d3108d33bd54a4839e92884c79c8597/bitbucket-pipelines.yml#lines-57:79) 파일의 마지막 단계는 Snyk으로 스캔하고 Amazon ECR에 안전하게 저장한 컨테이너 이미지를 가져와 이를 Amazon EKS 클러스터에 배포하는 것입니다.

```yaml
deploy-app: &deploy-app
  - step:
      name: "Deploy application"
      deployment: staging
      script:
        - pipe: atlassian/aws-eks-kubectl-run:1.2.4
          variables:
            AWS_ACCESS_KEY_ID: '$AWS_ACCESS_KEY_ID'
            AWS_SECRET_ACCESS_KEY: '$AWS_SECRET_ACCESS_KEY'
            AWS_DEFAULT_REGION: '$AWS_DEFAULT_REGION'
            CLUSTER_NAME: '$AWS_EKS_CLUSTER'
            KUBECTL_COMMAND: 'apply'
            RESOURCE_PATH: "./deployment/goof-service.yaml"
        - envsubst < ./deployment/goof-deployment-template.yaml > ./deployment/goof-deployment.yaml
        - cat ./deployment/goof-deployment.yaml
        - pipe: atlassian/aws-eks-kubectl-run:1.2.4
          variables:
            AWS_ACCESS_KEY_ID: '$AWS_ACCESS_KEY_ID'
            AWS_SECRET_ACCESS_KEY: '$AWS_SECRET_ACCESS_KEY'
            AWS_DEFAULT_REGION: '$AWS_DEFAULT_REGION'
            CLUSTER_NAME: '$AWS_EKS_CLUSTER'
            KUBECTL_COMMAND: 'apply'
            RESOURCE_PATH: './deployment/goof-deployment.yaml'
```

이 예에서는 [aws-eks-kubectl-run](https://bitbucket.org/atlassian/aws-eks-kubectl-run) 파이프를 활용하여 실행 중인 클러스터에 [서비스](https://bitbucket.org/snyk/patterns-library-atlassian-aws/src/master/deployment/goof-service.yaml) 및 [배포](https://bitbucket.org/snyk/patterns-library-atlassian-aws/src/master/deployment/goof-deployment-template.yaml) 매니페스트를 적용합니다. 여기서는 이전에 정의한 리포지토리 변수 중 일부를 참조하지만 [`envsubst`](https://www.gnu.org/software/gettext/manual/html\_node/envsubst-Invocation.html#index-envsubst) linux 명령을 호출하여 변수 중 하나의 값을 대체합니다.

리포지토리의 `./deployments` 디렉터리에 있는 [goof-deployment-template.yaml](https://bitbucket.org/snyk/patterns-library-atlassian-aws/src/08298e9b6d3108d33bd54a4839e92884c79c8597/deployment/goof-deployment-template.yaml#lines-19) 파일에는 두 개의 변수 `${AWS_ECR_URI}` 및 `${BITBUCKET_COMMIT}`이 포함되어 있으며 이를 docker 태그의 값으로 대체하여 Amazon ECR로 부터 이미지를 가져올 수 있습니다.

```yaml
    spec:
      containers:
        - name: goof
          image: ${AWS_ECR_URI}:${BITBUCKET_COMMIT}
```

[goof-service.yaml ](https://bitbucket.org/snyk/patterns-library-atlassian-aws/src/master/deployment/goof-service.yaml)파일은 `service`를 생성하고 프런트엔드 앱을 `type: LoadBalancer`로 배포하여 표준 `http` 포트 `80`에 노출합니다.

```yaml
apiVersion: v1
kind: Service
metadata:
  name: goof
spec:
  type: LoadBalancer
  ports:
    - protocol: TCP
      port: 80
      targetPort: 3001
      name: "http"
    - protocol: TCP
      port: 9229
      targetPort: 9229
      name: "debug"
  selector:
    app: goof
    tier: frontend
---
apiVersion: v1
kind: Service
metadata:
  name: goof-mongo
spec:
  ports:
    - protocol: TCP
      port: 27017
      targetPort: 27017
      name: "mongo"
  selector:
    app: goof
    tier: backend
```

다음 섹션으로 넘어가겠습니다.
