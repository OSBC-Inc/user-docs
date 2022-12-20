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

통합 ID를 환경 변수로 저장하여 다음 명령을 복사하여 붙여넣습니다:

```
IntegrationId=<<your_integration_id>>
```

통합 ID가 포함된 클러스터에 시크릿을 생성합니다:

```
kubectl create secret generic snyk-monitor -n snyk-monitor \
        --from-literal=dockercfg.json={} \
        --from-literal=integrationId=$IntegrationId
```

이제 Helm을 사용하여 Kubernetes 모니터를 배포합니다:

```
helm upgrade --install snyk-monitor snyk-charts/snyk-monitor \
             --namespace snyk-monitor \
             --set clusterName="Docker Desktop"
```

배포가 완료되면 클러스터 워크로드를 Snyk로 가져올 수 있습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/k8s-import.png)

`goof` 및 `mongo` 배포를 모두 가져오려면 선택합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/k8simport2.png)

가져오기가 완료되면 Snyk 대시보드의 다른 프로젝트 옆에 표시됩니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/k8sworkloads.png)

동일한 컨테이너이므로 `snyk-docker/deployment.apps/goof` 프로젝트를 클릭하면 이전 섹션의 `Dockerfile` 프로젝트와 동일한 취약점이 표시됩니다.

`Dockerfile`에서 Kubernetes 프로젝트를 가리켜 기본 이미지 제안을 볼 수 있습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/k8ssettings.png)

이렇게 하면 실행 중인 워크로드에 대해 동일한 기본 이미지 제안이 제공됩니다. 다른 기본 이미지를 사용하면 수백 가지의 취약점을 해결할 수 있음을 알 수 있습니다. 이것은 막대한 보상을 제공하는 상대적으로 적은 노력의 수정입니다. 애플리케이션에 보다 안전한 기반을 적용해 보겠습니다.

## 더 안전한 기본 이미지 선택

텍스트 편집기로 `Dockerfile`을 열고 이전 기본 이미지를 새 이미지로 바꾸거나 주석 처리합니다. 이 예에서는 `node:10.23.1`을 사용합니다.

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

변경 사항을 저장합니다. 이제 컨테이너를 빌드하고 Docker Hub에 푸시합니다.

```bash
docker build -t $DockerId/goof:dev .
docker push $DockerId/goof:dev
```

완료되면 `kubectl`로 `goof` 배포를 확장하여 Kubernetes에서 테스트합니다. 배포의 `ImagePullPolicy`는 Kubernetes가 Docker Hub에서 최신 이미지를 가져오도록 합니다.

```bash
kubectl scale deployment goof --replicas=0
kubectl scale deployment goof --replicas=1
```

[http://localhost:3001](http://localhost:3001/)로 이동하여 앱을 테스트합니다. 성공! 새로운 기본 이미지를 좋아합니다. Docker Hub에서는 `dev` 태그가 `PROD`보다 취약성이 낮다는 것을 알 수 있습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/dockerhub-tagvulns%20\(1\).png)

Kubernetes Monitor를 사용하여 프로젝트를 가져온 경우 Snyk Monitor가 프로젝트를 다시 테스트하면 새 결과가 표시됩니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/k8sproject.png)

이러한 변경 사항을 GitHub 저장소의 PROD branch에 적용해 봅시다!

## 변경 사항을 GitHub에 Commit한 다음 PROD에 Commit합니다.

### 개발 branch에 대한 변경 사항 Commit

먼저 저장소의 `develop` branch에 대한 변경 사항을 Commit해야 합니다. Git을 사용하십시오.

```bash
git add Dockerfile
git commit -m "new base image"
git push
```

### 개발에서 PROD로 Pull Request 열기

GitHub에서 `develop` branch에서 PROD branch로 Pull Request를 생성합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-newpr.png)

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-pr-newbase.png)

### 실제로 구성한 PR 확인 보기

이전에 구성한 워크플로우는 이 PR의 일부로 실행됩니다. PR Merge를 선택하기 전에 PR 보기에서 워크플로우 실행 결과를 볼 수 있습니다. 각각의 기능을 요약하면 다음과 같습니다:

* **license/snyk**는 새 라이선스 문제에 대해 Snyk의 스냅샷에 대해 들어오는 변경 사항을 확인합니다.
* **security/snyk**는 새로운 취약성에 대해 Snyk의 스냅샷에 대해 들어오는 변경 사항을 확인합니다.
* **Snyk으로 오픈 소스 취약점 확인**은 수정 사항이 있는 애플리케이션에 취약한 오픈 소스 구성 요소가 **있는지** 확인합니다.
* **PROD Branch에 대한 CI 작업**이 다시 빌드되고 앱과 컨테이너가 올바르게 빌드되는지 확인합니다.
* **코드 스캔 결과**는 컨테이너 스캔 결과를 사용을 위해 GitHub 보안으로 푸시합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-prchecks%20\(1\).png)

오픈 소스 취약점이 있어도 PR을 Merge하십시오. 이렇게 하면 AutoBuild가 트리거되어 PROD 컨테이너를 빌드하고 다시 스캔합니다. 완료되면 취약점 수가 감소합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/dockerhub-tags.png)

보다 안전한 기본 이미지를 선택하는 것은 시작에 불과했습니다! 다음 섹션에서는 애플리케이션의 취약한 애플리케이션 종속성을 다룰 것입니다.
