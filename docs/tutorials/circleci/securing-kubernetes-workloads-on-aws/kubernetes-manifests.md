# Kubernetes manifests

애플리케이션을 간단하게 배포하기 위해 애플리케이션을 실행하는 데 필요한 리소스를 생성하는 두 개의 [구성 파일](https://kubernetes.io/docs/concepts/configuration/overview/)을 제공했습니다. 이 두 파일은 배포 및 서비스로 구성되며 함께 제공되는 GitHub 저장소의 `./deployment` 디렉터리에서 사용할 수 있습니다. 각 구성 파일에 무엇이 있는지 살펴보겠습니다.

## 배포

[배포](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)는 원하는 상태를 정의하고 ReplicaSet를 생성합니다. 여기에서 사용할 컨테이너 이미지와 cpu 및 메모리 제한을 정의합니다.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: goof
spec:
  replicas: 1
  selector:
    matchLabels:
      app: goof
      tier: frontend
  template:
    metadata:
      labels:
        app: goof
        tier: frontend
    spec:
      containers:
        - name: goof
          image: DOCKER_IMAGE_NAME
          resources:
            requests:
              cpu: 100m
              memory: 100Mi
          ports:
            - containerPort: 3001
            - containerPort: 9229
          env:
            - name: DOCKER
              value: "1"
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: goof-mongo
spec:
  replicas: 1
  selector:
    matchLabels:
      app: goof
      tier: backend
  template:
    metadata:
      labels:
        app: goof
        tier: backend
    spec:
      containers:
        - name: goof-mongo
          image: mongo
          ports:
            - containerPort: 27017
```

## 서비스

[서비스](https://kubernetes.io/docs/concepts/services-networking/service/)는 포드 세트에서 실행 중인 애플리케이션을 네트워크 서비스로 노출하기 위한 추상화입니다. 여기에서 우리는 goof 애플리케이션인 프런트엔드와 우리의 경우 mongodb 컨테이너 이미지가 될 백엔드로 구성된 2계층 애플리케이션을 정의하고 있습니다.

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
