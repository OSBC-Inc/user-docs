# 레지스트리에 이미지 Push

다음으로 `circleci/aws-ecr orb`를 한 번 더 호출하지만 이번에는 [`build-and-push-image`](https://circleci.com/orbs/registry/orb/circleci/aws-ecr#commands-build-and-push-image) 명령을 호출하여 AWS 계정을 인증하고 이미지를 푸시합니다.

```yaml
  build_and_push_image:
    <<: *defaults
    steps:
      - attach_workspace:
          at: ~/repo
      - setup_remote_docker
      - aws-ecr/build-and-push-image:
          account-url: AWS_ECR_ACCOUNT_URL_ENV_VAR_NAME
          aws-access-key-id: ACCESS_KEY_ID_ENV_VAR_NAME
          aws-secret-access-key: SECRET_ACCESS_KEY_ENV_VAR_NAME
          region: AWS_REGION_ENV_VAR_NAME
          repo: ${CIRCLE_PROJECT_REPONAME}
          create-repo: true
          checkout: true
          dockerfile: Dockerfile
          path: ./submodules/goof/
          tag: ${CIRCLE_SHA1}
```

{% hint style="info" %}
`create-repo`를 `true`로 설정하면 orb는 저장소가 없는 경우 저장소를 생성하지만 후속 작업 실행은 단순히 이미지를 기존 저장소로 업데이트합니다.
{% endhint %}
