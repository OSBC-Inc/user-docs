# 컨테이너 이미지 스캐닝

다음으로 [`circleci/aws-ecr`](https://circleci.com/orbs/registry/orb/circleci/aws-ecr)를 호출하여 프로젝트 저장소의 `Dockerfile`에서 이미지를 빌드하고 [`snyk/scan`](https://circleci.com/orbs/registry/orb/snyk/snyk#commands-scan) 명령을 호출하여 기본 이미지에서 취약성을 찾습니다. 다시 한 번 여기에서 `fail-on-issues`를 `false`로 설정하고 `severity-threshold`를 `high`로 설정하는 것과 같은 몇 가지 선택을 했습니다.

```yaml
  build_and_scan_image:
    <<: *defaults
    steps:
      - attach_workspace:
          at: ~/repo
      - setup_remote_docker
      - aws-ecr/build-image:
          account-url: AWS_ECR_ACCOUNT_URL_ENV_VAR_NAME
          dockerfile: Dockerfile
          path: ./submodules/goof/
          repo: ${CIRCLE_PROJECT_REPONAME}
          tag: ${CIRCLE_SHA1}
      - snyk/scan:
          docker-image-name: '$AWS_ECR_ACCOUNT_URL_ENV_VAR_NAME/${CIRCLE_PROJECT_REPONAME}:${CIRCLE_SHA1}'
          fail-on-issues: false
          monitor-on-build: true
          project: '${CIRCLE_PROJECT_REPONAME}/${CIRCLE_BRANCH}-container'
          severity-threshold: high
          target-file: ./submodules/goof/Dockerfile
          token-variable: SNYK_TOKEN
```
