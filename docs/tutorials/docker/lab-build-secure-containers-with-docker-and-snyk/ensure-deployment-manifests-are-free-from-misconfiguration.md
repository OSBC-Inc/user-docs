# 배포 매니페스트에 구성 오류가 없는지 확인

이전 섹션에서는 컨테이너 기본 이미지와 애플리케이션 종속성에 의해 도입된 취약성을 수정하고 Kubernetes에 배포하여 변경 사항을 테스트했습니다.

취약점이 0개라도 애플리케이션의 배포 매니페스트가 작성되는 방식에 따라 위험에 노출될 수 있습니다. 이 섹션에서는 Snyk을 사용하여 해당 파일에서 문제를 찾아 수정합니다.

## 배포 매니페스트의 문제 조사

이전에 가져온 Snyk 프로젝트에서 goof 애플리케이션에 대한 두 개의 Kubernetes 매니페스트를 볼 수 있습니다. 하나는 애플리케이션을 배포하고 다른 하나는 필요한 mongo 데이터베이스를 배포합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-iac-dockerlab.png)

이 중 하나를 클릭하면 Snyk이 파일에서 식별한 구성 위험이 발생합니다. `goof-mongo-deployment.yaml` 파일부터 다음과 같은 문제가 나타납니다:

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/goof-mongo-issues.png)

각 문제에 대해 Snyk은 식별된 문제, 그 영향 및 해결 방법을 호출합니다. 또한 Issue가 있는 코드 줄을 강조 표시합니다. 아래 예에서는 배포에 `ImagePullPolicy`를 추가하여 해결할 수 있는 낮은 심각도 구성 위험을 볼 수 있습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/iac-pullpolicyissue.png)

이 정보를 사용하여 개발자는 문제를 무시하거나 배포 매니페스트에 필요한 변경을 수행하여 Issue를 해결할 수 있습니다.

{% hint style="danger" %}
다음은 예입니다. 응용 프로그램에 관리 권한 또는 기타 명시적으로 명시된 권한이 필요할 수 있습니다. 파일을 변경하기 전에 애플리케이션과 해당 종속성을 파악하십시오. 주의하지 않으면 배포를 중단할 수 있습니다.
{% endhint %}

## 배포 매니페스트의 구성 Issue 수정

경고 상태에서 구성 Issue는 매우 미묘합니다. 우리가 확인하는 문서화된 모범 사례가 있지만 워크로드가 올바르게 작동하려면 그러한 모범 사례가 필요할 수 있습니다. 이러한 이유로 Snyk이 실행하는 [구성 검사의 심각도를 변경](https://support.snyk.io/hc/en-us/articles/360006402818#UUID-c1919782-6bfa-b84b-a638-3913cee39fc5)할 수 있습니다.

이 예에서는 수정이 필요하다고 판단되는 몇 가지 문제를 수정합니다.

### Issue: 컨테이너가 오래된 이미지로 실행될 수 있음

위의 Issue를 다시 한 번 살펴 보겠습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/iac-pullpolicyissue.png)

Issue 설명을 읽으면 컨테이너 사양에 `ImagePullPolicy` 특성을 추가하여 이 Issue를 해결할 수 있습니다. IDE 또는 텍스트 편집기에서 속성을 `goof-mongo-deployment.yaml`에 추가합니다.

```yaml
spec:
  containers:
    - image: mongo
      name: goof-mongo
      imagePullPolicy: Always
      ports:
```

### Issue: 컨테이너가 루트 사용자 제어 없이 실행 중입니다.

다른 문제를 봅시다. 이번에는 컨테이너에 부여된 권한과 관련이 있습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/iac-runasnoonroot.png)

이것은 `container`에 `securityContext`를 설정하여 수정할 수 있습니다. 이를 설정하려면 `goof-deployment-mongo.yaml` 파일에 다음을 추가하십시오.

```yaml
spec:
  containers:
    - image: mongo
      name: goof-mongo
      imagePullPolicy: Always
      securityContext:
        runAsNonRoot: true
```

## 구성 파일을 테스트하여 작동하는지 확인하십시오.

구성 파일을 로컬에서 변경할 때마다 변경 사항을 GitHub에 Commit하기 전에 로컬에서 테스트하는 것이 좋습니다. 네임스페이스를 삭제하여 현재 배포를 해제합니다:

```yaml
kubectl delete ns snyk-docker
```

제거되면 다음 명령을 사용하여 애플리케이션을 다시 배포합니다.

```yaml
# Create a namespace
kubectl create ns snyk-docker

# Set the current context to use the new namespace
kubectl config set-context --current --namespace snyk-docker

# Spin up the goof deployment and service
kubectl create -f goof-deployment.yaml,goof-mongo-deployment.yaml
```

제대로 회전하면 [http://localhost:3001](http://localhost:3001/)로 이동하여 앱을 테스트합니다. 작동하는지 확인한 후 변경 사항을 GitHub에 Commit하십시오! Snyk은 파일을 다시 테스트하고 업데이트된 Issue 수를 표시합니다.

You reached the end! We hope you enjoyed it. Check out [Recap and Next Steps](recap-and-next-steps.md) for extra resources.

학습이 끝났습니다! 이 학습이 즐거웠기를 바랍니다. 추가 리소스는 [요약 및 다음 단계](recap-and-next-steps.md)를 확인하십시오.
