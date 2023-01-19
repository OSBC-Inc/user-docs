# 컨테이너 이미지 빌드

## 배경

**Securing AKS with Snyk**에서는 Microsoft AKS(Azure Kubernetes Service)에서 실행되는 Kubernetes 클러스터에 애플리케이션을 배포했습니다. 매니페스트 템플릿 파일을 사용하여 배포했습니다. [매니페스트](https://kubernetes.io/docs/concepts/cluster-administration/manage-deployment/)는 배포를 단순화하는 리소스 구성을 구성하는 수단을 제공합니다. azure-vote.yaml을 검사하면 백 엔드 및 프런트 엔드 애플리케이션에 대한 컨테이너 이미지를 각각 pull `redis` 및 `microsoft/azure-vote-front:v1`로 정의하고 있음을 알 수 있습니다.

나중에 Kubernetes Workload를 스캔했을 때 Kubernetes 보안 구성과 컨테이너 이미지에서 취약점을 발견했습니다. 감지된 보안 구성 문제를 수정할 수 있었습니다. 그러나 컨테이너 이미지를 조사했을 때 다음 경고를 발견했습니다:

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk\_scan\_06.png)

이 모듈에서는 컨테이너 이미지를 빌드하고 ACR과 같은 개인 레지스트리에 저장하고 Snyk로 해당 레지스트리를 모니터링하기 위한 몇 가지 모범 사례를 다룹니다.

## Docker 이미지 빌드

Snyk의 [오픈 소스 보안 상태 보고서 – 2019](https://snyk.io/blog/top-ten-most-popular-docker-images-each-contain-at-least-30-vulnerabilities/)에서 우리는 Docker Hub 웹사이트에 소개된 많은 인기 있는 Docker 컨테이너가 많은 알려진 취약점이 포함된 번들 이미지를 발견했습니다. 주제에 대해 자세히 알아보려면 이 보고서와 최신 블로그인 [10가지 Docker 이미지 보안 모범 사례](https://snyk.io/blog/10-docker-image-security-best-practices/)를 읽어 보시기 바랍니다. 다음 연습은 이러한 모범 사례와 일치하며 최소한의 이미지 개념부터 시작하여 단계적으로 다룰 것입니다.

### Dockerfile

백엔드 애플리케이션부터 시작하겠습니다. 매니페스트에서 [Redis](https://hub.docker.com/\_/redis)용 [Docker Official 이미지](https://docs.docker.com/docker-hub/official\_repos/)를 사용하고 있음을 알 수 있습니다. Dockerfile에서 새로운 이미지를 빌드하고 ACR의 개인 레지스트리에 저장하여 보안 태세를 개선하는 첫 번째 단계를 수행할 것입니다.

터미널에서 `pwd`를 입력하고 결과에 `$HOME/snyk-azure-resources/`가 표시되는지 확인하여 복제된 리포지토리의 루트에 있는지 확인합니다. 우리 리포지토리에는 Dockerfile을 포함하는 공식 redis 이미지의 소스를 가리키는 [`submodule`](https://git-scm.com/book/en/v2/Git-Tools-Submodules)이 포함되어 있습니다. 하위 모듈을 동기화하려면 다음 명령을 입력하십시오:

```bash
git submodule update --recursive
```

그런 다음 다음 명령을 입력하여 디렉토리를 변경해 보겠습니다:

```bash
cd app/redis/6.0/
```

여기에서 간단한 `ls -a` 명령으로 내용이 표시되고 해당 디렉터리에 Dockerfile이 표시됩니다. [Microsoft Visual Studio Code](https://code.visualstudio.com/)와 같은 선호하는 편집기에서 이 파일을 열고 내용을 검토할 수 있습니다. 맨 위 몇 줄은 다음과 유사해야 합니다:

```
FROM debian:buster-slim

# add our user and group first to make sure their IDs get assigned consistently, regardless of whatever dependencies get added
RUN groupadd -r -g 999 redis && useradd -r -g redis -u 999 redis
```

이 `Dockerfile`은 나중에 다시 다루겠지만 지금은 기본 이미지가 `debian:buster-slim`이라는 점에 유의하세요.

### Docker 빌드

이제 `app/redis/6.0/` 디렉터리에서 제공된 Dockerfile을 사용하여 자체 컨테이너 이미지를 빌드하고 태그를 지정합니다. 이를 위해 다음과 같이 [`docker build`](https://docs.docker.com/engine/reference/commandline/build/) 명령을 실행합니다:

```bash
docker build -t my-redis:v1 .
```

성공적으로 완료되면 다음과 유사한 결과가 표시됩니다.:

```
Successfully built aa8130687a13
Successfully tagged my-redis:v1
```

### Docker tag

초기 이미지를 Azure Container Registry에 Push할 준비가 거의 되었습니다. 그러나 진행하기 전에 몇 가지 [`docker tag`](https://docs.docker.com/engine/reference/commandline/tag/) 명령을 실행하여 ACR 로그인 서버의 정규화된 이름으로 이미지에 태그를 지정해야 합니다. `docker tag` 명령 내에서 Azure CLI를 사용하여 ACR 로그인 서버의 값을 쿼리하여 이를 흥미롭게 만들 것입니다. 이를 위해 `az acr show`를 호출하고 레지스트리 이름을 지정하면서 일반 텍스트에 대한 `-o tsv` 매개 변수로 출력 형식을 지정합니다.

```bash
docker tag my-redis:v1 $(az acr show --name mySnykContainerRegistry --query loginServer --output tsv)/my-redis:v1
```

We tagged the first with a `version` and we will tag it a second time with `latest`.

첫 번째를 `version` 태그로 지정하고 `latest` 태그를 두 번째로 지정합니다.

```bash
docker tag my-redis:v1 $(az acr show --name mySnykContainerRegistry --query loginServer --output tsv)/my-redis:latest
```

이제 빠른 [`docker images`](https://docs.docker.com/engine/reference/commandline/images/)를 실행하고 모든 항목이 올바르게 태그 지정되었는지 확인합니다.

```
REPOSITORY                                                      TAG                 IMAGE ID            CREATED             SIZE
my-redis                                                        v1                  aa8130687a13        4 hours ago         104MB
mysnykcontainerregistry.azurecr.io/my-redis                     latest              aa8130687a13        4 hours ago         104MB
mysnykcontainerregistry.azurecr.io/my-redis                     v1                  aa8130687a13        4 hours ago         104MB
debian                                                          buster-slim         e5aad4204d00        7 days ago          69.2MB
```

### Docker push

해냈습니다. 이제 태그가 지정된 이미지에서 [`docker push`](https://docs.docker.com/engine/reference/commandline/push/)를 실행하고 ACR에 저장할 준비가 되었습니다. 첫 번째 태그가 지정된 이미지 `v1`부터 시작하겠습니다:

```bash
 docker push $(az acr show --name mySnykContainerRegistry --query loginServer --output tsv)/my-redis:v1
```

아래와 비슷한 출력이 표시되어야 합니다:

```
The push refers to repository [mysnykcontainerregistry.azurecr.io/my-redis]
555634e64cd8: Pushed
12534748095c: Pushed
ea013d725bd6: Pushed
63689ea7c92e: Pushed
2c2aedafe0c2: Pushed
c2adabaecedb: Pushed
v1: digest: sha256:f8e1a610528d3fbd6f1b26fc2a2610c05fd07938b68e8aef7cb87ef1c9a6ec65 size: 1573
```

다음으로 두 번째로 태그가 지정된 `latest` 이미지입니다:

```bash
docker push $(az acr show --name mySnykContainerRegistry --query loginServer --output tsv)/my-redis:latest
```

아래와 비슷한 출력이 표시되어야 합니다:

```
555634e64cd8: Layer already exists
12534748095c: Layer already exists
ea013d725bd6: Layer already exists
63689ea7c92e: Layer already exists
2c2aedafe0c2: Layer already exists
c2adabaecedb: Layer already exists
latest: digest: sha256:f8e1a610528d3fbd6f1b26fc2a2610c05fd07938b68e8aef7cb87ef1c9a6ec65 size: 1573
```

또한 Azure CLI를 통해 쿼리하여 레지스트리에 실제로 푸시되었는지 확인할 수도 있습니다:

```bash
az acr repository list --name mySnykContainerRegistry --output json
```

아래와 비슷한 출력이 표시되어야 합니다:

```
[
  "my-redis"
]
```

`my-redis` 저장소의 태그 목록이 푸시한 것과 일치하는지 확인하려면 다음 명령을 실행할 수 있습니다:

```bash
az acr repository show-tags --name mySnykContainerRegistry --repository my-redis --output table
```

아래와 비슷한 출력이 표시됩니다:

```
Result
--------
latest
v1
```

물론 Azure Portal에서도 동일한 결과를 볼 수 있습니다:

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/acr\_repository\_01.png)
