---
description: 도커 데스크탑을 사용하시나요? Docker CLI는 Snyk에서 제공하는 기본 취약성 감지 및 수정을 제공합니다.
---

# Docker CLI로 스캔

## Lab Meta

> 난이도: 초보자
>
> 소요시간 약 15분

[Snyk와 Docker의 파트너십](https://snyk.io/blog/snyk-docker-secure-containerized-applications/)의 일환으로 취약점에 대한 컨테이너 이미지 스캔은 Docker Desktop에 내장되어 있으며 docker 스캔만큼 간단합니다. 이 실습에서는 작동 방식을 보여줍니다.

다음 단계를 완료합니다:

* Step 1 - 샘플 애플리케이션의 GitHub 저장소 복제
* Step 2 - 일부 Docker 이미지 빌드
* Step 3 - 취약점에 대한 이미지 스캔
* Step 4 - 스캔 결과 검토
* Step 5 - 제공된 기본 이미지 권장 사항 자세히 알아보기
* Step 6 - 보다 안전한 기본 이미지 적용 및 이미지 재구축
* Step 7 - 취약점 재검색

## 전제 조건

* Docker Desktop을 다운로드하고 설치합니다.
  * [Mac용 다운로드](https://desktop.docker.com/mac/stable/Docker.dmg)
  * [Windows용 다운로드](https://desktop.docker.com/win/stable/Docker%20Desktop%20Installer.exe)
* **\[선택 사항]** [Docker Goof Repo](https://github.com/snyk/docker-goof)를 GitHub 계정으로 포크합니다.

{% hint style="info" %}
Snyk 계정은 필요하지 않지만 로그인하지 않고 10회만 스캔할 수 있습니다. [Docker ID를 사용하여 Snyk에 가입](https://snyk.co/SnykDockerAcademy)한 다음 `docker scan --login`을 실행하고 로그인하여 매월 200개의 무료 스캔을 잠금 해제하십시오.
{% endhint %}

`docker scan --version`을 실행하여 설치를 확인하십시오. docker scan의 현재 버전과 Snyk 엔진 버전이 인쇄되어야 합니다.

```bash
docker scan --version
```

## Step 1: Docker Goof 애플리케이션 또는 BYO 앱 복제

{% hint style="info" %}
이 실습에서는 Docker Goof 애플리케이션을 사용하지만 자체 애플리케이션을 가져와도 됩니다. 그렇게 하면 애플리케이션 빌드를 보장할 책임이 있습니다!
{% endhint %}

[Docker Goof 애플리케이션](https://github.com/snyk/docker-goof)을 워크스테이션에 복제한 다음 앱의 최상위 디렉터리로 변경합니다. Git이 없으신가요? [Docker-Goof 저장소를 Zip 파일로 다운로드할 수 있습니다](https://github.com/snyk/docker-goof/archive/master.zip).

```
git clone https://github.com/snyk/docker-goof && cd docker-goof
# If you forked the repo, clone your fork.
```

## Step 2: 하나(또는 여러 개)의 docker-goof 이미지 빌드

Docker Goof 저장소에는 많은 Dockerfile이 있습니다. 그들 중 일부 또는 전부를 만들 수 있습니다.

포함된 쉬운 버튼 `./build.sh`를 사용하여 한 번에 모두 빌드하십시오.

```bash
# Easy button? Yes please. Build all images at once with:
./build.sh
```

이미지를 하나씩 빌드하려면 Dockerfile을 가리키는 `-f`를 전달해야 합니다.

```bash
# Build your images with docker build.
docker build -t docker-goof-slim -f slim.Dockerfile .
docker build -t docker-goof -f Dockerfile .
```

이미지는 이제 로컬 Docker 캐시에 있습니다. `docker images`를 실행하여 나열합니다.

```bash
docker images
```

다음 단계에서 이러한 이미지를 사용합니다.

## Step 3: Snyk으로 이미지의 취약점 스캔

`docker scan`을 사용하여 취약점을 스캔합니다. `--file`을 사용하여 이미지를 빌드하는 데 사용되는 `Dockerfile`을 전달하여 Dockerfile 명령 및 기본 이미지 업그레이드 지침의 취약성을 포함하는 보다 강력한 결과를 얻는 것이 모범 사례입니다. 예를 들어,

docker-goof를 스캔하고 Dockerfile을 전달하려면:

```bash
# Scanning the docker-goof image and passing the Dockerfile 
docker scan docker-goof --file=Dockerfile
```

docker-goof-app을 스캔하고 Dockerfile을 전달하려면:

```bash
# Scanning the docker-goof-app image and passing the Dockerfile
docker scan docker-goof-app --file=app.Dockerfile
```

Dockerfile을 전달하지 않고 docker-goof-n6-slim을 스캔하려면:

```bash
# Scanning an image without passing the Dockerfile
docker scan docker-goof-n6-slim
```

{% hint style="info" %}
가능한 모든 CLI 옵션에 대해서는 [Docker 스캔 문서](https://docs.docker.com/engine/scan/)를 확인하십시오.
{% endhint %}

Snyk으로 이미지에서 오픈 소스 취약점을 스캔하는 것은 정말 쉽습니다! 완료되면 수정 조언과 함께 스캔 결과가 터미널에 표시됩니다.

## Step 4: 취약점 스캔 결과 검토

취약점은 도입 방법에 따라 여러 섹션으로 나뉩니다:

### 취약한 기본 이미지 패키지

컨테이너의 기본 이미지에 의해 도입된 취약성은 `Introduced by your base image` 행의 존재로 식별할 수 있습니다. (아래 9행)

```bash
✗ High severity vulnerability found in curl/libcurl3
  Description: Buffer Overflow
  Info: https://snyk.io/vuln/SNYK-DEBIAN8-CURL-466507
  Introduced through: curl@7.38.0-4+deb8u11, curl/libcurl4-openssl-dev@7.38.0-4+deb8u11, git@1:2.1.4-2.1+deb8u6
  From: curl@7.38.0-4+deb8u11 > curl/libcurl3@7.38.0-4+deb8u11
  From: curl/libcurl4-openssl-dev@7.38.0-4+deb8u11 > curl/libcurl3@7.38.0-4+deb8u11
  From: curl@7.38.0-4+deb8u11
  and 2 more...
  Introduced by your base image (node:10.4.0)
  Fixed in: 7.38.0-4+deb8u16
```

사용자 명령어 취약점

일부 취약점은 Dockerfile의 사용자 지침에 의해 도입되었습니다. Snyk는 `Introduced in your Dockerfile by` 줄과 함께 취약점을 도입한 명령을 강조 표시합니다. (9행)

```bash
✗ High severity vulnerability found in bzip2/bzip2
  Description: Out-of-bounds Write
  Info: https://snyk.io/vuln/SNYK-DEBIAN8-BZIP2-450781
  Introduced through: bzip2/bzip2@1.0.6-7+b3, dpkg/dpkg-dev@1.17.27, bzip2/libbz2-dev@1.0.6-7+b3, imagemagick/libmagickcore-dev@8:6.8.9.9-5+deb8u12, meta-common-packages@meta
  From: bzip2/bzip2@1.0.6-7+b3
  From: dpkg/dpkg-dev@1.17.27 > bzip2/bzip2@1.0.6-7+b3
  From: bzip2/libbz2-dev@1.0.6-7+b3
  and 2 more...
  Introduced in your Dockerfile by 'RUN apt-get install -y imagemagick'
  Fixed in: 1.0.6-7+deb8u1
```

### 취약한 앱 종속성

이미지에 포함될 수 있는 마지막 종류의 취약성은 애플리케이션 종속성에 의해 도입됩니다. Snyk는 이를 도입한 패키지 매니페스트 `Target File`을 강조 표시합니다. (14행)

```bash
Issues to fix by upgrading:

  Upgrade @tryghost/members-api@0.8.2 to @tryghost/members-api@0.24.1 to fix
  ✗ Remote Code Execution (RCE) [Medium Severity][https://snyk.io/vuln/SNYK-JS-BUNYAN-573166] in bunyan@1.8.12
    introduced by ghost-ignition@3.1.0 > bunyan@1.8.12 and 8 other path(s)

  Upgrade @tryghost/members-ssr@0.7.1 to @tryghost/members-ssr@0.8.3 to fix
  ✗ Remote Code Execution (RCE) [Medium Severity][https://snyk.io/vuln/SNYK-JS-BUNYAN-573166] in bunyan@1.8.12
    introduced by ghost-ignition@3.1.0 > bunyan@1.8.12 and 8 other path(s)


Organization:      demo-inc
Package manager:   yarn
Target file:       /var/lib/ghost/versions/2.37.2/package.json
Project name:      ghost
Docker image:      docker-goof-app
```

{% hint style="info" %}
[Container CLI 결과에 대한 정보는 Snyk 문서](https://support.snyk.io/hc/en-us/articles/360003946937-Understanding-container-CLI-scan-results)를 확인하십시오.
{% endhint %}

## Step 5: 기본 이미지 권장 사항 검토

Snyk의 수정 조언은 개발자가 수정에 소요되는 시간을 줄이고 개발에 더 많은 시간을 할애하도록 도와줍니다! 취약성을 해결하는 한 가지 방법은 보다 안전한 기본 이미지를 선택하는 것입니다. Dockerfile을 `docker scan`에 제공함으로써 Snyk는 Dockerfile의 `FROM` 문에서 사용할 수 있는 다른 기본 이미지를 제안하여 이러한 취약성 수를 줄일 수 있습니다.

애플리케이션과의 호환성 정도에 따라 다음과 같이 그룹화됩니다:

* `Minor` 업그레이드는 작은 작업과 호환될 가능성이 가장 높으며,
* `Major` 업그레이드는 이미지 사용에 따라 주요 변경 사항을 도입할 수 있습니다.
* 더 많은 기술 사용자가 조사할 수 있도록 `Alternative` 아키텍처 이미지가 표시됩니다.

{% hint style="info" %}
이러한 제안은 적절한 통합 테스트를 대신할 수 없습니다. 잠재적인 기본 이미지 선택 범위를 좁히는 데 도움이 됩니다.
{% endhint %}

```bash
Organization:      demo-inc
Package manager:   deb
Target file:       Dockerfile
Project name:      docker-image|docker-goof
Docker image:      docker-goof
Base image:        node:10.4.0
Licenses:          enabled

Tested 382 dependencies for known issues, found 459 issues.

Base Image   Vulnerabilities  Severity
node:10.4.0  951              451 high, 480 medium, 20 low

Recommendations for base image upgrade:

Minor upgrades
Base Image  Vulnerabilities  Severity
node:10.22  498              53 high, 48 medium, 397 low

Major upgrades
Base Image  Vulnerabilities  Severity
node:14.13  497              53 high, 47 medium, 397 low

Alternative image types
Base Image                 Vulnerabilities  Severity
node:14.13-buster-slim     51               9 high, 4 medium, 38 low
node:14.12.0-slim          70               17 high, 7 medium, 46 low
node:14.11.0-stretch-slim  70               17 high, 7 medium, 46 low
node:14.13.1-buster        254              31 high, 30 medium, 193 low
```

## Step 6: 보다 안전한 기본 이미지 적용

docker-goof에 대해 더 안전한 기본 이미지를 선택해 보겠습니다. Snyk에서 권장하는 마이너 업그레이드를 적용하여 이를 수행합니다. Dockerfile에서 FROM 문을 변경합니다.

```bash
# Comment out the old FROM Statement
# FROM node:10.4.0

# Write in the new one
FROM node:10.22

RUN apt-get install -y imagemagick
```

이제 새 이미지를 빌드합니다. 결과를 이전 스캔과 나란히 비교하기 위해 이미지를 빌드할 때 다른 태그를 지정합니다.

```bash
docker build -t docker-goof:v2 -f Dockerfile .
```

## Step 7: Snyk으로 이미지의 취약점 스캔

이제 `docker scan`을 사용하여 취약점을 스캔해 보겠습니다. 다시 한 번 더 강력한 결과를 얻으려면 `--file`을 사용하여 이미지를 빌드하는 데 사용된 `Dockerfile`을 전달합니다.

```bash
# Scanning the docker-goof image and passing the Dockerfile 
docker scan docker-goof:v2 --file=Dockerfile
```

{% hint style="info" %}
가능한 모든 CLI 옵션에 대해서는 [Docker 스캔 문서](https://docs.docker.com/engine/scan/)를 확인하십시오.
{% endhint %}

가장 안전한 기본 이미지를 실행할 때까지 이 빌드-스캔-푸시 주기를 계속합니다.

## 요약: 추가 리소스 및 Docker 허브 프로모션!

이 실습을 즐기셨기를 바랍니다. 이 패턴에서는 Docker CLI를 사용하여 이미지의 취약성을 확인하고 기본 이미지, Dockerfile 명령 및 애플리케이션 종속성에 의해 도입된 취약성을 확인했습니다.

더 안전한 기본 이미지를 적용하는 것은 이미지를 더 안전하게 만들기 위한 훌륭한 첫 번째 단계입니다. 위에서 언급한 것처럼 취약점은 애플리케이션 종속성 및 Dockerfile 사용자 지침에서도 발생할 수 있습니다. Snyk Academy의 다른 과정을 확인하여 Snyk가 이미지의 다른 취약성을 수정하고 줄이는 데 어떻게 도움이 되는지 알아보세요.

Docker와의 파트너십을 계속 발전시키면서 개발자가 컨테이너 이미지를 안전하게 빌드하고 확신을 가지고 배포하는 데 도움이 되는 새로운 기능을 계속 추가할 것입니다. 자신의 애플리케이션에서 이 워크플로우를 시도하고 의견을 알려주세요!

{% hint style="success" %}
Snyk Academy의 다른 과정에는 Snyk 계정이 필요할 수 있습니다. 잊지 마세요. [Docker Hub로 로그인](https://snyk.co/SnykDockerAcademy)하는 새 계정은 월 200회 스캔이라는 프로모션 무료 계층 제한을 해제합니다!
{% endhint %}
