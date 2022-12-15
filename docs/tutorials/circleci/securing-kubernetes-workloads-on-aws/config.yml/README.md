# config.yml

## CircleCI 구성 워크스루

{% hint style="info" %}
CircleCI orbs는 반복되는 구성 부분을 한 줄의 코드로 압축하는 재사용 가능한 YAML 구성 패키지입니다. orb를 사용하는 이유에 대해 자세히 알아보거나 [여기](https://circleci.com/orbs/)에서 사용 사례를 살펴보세요.
{% endhint %}

### 기본 사항

우리는 [`version`](https://circleci.com/docs/2.0/configuration-reference/#version)을 [Config Reference 2.1](https://circleci.com/docs/reference-2-1/#section=configuration)로 정의했으며 작업에 활용하려는 [`orbs`](https://circleci.com/docs/2.0/configuration-reference/#orbs-requires-version-21)를 정의했습니다. 우리는 다음 orb를 사용할 것입니다:

* Kubernetes용 Amazon EKS(Amazon Elastic Container Service) 작업을 위한 [`aws-eks`](https://circleci.com/orbs/registry/orb/circleci/aws-eks).
* 이미지를 빌드하고 Amazon Elastic Container Registry로 푸시하는 [`aws-ecr`](https://circleci.com/orbs/registry/orb/circleci/aws-ecr).
* CircleCI에서 Kubernetes로 작업하기 위한 도구 모음인 [`kubernetes`](https://circleci.com/orbs/registry/orb/circleci/kubernetes).
* [`snyk`](https://circleci.com/orbs/registry/orb/snyk/snyk)을 사용하여 앱 종속성 및 도커 이미지에서 알려진 취약점을 찾고 수정하고 모니터링합니다.

```yaml
version: 2.1

orbs:
  aws-eks: circleci/aws-eks@0.2.7
  aws-ecr: circleci/aws-ecr@6.8.2
  kubernetes: circleci/kubernetes@0.11.0
  snyk: snyk/snyk@0.0.10

defaults: &defaults
  docker:
    - image: circleci/node:9.11.2
  working_directory: ~/repo
```

효율성을 위해 나중에 작업에서 호출할 프로젝트에 대한 몇 가지 기본값도 정의했습니다.

{% hint style="info" %}
대부분의 사용 사례를 해결하기 위해 여러 인증 및 파트너 오브에 대해 [CircleCI 레지스트리](https://circleci.com/orbs/registry/)를 검색할 수 있다는 사실을 알고 계셨습니까?
{% endhint %}

### Workflows

예제 `config.yml` 파일도 [`workflows`](https://circleci.com/docs/2.0/configuration-reference/#workflows)를 사용하여 정의된 작업을 구성하고 오케스트레이션합니다.

```yaml
workflows:
  build_and_deploy:
    jobs:
      - test_app
      - scan_app:
          requires:
            - test_app
      - build_and_scan_image:
          requires:
            - scan_app
      - build_and_push_image:
          requires:
            - build_and_scan_image
      - deploy_app:
          cluster-name: ${CIRCLE_PROJECT_REPONAME}
          aws-region: ${AWS_REGION_ENV_VAR_NAME}
          docker-image-name: "$AWS_ECR_ACCOUNT_URL_ENV_VAR_NAME/${CIRCLE_PROJECT_REPONAME}:${CIRCLE_SHA1}"
          version-info: "${CIRCLE_SHA1}"
          requires:
            - build_and_push_image
```
