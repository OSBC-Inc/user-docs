# Goof Sample App 배포

{% hint style="danger" %}
이 샘플 애플리케이션을 프로덕션 환경에 **배포하지 마십시오**.
{% endhint %}

이러한 예를 위해 랩 환경에 배포할 수 있는 샘플 취약한 Node.js 애플리케이션을 제공하고 있습니다. 이 앱은 로컬 개발 머신에 **복제**할 수 있는 [공용 GitHub 저장소](https://github.com/snyk-partners/k8s-goof)에서 사용할 수 있습니다.

터미널에서 저장소를 복제한 위치로 이동하고 다음 명령을 실행합니다:

```bash
 kubectl apply -f goof-service.yaml
```

```bash
kubectl apply -f goof-deployment.yaml
```

성공적으로 배포되면 다음과 같은 결과가 표시됩니다:

```bash
deployment.apps/goof created
deployment.apps/goof-mongo created
```

이 앱의 퍼블릭 엔드포인트에 액세스하려면 다음 명령을 실행하고 **EXTERNAL-IP** 출력을 복사하여 웹 브라우저에 붙여넣으면 됩니다.

```bash
kubectl get svc
```

This step is not necessary for this exercise. You may proceed to the next section.
