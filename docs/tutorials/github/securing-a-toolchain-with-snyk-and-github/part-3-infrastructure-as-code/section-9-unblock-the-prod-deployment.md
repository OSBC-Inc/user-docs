---
description: Pull Request 차단을 해제할 수 있도록 식별된 중간 심각도 문제를 수정하는 작업을 합니다.
---

# Section 3: PROD 배포 차단 해제

## Step 1: 서비스 정의 YAML 파일의 Issue 수정

프로젝트 문제에서 Snyk은 식별된 문제, 그 영향 및 해결 방법을 호출합니다. 또한 문제가 있는 코드 줄을 강조 표시합니다. 이 경우 현재 정의된 로드 밸런서가 전 세계에 공개되어 있기 때문에 `goof-service.yaml` 파일에서 문제가 식별되었습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-iac-viewissuedetails.png)

로드 밸런서가 외부에 공개되는 것과 같은 일부 시나리오에서는 그것이 클라이언트 대면 웹 애플리케이션이기 때문에 의도적으로 문제를 무시하도록 선택할 수 있습니다. 이 경우 Kubernetes 클러스터가 VPC에 있고 외부 Application Load Balancer가 사용 중이라고 가정해 보겠습니다. 이 Kubernetes 로드 밸런서를 가상 VPC의 CIDR 블록으로 제한합니다.

GitHub Web Editor로 `goof-service.yaml`을 열고 콘텐츠를 다음으로 바꿉니다:

```
apiVersion: v1
kind: Service
metadata:
  name: goof
spec:
  type: LoadBalancer
  loadBalancerSourceRanges:
    - "143.231.0.0/16"
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

준비가 되면 새 Branch를 생성하고 Pull Request를 열어 변경 사항을 제안하세요. 이렇게 하면 이전에 설정한 IaC Verification Workflow가 트리거됩니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-iac-editservice.png)

검사가 완료되면 IaC Workflow의 실행 세부 정보에서 `goof-service.yaml` 파일에 다른 문제가 없음을 알 수 있습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-iac-checkspostfix.png)

계속해서 PR을 Merge하십시오. 이제 개발 Branch에 대한 CI Workflow가 시작됩니다. 완료되면 GitHub Security Code Scanning 결과와 Snyk UI 모두에서 `goof-service.yaml`의 문제가 사라진 것을 확인할 수 있습니다! 잘했습니다!

## Step 2: 배포 매니페스트의 문제 수정

이제 `goof-deployment.yaml` 파일과 4가지 차단 문제에 대해 살펴보겠습니다. 이 파일에는 실제로 두 개의 배포 정의가 포함되어 있습니다. 하나는 데이터베이스용이고 다른 하나는 앱의 프런트엔드용입니다. 네 가지 차단 문제는 실제로 두 배포 모두에 존재하는 두 가지 문제입니다. Snyk UI를 살펴보겠습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-iac-rootissue.png)

첫 번째 문제는 컨테이너가 루트 사용자 제어 없이 실행되고 있음을 나타냅니다. 비슷한 맥락에서 두 번째 문제는 컨테이너가 잠재적으로 불필요한 권한으로 실행되고 있음을 알려줍니다. 컨테이너 사양에 securityContext를 추가하여 이 두 가지 문제를 모두 해결할 수 있습니다.

{% hint style="danger" %}
이것은 실용적인 예입니다. 응용 프로그램에 관리 권한 또는 기타 명시적으로 명시된 권한이 필요할 수 있습니다. 파일을 임의로 변경하기 전에 애플리케이션과 해당 종속성을 파악하십시오. 주의하지 않으면 배포가 중단될 수 있습니다.
{% endhint %}

SecurityContext를 `runAsNonRoot`로 설정하면 컨테이너가 0이 아닌 UID를 가진 사용자와 함께 실행되어야 하며 기능을 삭제하면 컨테이너가 클러스터와 상호 작용하는 방식이 제한됩니다. GitHub Web Editor를 사용하여 두 배포에 대한 goof-deployment 파일의 `spec`을 수정합니다.

### App Container에 Security Contex 추가

```
spec:
  containers:
    - name: goof-app
      image: goof:PROD
      ports:
        - containerPort: 3001
        - containerPort: 9229
      env:
        - name: DOCKER
          value: "1"
      securityContext:
        runAsNonRoot: true
        capabilities:
          drop: 
            - all
```

### DB Container에 Security Context 추가

```
spec:
  containers:
    - name: goof-mongo
      image: mongo
      ports:
       - containerPort: 27017
      securityContext:
        runAsNonRoot: true
        capabilities:
          drop:
            - all
```

{% hint style="warning" %}
It's possible to set securityContext for both the Pod and the Containers it runs. In this case, we're setting securityContext for the containers. Learn more in the [Kubernetes Documentation](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/).
{% endhint %}

Merge the changes into the `develop` branch and wait for the CI workflows to run. Like before, the issue counts will be updated in both GitHub Security Code Scanning and the Snyk UI.

## Step 3: Merge our changes into PROD

Back in Section 7, our Snyk Gate blocked the Pull Request we creates from `develop` into `PROD`. Now that we've fixed the issues in our files, back in the Pull Request, we can appreciate that our tests re-ran and this time the Snyk Security Gate is pleased with the changes we made.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-iac-prodprcheckspass.png)

With this assurance, we can merge our changes into PROD. Once merged, our CI workflows will re-run for `PROD`. If we had a workflow to re-deploy our application, it would also run.

That's it! You reached the end of this lab! Check out the next section to recap what you accomplished.
