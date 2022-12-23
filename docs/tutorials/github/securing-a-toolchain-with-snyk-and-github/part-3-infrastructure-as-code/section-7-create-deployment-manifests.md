# Section 1: 배포 매니페스트 생성

## Step 1: 컨테이너 파일에 대한 새 Branch 만들기

개발을 위해 Merge하기 전에 응용 프로그램에 대한 배포 매니페스트를 만드는 `develop` Branch에서 새 Branch를 생성하여 시작하겠습니다. 그것을 `add-iac-files` 라고 부르십시오.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-iac-createbranch.png)

## Step 2: 애플리케이션 매니페스트 만들기

{% hint style="warning" %}
이 단계에서는 애플리케이션의 배포 구성으로 YAML 파일을 생성합니다. 거기에서 복사-붙여넣기를 원하는 경우 `iac-actions` Branch의 파일. 참고용입니다. 해당 Branch를 Merge하여 개발하려고 하면 Merge 충돌이 발생합니다.
{% endhint %}

### 배포 정의 만들기

먼저 오케스트레이션 환경에 Goof 컨테이너를 가동하는 방법을 알려주는 구성 파일인 배포를 만듭니다. 새 분기로 전환하고 "Add File"를 클릭한 다음 "Create new file"를 클릭합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-iac-createfile.png)

새 파일 `goof-deployment.yaml`을 호출하고 이를 파일의 내용으로 붙여넣습니다.

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: goof
spec:
  replicas: 1
  selector:
    matchLabels:
      app: goof
      tier: frontend
  template:
    metadata:
      labels:
        app: goof
        tier: frontend
    spec:
      containers:
        - name: goof-app
          image: goof:PROD
          ports:
            - containerPort: 3001
            - containerPort: 9229
          env:
            - name: DOCKER
              value: "1"
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: goof-mongo
spec:
  replicas: 1
  selector:
    matchLabels:
      app: goof
      tier: backend
  template:
    metadata:
      labels:
        app: goof
        tier: backend
    spec:
      containers:
        - name: goof-mongo
          image: mongo
          ports:
            - containerPort: 27017
```

준비가 되면 변경 사항을 `add-iac-files` Branch에 직접 Commit합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-iac-commitdeployment.png)

### 서비스 정의 만들기

다음으로 애플리케이션이 노출되는 방식을 정의하는 `Service`를 만듭니다. 새 Branch에서 파일을 추가하고 이름을 `goof-service.yaml` 로 지정하고 내용으로 붙여넣습니다.

```
apiVersion: v1
kind: Service
metadata:
  name: goof
spec:
  type: LoadBalancer
  ports:
    - protocol: TCP
      port: 80
      targetPort: 3001
      name: "http"
    - protocol: TCP
      port: 9229
      targetPort: 9229
      name: "debug"
  selector:
    app: goof
    tier: frontend
---
apiVersion: v1
kind: Service
metadata:
  name: goof-mongo
spec:
  ports:
    - protocol: TCP
      port: 27017
      targetPort: 27017
      name: "mongo"
  selector:
    app: goof
    tier: backend
```

파일을 `add-iac-files` Branch에 직접 Commit합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-iac-commitservice.png)

## Step 3: Snyk IaC Test Workflow 만들기

구성 문제에 대해 매니페스트 파일을 확인하기 위해 Snyk IaC로 확인하는 Workflow를 만듭니다. `.github/workflows` 폴더에 `snyk-iac-check.yaml`이라는 파일을 만들고 다음 내용을 내용으로 붙여넣습니다:

```
name: Test Infrastructure as Code with Snyk
on:
  push:
    paths: 
      - '**.yaml'
jobs:
  snyk:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Check configuration files for security issues with Snyk
        continue-on-error: true
        uses: snyk/actions/iac@master
        env:
          SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}
        with:
          file: goof-deployment.yaml goof-service.yaml
      - name: Upload result to GitHub Code Scanning
        uses: github/codeql-action/upload-sarif@v1
        with:
          sarif_file: snyk.sarif
```

{% hint style="info" %}
`files` Section은 우리가 생성한 YAML 파일이 변경될 때 GitHub Actions가 Workflow를 실행하도록 지시합니다. 실행 후 결과는 GitHub Security Code Scanning으로 Push됩니다. 이러한 파일과 관련되지 않은 GitHub 활동의 경우 아무 일도 일어나지 않습니다.
{% endhint %}

이 파일을 `add-iac-files` Branch에 직접 Commit합니다.

## Step 4: Snyk Gate에 IaC 검사 추가

Part 1에서는 PROD Branch에 코드의 배포 준비 상태가 포함되어 있음을 설정했습니다. GitHub Actions를 사용하면 애플리케이션을 오케스트레이션 환경에 지속적으로 배포하는 Workflow를 생성할 수 있습니다. 예를 들어 다음과 같은 작업이 있습니다.

* [Azure Kubernetes에 배포](https://github.com/marketplace/actions/deploy-to-kubernetes-cluster)
* [DigitalOcean Kubernetes에 배포](https://github.com/do-community/example-doctl-action)
* [OpenShift에 배포할 `oc` 도구 설정](https://github.com/marketplace/actions/openshift-client-installer)

이러한 작업은 생성한 매니페스트 파일을 입력으로 사용하며 코드가 `PROD` Branch로 Push될 때 애플리케이션을 재배포할 수 있습니다. Pull Request 프로세스 중에 실행되도록 Snyk 게이트를 구성하여 구성 문제에 대한 배포 매니페스트를 확인하고 해당 연속 배포 시나리오에서 프로덕션 환경에 문제가 도입되기 전에 문제를 포착합니다.

### Snyk Gate 편집

Snyk Gate는 `.github/workflows/snyk-gate.yml`에 있습니다. `add-iac-files` Branch에 있는 동안 GitHub web 편집기로 엽니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-iac-editgate.png)

파일의 내용을 다음으로 바꿉니다. 새로운 `iac-security` 작업에 주목하십시오. 작업 정의에서 중간 심각도 이상의 문제가 있는 경우 확인에 실패하기로 결정했습니다.

```
name: Snyk Security Gate
on: 
  pull_request:
    branches:
      PROD
jobs:
  oss-security:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@master
    - name: Check for High Severity OSS Vulnerabilities
      uses: snyk/actions/node@master
      env:
        SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}
      with:
        args: --severity-threshold=high --fail-on=upgradable
  iac-security:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Snyk IaC Test
        uses: snyk/actions/iac@master
        env:
          SNYK_TOKEN: ${{ Secrets.SNYK_TOKEN }}
        with:
          file: goof-deployment.yaml goof-service.yaml
          args: --severity-threshold=medium
```

준비가 되면 변경된 파일을 `add-iac-files` Branch에 직접 Commit합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-iac-commitgatechanges.png)

### 새로운 Snyk Gate Workflow 이해

이제 Snyk Gate는 PROD branch에 대해 Pull Request가 열릴 때 두 가지를 확인합니다.

* 수정 가능한 심각도 높음 Issue가 있는 애플리케이션 종속성이 있습니까?
* 배포 매니페스트에 중간 심각도 구성 문제가 있습니까?

이것은 우리 팀이 프로덕션 환경에 대해 결정한 허용 오차입니다. PR 프로세스의 일부로 이 검사를 자동화하면 PROD에 병합하는 것이 이러한 규칙을 준수한다는 확신을 갖게 됩니다.

## Step 5: Pull Request를 작성하여 개발

`add-iac-files` Branch를 `develop` Branch로 Merge할 준비가 되었습니다. GitHub에서 `develop`에서 PROD로 Pull Request를 시작합니다. Fork를 기본 저장소로 선택해야 합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-iac-developpr.png)

PR이 생성되면 결과를 GitHub Security Code Scanning에 업로드하는 Pull Request의 일부로 실행되는 새로운 Snyk IaC 검사 Workflow를 볼 수 있습니다. 완료되면 변경 사항을 Merge합니다.

## Step 6: PROD에 Pull Request 생성

`develop` branch에는 이제 애플리케이션을 Kubernetes에 배포하는 데 필요한 것이 있습니다! Pull Request를 열어 변경 사항과 배포 매니페스트를 PROD에 Merge해 보겠습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-iac-prodpr.png)

PR Check에서 IaC 게이트가 실패한 것을 볼 수 있습니다!

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-iac-iacgatefail.png)

지금은 Pull Request를 열어두세요. 다음 Section에서는 Snyk이 식별하고 생산 지점에 도입하지 못하도록 방지한 위험에 대해 자세히 설명합니다.
