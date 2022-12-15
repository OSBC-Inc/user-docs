# 애플리케이션 테스트

우리 프로젝트에는 다른 프로젝트의 샘플 애플리케이션이 포함되어 있습니다. 이를 위해 우리는 [`git submodule`](https://git-scm.com/book/en/v2/Git-Tools-Submodules)을 활용하여 Git 저장소를 다른 Git 저장소의 하위 디렉토리로 유지했습니다. 이 예에서 우리는 `./submodules` 디렉토리 아래의 리포지토리에서 찾을 수 있는 [Snyk의 취약한 데모 앱](https://github.com/snyk/goof)으로 작업하고 있습니다.

The next section of our `config.yml` defines a few `jobs` starting with `test_app` which will run some commands in our build environment. Here, we are importing the parameters defined earlier under `defaults` such as the Docker image for our build: `circleci/node:9.11.2`. We will also invoke `git submodule` and `npm install` the application. Lastly, because we will want this artifact downstream, we will call `persist_to_workspace` to reference it later on.

`config.yml`의 다음 섹션에서는 빌드 환경에서 일부 명령을 실행할 `test_app`으로 시작하는 몇 가지 `jobs`  를 정의합니다. 여기에서는 빌드용 Docker 이미지(`circleci/node:9.11.2`)와 같은 기본값으로 이전에 정의된 매개변수를 가져옵니다. 또한 `git submodule`을 호출하고 `npm`이 애플리케이션을 설치합니다. 마지막으로 이 아티팩트 다운스트림을 원하기 때문에 나중에 이를 참조하기 위해 `persist_to_workspace`를 호출합니다.

```yaml
jobs:
  test_app:
    <<: *defaults
    steps:
      - checkout
      - run:
          name: "pull submodules"
          command: |
            git submodule init
            git submodule update --recursive
      - run:
          name: "run test"
          command: |
            cd submodules/goof
            npm install
      - persist_to_workspace:
          root: .
          paths:
            - .
```

{% hint style="info" %}
You can read more about basic concepts to help you understand how CircleCI manages your CICD pipelines [here](https://circleci.com/docs/2.0/concepts/). Also checkout the blog post [Persisting Data in Workflows: When to Use Caching, Artifacts, and Workspaces](https://circleci.com/blog/persisting-data-in-workflows-when-to-use-caching-artifacts-and-workspaces/) to learn more about how to move data into and out of jobs.
{% endhint %}
