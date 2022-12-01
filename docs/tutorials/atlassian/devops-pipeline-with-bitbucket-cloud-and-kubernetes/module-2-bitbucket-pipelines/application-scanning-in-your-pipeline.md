# Pipeline의 애플리케이션 스캐닝

bitbucket-pipelines.yml은 파이프라인 빌드 구성을 정의합니다. Pipelines를 처음 사용하는 경우 [여기](https://support.atlassian.com/bitbucket-cloud/docs/get-started-with-bitbucket-pipelines/)에서 시작하는 방법에 대해 자세히 알아볼 수 있습니다.

이 워크숍에서는 워크플로에 매핑된 개별 단계가 포함된 샘플 bitbucket-pipelines.yml 파일을 제공했습니다.

* 코드 빌드
* 도커 이미지 빌드
* 컨테이너 이미지 스캔
* 컨테이너 이미지를 레지스트리에 배포
* Kubernetes 클러스터에 컨테이너 이미지 배포

코드와 컨테이너를 빌드하는 첫 번째 단계부터 살펴보겠습니다:

```yaml
image: atlassian/default-image:2

build-app: &build-app
  - step:
      name: Build and Test
      caches:
        - maven
      script:
        - mvn -B verify --file pom.xml
      after-script:
          # Collect checkstyle results, if any, and convert to Bitbucket Code Insights.
        - pipe: atlassian/checkstyle-report:0.2.0

atlassian-security-scan: &atlassian-security-scan
  - step:
      name: Security Scan
      script:
        # Run a security scan for sensitive data.
        # See more security tools at https://bitbucket.org/product/features/pipelines/integrations?&category=security
        - pipe: atlassian/git-secrets-scan:0.4.3
```

이 예에서는 대표적인 파이프라인을 설명하기 위해 몇 가지 활동을 수행합니다. 첫 번째 단계는 **build-app**이며 주요 목적은 jar 파일을 생성하기 위해 checkstyle로 maven 빌드를 실행하는 것입니다. 다음 단계는 **atlassian-security-scan**으로 제목이 지정되며 Atlassian 파이프를 사용하여 git 보안을 검색합니다. 이 두 단계는 편의를 위해 포함되었으며 일이 제대로 작동하는지 확인하기 위한 모범 사례를 보여줍니다. 워크샵에서 자세한 내용을 다루지는 않을 것이며 관심이 있으시면 검토해 보시기 바랍니다.

다음 블록에는 두 개의 파이프를 사용하여 이미지를 스캔하고 푸시하는 Snyk 스캔이 포함됩니다.

```
snyk-scan-push-image: &snyk-scan-push-image
  - step:
      name: "Push container image"
      services:
        - docker
      script:
        - docker build -t $IMAGE .
#        - docker tag $IMAGE $IMAGE:${BITBUCKET_COMMIT}
        - docker tag $IMAGE $IMAGE:latest
        - pipe: snyk/snyk-scan:0.5.1
          variables:
            SNYK_TOKEN: $SNYK_TOKEN
            LANGUAGE: "docker"
            IMAGE_NAME: $IMAGE
            TARGET_FILE: "Dockerfile"
            CODE_INSIGHTS_RESULTS: "true"
            SEVERITY_THRESHOLD: "high"
            DONT_BREAK_BUILD: "true"
            MONITOR: "true"
        - pipe: atlassian/aws-ecr-push-image:1.1.3
          variables:
            AWS_ACCESS_KEY_ID: '$AWS_ACCESS_KEY_ID'
            AWS_SECRET_ACCESS_KEY: '$AWS_SECRET_ACCESS_KEY'
            AWS_DEFAULT_REGION: '$AWS_DEFAULT_REGION'
            IMAGE_NAME: $IMAGE
#            TAGS: '${BITBUCKET_COMMIT}'
            TAGS: latest
```

스크립트의 첫 번째 부분은 도커 사용자에게 이미 익숙한 명령으로 도커 이미지를 빌드합니다.

다음 블록은 구성 매개변수가 있는 Atlassian Bitbuckets용 [Snyk Scan](https://bitbucket.org/product/features/pipelines/integrations?p=snyk/snyk-scan) 파이프입니다. 파이프 구성에 대한 세부 정보는 온라인에서 볼 수 있지만 사람이 읽을 수 있는 이름을 보면 진행 상황을 쉽게 이해할 수 있습니다. 다음 중 몇 가지를 자세히 살펴보겠습니다.

1. `SNYK_TOKEN` 은 이전에 \[**Bitbucket Configuration]** 모듈에서 정의한 저장소변수로 파이프에 전달되고 있습니다.
2. `PROJECT_FOLDER` 은 프로젝트가 있는 폴더이며 일반적으로 기본값은 `.`이지만 이 예에서는 app/goof로 설정하고 이를 파이프라인의 다른 단계에 아티팩트로 전달하고 있습니다.
3. `CODE_INSIGHTS_RESULTS` 의 기본값은`false` 입니다. 그러나 Snyk 테스트 결과로 [Code Insight 보고서](https://snyk.io/blog/enhanced-security-for-bitbucket-cloud-development/)를 생성하려고 하므로 이를 `true`로 설정했습니다.
4. `SEVERITY_THRESHOLD` 는 제공된 수준 이상의 문제에 대해 보고합니다. 기본값은 `low` 지만 우리의 경우에는 `high` 에만 관심이 있으므로 그에 따라 이 변수를 정의했습니다.
5. `DONT_BREAK_BUILD` 기본값은 `false`이며 이는 예상된 것입니다. 정상적인 상황에서 찾은 문제가 발생하면 빌드를 중단하고 싶을 것입니다. 그러나 이 워크숍의 목적을 위해 값을 `true`로 설정했습니다.

{% hint style="info" %}
풀 리퀘스트에서 **Snyk 보안 스캔**을 실행하고 Atlassian Marketplace의 새로운 Snyk Security Connect 앱을 통해 **Code Insights**에서 결과를 볼 수 있습니다. 시작하기 쉽고 몇 번의 클릭만으로 앱을 설치할 수 있습니다.
{% endhint %}

마지막 블록은 EKS 배포용입니다. 워크숍에 블록을 포함하여 대상 환경에 대한 배포 그림을 완성합니다. 파이프라인은 아래 선언에 따라 명명된 파이프라인에 컨테이너를 자동으로 배포합니다.

```
deploy-image: &deploy-image
  - step:
      name: "Push container image"
      script:
      - pipe: atlassian/aws-eks-kubectl-run:2.2.0
        variables:
          CLUSTER_NAME: $AWS_EKS_CLUSTER
          KUBECTL_COMMAND: 'apply'
          RESOURCE_PATH: 'k8s'
```
