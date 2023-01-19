# 샘플 애플리케이션 복제 및 실행

## Step 1: 샘플 앱 가져오기 및 저장소 복제

템플릿 GitHub Repo는 [Snyk의 Goof 애플리케이션](https://github.com/snyk/goof#goof---snyks-vulnerable-demo-app)을 사용하여 이 워크샵을 위해 제공됩니다.

{% embed url="https://github.com/snyk-partners/docker-academy" %}

"Use this Template"을 클릭하여 저장소를 GitHub 계정에 복사합니다.

{% hint style="danger" %}
이 지침의 명령을 올바르게 복사하여 붙여넣으려면 저장소 이름을 `docker-academy`로 지정하십시오. 그렇지 않으면 명령이 올바른 저장소 이름을 사용하는지 확인하십시오.
{% endhint %}

명령을 복사하여 붙여넣으려면 GitHub ID에 대한 환경 변수를 설정하십시오.

```bash
# Set an environment variable for your GitHub ID
GithubId=<<your_github_id>>
```

이제 저장소를 로컬 환경에 복제한 다음 `cd`합니다.

```bash
# Clone the Repo and cd 
git clone https://www.github.com/$GithubId/docker-academy && cd docker-academy
```

## Step 2: 애플리케이션을 로컬에서 테스트

### 종속성 설치

애플리케이션을 로컬에서 실행하려면 먼저 종속성을 설치해야 합니다.

```bash
# Install npm dependencies and generate lockfile
npm install --package-lock
```

### Mongo database 시작

앱이 작동하려면 MongoDB가 필요합니다. Mongo를 설치하는 대신 Docker 컨테이너에서 실행할 것입니다.

```bash
# Start detached mongo with container port 27017 mapped to host port 27017
docker run -d -p 27017:27017 mongo
```

`docker ps`를 실행하여 mongo가 실행 중인지 확인할 수 있습니다.

### 애플리케이션 시작

이제 응용 프로그램을 실행할 수 있습니다.

```bash
node app.js
```

시작되면 [http://localhost:3001](http://localhost:3001/)에서 사용할 수 있습니다. 할 일 목록에 몇 가지 항목을 추가하여 작동하는지 확인합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/todo.png)

성공! 이제 작동하는 것을 확인했으므로 배포용 컨테이너에 패키징해 보겠습니다.

## 도커 이미지 빌드

명령을 복사하여 붙여넣으려면 Docker ID에 대한 환경 변수를 설정하십시오.

```bash
# Set an environment variable for your GitHub ID
DockerId=<<your_docker_id>>
```

리포지토리의 `Dockerfile`은 `docker build`에 컨테이너 빌드 방법을 알려줍니다. Dockerfile 명령에 대한 자세한 내용은 [Docker 설명서](https://docs.docker.com/engine/reference/builder/)를 참조하십시오. 요약은 다음과 같습니다.

{% code title="Dockerfile" %}
```bash
FROM node:10.4 ## Use Node 10.4 as our base image

RUN mkdir /usr/src/goof ## Create the directory for our application
RUN mkdir /tmp/extracted_files
COPY . /usr/src/goof ## Copy the current directory files into the image
WORKDIR /usr/src/goof ## Set the working directory

RUN npm update ## Ensure npm is up to date
RUN npm install ## Install dependencies
EXPOSE 3001 ## Expose the port
EXPOSE 9229
ENTRYPOINT ["npm", "start"] ## The command
```
{% endcode %}

준비가 되면 컨테이너 이미지를 빌드하고 태그를 지정하여 Docker Hub에 푸시할 준비를 합니다.

```bash
# Build the container and tag it dev
docker build -t $DockerId/goof:dev .
```

빌드가 완료되면 컨테이너를 Docker Hub로 푸시합니다.

```bash
# Push to Docker Hub
docker push $DockerId/goof:dev
```

## Kubernetes에 애플리케이션 배포

클라우드 비용을 발생시키지 않고 컨테이너가 Kubernetes에 올바르게 배포되도록 하기 위해 Docker Desktop과 함께 제공되는 Kubernetes 클러스터를 사용합니다. 앱을 배포하기 전에 앱의 배포 매니페스트를 변경해야 합니다. 텍스트 편집기에서 `goof-deployment.yaml` 파일을 엽니다.

이 행을 찾아 표시된 곳에 Docker ID를 삽입하십시오.

```yaml
spec:
  containers:
  - image: <<DOCKERID>>/goof:dev #Edit with your Docker Hub ID
    name: goof
    imagePullPolicy: Always
```

변경 사항을 저장합니다. 이제 애플리케이션을 배포할 준비가 되었습니다. 다음 명령을 실행합니다:

```bash
# Create a namespace
kubectl create ns snyk-docker

# Set the current context to use the new namespace
kubectl config set-context --current --namespace snyk-docker

# Spin up the goof deployment and service
kubectl create -f goof-deployment.yaml,goof-mongo-deployment.yaml
```

애플리케이션이 시작될 때 포드의 상태를 확인하려면 다음 명령을 사용하십시오:

```bash
kubectl get pods
```

둘 다 실행되면 응용 프로그램은 이제 [http://localhost:3001](http://localhost:3001/)에서 액세스할 수 있습니다. 성공!

이제 애플리케이션이 Kubernetes에 배포될 때 작동한다는 것을 알았으므로 코드가 변경될 때 컨테이너를 다시 빌드하기 위해 지속적 통합 및 지속적 전달 파이프라인을 설정할 것입니다.
