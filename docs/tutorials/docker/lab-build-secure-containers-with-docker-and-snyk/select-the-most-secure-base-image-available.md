---
description: 컨테이너를 보호할 수 있는 가장 쉬운 방법 중 하나는 안전한 기본 이미지를 사용하고 있는지 확인하는 것입니다.
---

# 사용 가능한 가장 안전한 기본 이미지 선택

Snyk을 사용하면 컨테이너의 보안 기본 이미지를 쉽게 선택할 수 있습니다. Snyk UI와 Docker Desktop 사용 모두에서 기본 이미지 제안을 얻는 방법을 보여드리겠습니다.

## Docker Desktop의 기본 이미지 제안

개발자는 컨테이너를 `docker scan`하여 취약성 정보 및 기본 이미지 업그레이드 지침을 얻을 수 있습니다. 다음 명령을 실행하여 이미지를 스캔합니다. 기본 이미지 제안을 받으려면 `--file`을 사용하여 이미지를 빌드하는 데 사용되는 `Dockerfile`을 전달해야 합니다.

```
docker scan $DockerId/goof:dev --file=Dockerfile
```

{% hint style="info" %}
[간편한 치트 시트를 사용](https://snyk.io/blog/docker-security-scanning-cheatsheet-2021/)하여 Docker Scan으로 가능한 다른 작업에 대해 알아보십시오.
{% endhint %}

Snyk은 덜 취약한 기본 이미지를 호환 가능성에 따라 그룹화할 것을 권장합니다:

* `Minor` 업그레이드는 작은 작업과 호환될 가능성이 가장 높으며,
* `Major` 업그레이드는 이미지 사용에 따라 주요 변경 사항을 도입할 수 있습니다.
* 더 많은 기술 사용자가 조사할 수 있도록 `Alternative` 아키텍처 이미지가 표시됩니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/docker-scanvulns.png)

Next we'll show you how you can get these same base image suggestions inside the Snyk UI.

## Base image suggestions in Snyk

### Step 1: Snyk의 GitHub 통합 구성

{% hint style="info" %}
Snyk GitHub 통합을 이미 구성한 경우 2단계로 계속 진행합니다.
{% endhint %}

먼저 리포지토리를 가져올 수 있도록 Snyk을 GitHub에 연결해야 합니다. 다음과 같이 하십시오.

1. Snyk.io에 로그인합니다. 아직 [가입](https://snyk.co/SnykGH)하지 않았다면 가입하세요.
2. Integrations -> Integrations -> GitHub로 이동
3. 계정 자격 증명을 입력하여 GitHub 계정을 연결하세요.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-gh.png)

### Step 2: 포크된 저장소를 Snyk으로 가져오기

이제 Snyk이 GitHub 계정에 연결되었으므로 저장소를 Snyk 프로젝트로 가져옵니다.

1. Projects로 이동
2. "Add Project"를 클릭한 다음 "GitHub"를 선택합니다.
3. 생성한 저장소를 클릭합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-ghimport.png)

### Step 3: 앱에 대한 기본 이미지 제안 살펴보기

저장소를 가져올 때 Snyk은 컨테이너의 Dockerfile을 포함하여 저장소에서 지원되는 매니페스트 파일을 표시합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-proj-dockerfile.png)

Dockerfile을 클릭하면 기본 이미지 제안을 볼 수 있는 프로젝트 보기로 이동합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-baseimagerecs.png)

다음으로 Kubernetes 클러스터에서 실행 중인 컨테이너에서 취약성 및 기본 이미지 업그레이드 지침을 스캔합니다. 이 사용 사례는 사내에서 개발되지 않은 이미지를 실행할 때 유용합니다.

## 선택 사항: 실행 중인 워크로드의 취약점 찾기

Snyk의 Kubernetes Monitor를 사용하면 클러스터에서 실행 중인 워크로드의 취약성을 찾을 수 있습니다. 이 섹션에서는 Snyk Kubernetes Monitor를 배포하여 goof 애플리케이션을 스캔합니다.

{% hint style="info" %}
[Kubernetes Monitor 배포에 대한 전체 지침](https://support.snyk.io/hc/en-us/articles/360003916158#UUID-753328ea-3d73-0eeb-4301-c22522273797)은 문서에서 찾을 수 있습니다.
{% endhint %}

시작하려면 먼저 Snyk 모니터에 대한 네임스페이스를 만듭니다:

```
kubectl create ns snyk-monitor
```

다음으로 Snyk의 통합 메뉴에서 Kubernetes 통합 ID를 검색합니다.

![](https://support.snyk.io/hc/article\_attachments/360007147458/uuid-26f9c2cd-2755-07d5-61a0-bdb0261d87ab-en.gif)

통합 ID를 환경 변수로 저장하여 다음 명령을 복사하여 붙여넣습니다.

```
IntegrationId=<<your_integration_id>>
```

Create a secret in the cluster containing the Integration ID.

```
kubectl create secret generic snyk-monitor -n snyk-monitor \
        --from-literal=dockercfg.json={} \
        --from-literal=integrationId=$IntegrationId
```

Now deploy the Kubernetes monitor using Helm:

```
helm upgrade --install snyk-monitor snyk-charts/snyk-monitor \
             --namespace snyk-monitor \
             --set clusterName="Docker Desktop"
```

When it finishes deploying, you'll be able to import the cluster workloads into Snyk.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/k8s-import.png)

Select to import both the `goof` and `mongo` deployments.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/k8simport2.png)

When the import completes, they will show up next to the other projects in the Snyk dashboard.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/k8sworkloads.png)

Since it's the same container, clicking the `snyk-docker/deployment.apps/goof` project will show the same vulnerabilities as the `Dockerfile` project from the previous section.

You can point the Kubernetes project at the `Dockerfile` to see base image suggestions.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/k8ssettings.png)

This will provide the same base image suggestions for running workloads. We can see that using a different base image can address hundreds of vulnerabilities. This is a relatively low effort fix with huge payoff. Let's apply a more secure base for our application.

## Choose a more secure base image

Open the `Dockerfile` with a text editor, and replace, or comment out, the old base image with a new one. In this example, we'll use `node:10.23.1`.

{% code title="Dockerfile" %}
```bash
FROM node:10.23.1

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
{% endcode %}

Save the changes. Now build and push the container to Docker Hub.

```bash
docker build -t $DockerId/goof:dev .
docker push $DockerId/goof:dev
```

Once it's done, test it in Kubernetes by scaling the `goof` deployment with `kubectl`. The deployment's `ImagePullPolicy` forces Kubernetes to pull the latest image from Docker Hub.

```bash
kubectl scale deployment goof --replicas=0
kubectl scale deployment goof --replicas=1
```

Navigate to [http://localhost:3001](http://localhost:3001) to test the app. Success! It likes the new base image. In Docker Hub, we can appreciate the `dev` tag has less vulnerabilities than `PROD`.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/dockerhub-tagvulns%20\(1\).png)

If you imported the project using the Kubernetes Monitor, you'll see the new results once the Snyk Monitor re-tests the project.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/k8sproject.png)

Let's get these changes into our GitHub Repo's PROD branch!

## Commit the changes to GitHub, then into PROD

### Commit the changes to the develop branch

First we need to commit the changes to our Repo's `develop` branch. Use Git to do so.

```bash
git add Dockerfile
git commit -m "new base image"
git push
```

### Open a Pull Request from develop to PROD

In GitHub, create a Pull Request from the `develop` branch to the `PROD` branch.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-newpr.png)

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-pr-newbase.png)

### See the PR checks we configured in action

The workflows we configured earlier will run as part of this PR. You can see the results of the workflow runs in the PR view before choosing to Merge the PR. To recap what each one does:

* **license/snyk** checks the incoming changes against the snapshot in Snyk for new license issues
* **security/snyk** checks the incoming changes against the snapshot in Snyk for new vulnerabilities
* **Check for Open Source Vulnerabilities with Snyk** checks if there are **any** vulnerable open source components in the application with fixes available
* **CI Task for PROD Branch** rebuilds and app and container to make sure it correctly builds.
* **Code scanning results** pushes the container scan results to GitHub Security for consumption.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-prchecks%20\(1\).png)

Even though we have open source vulnerabilities, merge the PR. This triggers AutoBuild to build and re-scan the PROD container. When it completes, we see a reduction in the number of vulnerabilities.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/dockerhub-tags.png)

Choosing a more secure base image was just the start! In the next section, we'll address the application's vulnerable application dependencies.
