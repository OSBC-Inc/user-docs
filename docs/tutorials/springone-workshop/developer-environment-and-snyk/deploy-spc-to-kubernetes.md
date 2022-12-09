# Snyk으로 Kubernetes 파일 검사

## Kubernetes 파일 검증 및 Kubernetes에 SPC 배포

Snyk CLI를 사용하여 Kubernetes 파일이 개발자 환경의 보안 정책을 충족하고 있는지 확인해 보겠습니다. 현재 SPC 애플리케이션의 루트 폴더에 있다고 가정하고 이 명령을 실행합니다. 출력에는 Snyk이 발견한 모든 보안 Issue와 Kubernetes 파일을 수정하는 방법에 대한 제안이 표시됩니다.

### SPC Kubernetes YAML 파일 테스트

```
snyk iac test kubernetes/petclinic-deployment.yaml
```

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/screen-shot-2020-08-26-at-2.54.26-pm.png)

{% hint style="info" %}
이 스캔은 즉시 수행됩니다.
{% endhint %}

## Kubernetes에 SPC 배포

Kubernetes 파일의 빠른 검증 후 개발자 경험을 완료해 보겠습니다. Helm 기반 MySQL 인스턴스와 SPC 애플리케이션을 배포할 것입니다. 배포가 완료되면 배포를 검증하기 위한 간단한 요청을 보냅니다.

lab VM은 SPC 애플리케이션을 배포하기 위해 Kubernetes 클러스터로 구성됩니다. Kubectl (k) 및 Helm (h)에 대한 alias 명령을 만들어 일일이 타이핑하지 않아도 됩니다. 우리는 또한 demo라는 네임스페이스를 사용하고 있습니다.

### Kubernetes 네임스페이스 생성

```
k create namespace demo
```

### MySQL 데이터베이스 배포

```
h install petclinic-db --set mysqlDatabase=petclinic stable/mysql --namespace demo
```

### SPC Kubernetes 배포

```
k -n demo apply -f kubernetes/petclinic-deployment.yaml
```

```
k -n demo apply -f kubernetes/petclinic-svc-nodeport.yaml
```

### SPC 애플리케이션 테스트

lab view 상단에 있는 SPC 버튼을 사용하여 배포를 검증합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/spc\_button\_purpcle\_cicle.png)

모든 구성이 올바르다고 가정하면 SPC 버튼이 SPC 홈페이지를 표시합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/screen-shot-2020-08-28-at-3.57.03-pm.png)
