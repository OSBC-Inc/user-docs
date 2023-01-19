# 샘플 애플리케이션 배포

{% hint style="danger" %}
프로덕션 환경에서 다음 샘플 애플리케이션을 **배포하지 마십시오**. 이 응용 프로그램은 데모용으로 사용되며 많은 취약점을 포함하고 있습니다. 실습을 완료한 후 **애플리케이션을 즉시 제거**하는 것이 좋습니다.
{% endhint %}

Snyk은 이 실습에 사용할 수 있는 goof라는 데모 애플리케이션을 제공합니다. 원하는 응용 프로그램을 배포할 수 있습니다. **goof** 앱을 배포하려면 다음 명령을 사용하여 저장소를 로컬 환경에 복제합니다:

```bash
git clone https://github.com/snyk-partners/k8s-goof.git
```

다음으로 다음과 같이 디렉터리를 변경하거나 `cd`를 복제한 위치로 변경합니다.

```bash
cd k8s-goof/
```

이렇게 하면 배포에 도움이 되는 일부 Kubernetes 매니페스트를 편리하게 배치한 위치로 이동합니다. 다음 명령을 실행합니다:

```bash
kubectl create namespace goof && \
kubectl apply -f ./manifests -n goof
```

애플리케이션이 준비되는 데 몇 분 정도 걸릴 수 있지만 다음 명령을 사용하여 상태를 확인할 수 있습니다:

```bash
kubectl get pods -n goof
```

이들이 **준비** 상태 `1/1`에 있음을 표시하면 외부 IP를 끌어와 이를 브라우저 창으로 지나 애플리케이션에 액세스할 수 있어야 합니다. 다음 명령을 사용하여 애플리케이션의 외부 IP를 가져올 수 있습니다:

```bash
kubectl get svc -n goof
```
