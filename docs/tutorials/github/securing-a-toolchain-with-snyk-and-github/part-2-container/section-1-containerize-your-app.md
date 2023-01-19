# Section 1: 앱 컨테이너화

## Step 1: 컨테이너 파일에 대한 새 Branch 만들기

`develop`을 위해 Merge하기 전에 이 Section에 대한 파일을 생성할 `develop` Branch에서 새 Branch를 생성하는 것으로 시작하겠습니다. 그것을 `add-container-files` 라고 부릅니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-container-newbranch.png)

## Step 2: Container workflow용 파일 만들기

{% hint style="info" %}
이 단계에서는 Dockerfile을 만들고 GitHub Actions CI Workflow를 수정합니다. 거기에서 복사-붙여넣기를 원하는 경우 파일은 `container-actions` Branch에서 사용할 수 있습니다. 이것들은 참조용입니다. 해당 Branch를 Merge하여 `develop`하려고 하면 Merge 충돌이 발생합니다.
{% endhint %}

### Dockerfile 만들기

우리가 만들 첫 번째 파일은 애플리케이션을 컨테이너로 패키징하는 지침인 `Dockerfile` 입니다. 새 분기에 있는지 확인하고 "Add File"를 클릭한 다음 "Create new file"를 클릭합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-container-createnewfile.png)

아래와 같이 새 파일 `Dockerfile`을 호출합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-container-createdockerfile.png)

이것을 `Dockerfile`의 내용으로 붙여넣으십시오.

```
FROM node:6-stretch

RUN mkdir /usr/src/goof
RUN mkdir /tmp/extracted_files
COPY . /usr/src/goof
WORKDIR /usr/src/goof

RUN npm update
RUN npm install
EXPOSE 3001
EXPOSE 9229
ENTRYPOINT ["npm", "start"]
```

준비가 되면 변경 사항을 `add-container-files` Branch에 직접 Commit합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-container-createdockerfile2.png)

### CI Workflow로 수정

이제 GitHub Actions에 컨테이너 빌드 방법을 알려야 합니다. `.github/workflows` 폴더에는 Branch에 대한 Pull Request이 열릴 때 애플리케이션을 다시 빌드하는 CI Workflow가 포함되어 있습니다. GitHub Editor를 사용하여 두 CI Workflow에 컨테이너 빌드 단계를 추가해 보겠습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-container-editdevelopci.png)

`.github/workflows/goof-ci-develop`의 내용을 다음으로 바꿉니다.

```
# This workflow will do a clean install of node dependencies, build the source code and run tests across different versions of node
# For more information see: https://help.github.com/actions/language-and-framework-guides/using-nodejs-with-github-actions

name: Node.js CI task for develop branch

on:
  push:
    branches: [ develop ]
  pull_request:
    branches: [ develop ]

jobs:
  build_app:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    - name: Use Node.js 12.x
      uses: actions/setup-node@v1
      with:
        node-version: 12.x
    - run: npm ci
    - run: npm run build --if-present
  build_container:
    needs: [build_app]
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Setup up Docker Buildx
        uses: docker/setup-buildx-action@v1
      - name: Build Docker Image
        id: docker_build
        uses: docker/build-push-action@v2
        with:
          push: false
          load: true
          tags: goof:develop         
      - name: Snyk Container Test
        continue-on-error: true
        uses: snyk/actions/docker@master
        env:
          SNYK_TOKEN: ${{ Secrets.SNYK_TOKEN }}
        with:
          image: goof:develop
          args: --file=Dockerfile
      - name: Upload Container Scan results to GitHub Code Scanning
        uses: github/codeql-action/upload-sarif@v1
        with:
          sarif_file: snyk.sarif
```

CI Workflow는 이제 다음 작업을 수행합니다:

1. 먼저 앱을 빌드합니다. 이것은 `build-app` 작업입니다.
2. 앱 빌드가 성공하면 컨테이너를 빌드합니다.
3. 컨테이너가 성공적으로 빌드되면 Snyk Container로 스캔합니다.
4. 스캔이 완료되면 결과가 GitHub Security Code Scanning으로 푸시됩니다.

Now commit the changes directly to our new `add-container-files` branch.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-container-commitcontainerci.png)

이제 PROD Workflow에 대해 동일한 프로세스를 반복하여 36행과 43행에 지정된 이미지 태그를 `goof:develop`에서 `goof:PROD`로 바꿉니다. 이렇게 하면 PROD 및 `develop` 컨테이너가 컨테이너 레지스트리에 업로드된 후 별도의 엔터티로 유지됩니다.

## Step 3: Pull Request를 작성하여 개발

Dockerfile이 생성되고 Workflow가 수정되면 `add-container-files` Branch를 `develop` Branch에 Merge하여 공식화합니다. GitHub에서 Pull Request를 시작합니다. 이전 Section에서와 마찬가지로 Fork를 기본 저장소로 선택해야 합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-container-addfilespr.png)

PR이 생성되면 컨테이너 이미지를 빌드하기 위해 추가한 새 항목을 포함하여 검사가 실행됩니다. 모든 확인이 완료되면 Pull Request를 Merge하고 Branch를 삭제합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-container-addfileprchecks.png)

이제 애플리케이션을 컨테이너에 패키징했습니다! 애플리케이션의 오픈 소스 구성 요소와 관련된 공개적이고 수정 가능한 모든 문제를 수정했음에도 불구하고 이를 컨테이너에 패키징하기로 결정함에 따라 해결해야 할 추가 위험이 발생했습니다. Snyk Container가 이러한 문제를 찾고 해결하는 데 어떻게 도움이 되는지 알아보려면 Section 2로 이동하십시오.
