# 테스트 배포

이제 작업이 성공적으로 실행되었으므로 애플리케이션이 실행 중인지 확인하겠습니다. 이를 위해 `kubectl get svc`를 한 번 더 실행합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/kubectl\_get\_svc\_external-ip.gif)

이번에는 Kubernetes 매니페스트의 배포 및 서비스 구성에 해당하는 **두 가지** **추가 서비스** goof **및** goof-mongo를 볼 수 있습니다. `./deployment/goof-service.yaml`에서 이를 표준 `http` 포트 `80`에서 수신하는 `LoadBalancer` 유형의 `frontend` 앱으로 정의했음을 기억하십시오.

## jq 설치

결과를 복사하여 클립보드에 붙여넣을 수도 있지만 다른 접근 방식을 취하고 일부 명령줄 마법을 사용하여 더 나은 결과를 얻을 수 있습니다. Homebrew를 사용하여 명령줄 JSON 프로세서 [`jq`](https://formulae.brew.sh/formula/jq)를 설치하는 것으로 시작하겠습니다.

```bash
brew update && brew install jq
```

다음으로 환경 변수 `GOOF_HOST`를 만들고 하나의 명령으로 **goof** 서비스에 대한 `EXTERNAL-IP` 값을 전달합니다.

```bash
GOOF_HOST=$(kubectl get svc goof -o json | \
jq -r '.status.loadBalancer.ingress[].hostname')
```

제대로 작동하는지 확인하고 터미널 명령줄에 `echo $GOOF_HOST`를 입력하고 결과를 확인합니다. `EXTERNAL-IP`와 일치하는 반환 값이 표시되어야 합니다. 다음으로 간단한 테스트를 수행하여 애플리케이션이 요청을 처리하는지 확인합니다. 이를 위해 간단한 `curl` 명령을 실행하고 `./public/about.html`을 찾아봅니다. 결과는 다음과 유사해야 합니다:

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/goof\_curl\_about.gif)

원하는 경우 즐겨찾는 웹 브라우저를 시작하고 아래와 같이 `LoadBalancer` 의 `EXTERNAL-IP`로 이동할 수도 있습니다:

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/circleci\_goof.png)
