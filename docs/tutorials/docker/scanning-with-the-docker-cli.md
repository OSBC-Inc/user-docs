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

## Step 3: Scan your Image for vulnerabilities with Snyk

Use `docker scan` to scan for vulnerabilities. It's a best practice to pass the `Dockerfile` used to build the image with `--file` to get more robust results that include vulnerabilities from Dockerfile instruction and base image upgrade guidance. For example,

To scan docker-goof, and pass the Dockerfile:

```bash
# Scanning the docker-goof image and passing the Dockerfile 
docker scan docker-goof --file=Dockerfile
```

To scan docker-goof-app, and pass the Dockerfile:

```bash
# Scanning the docker-goof-app image and passing the Dockerfile
docker scan docker-goof-app --file=app.Dockerfile
```

To scan docker-goof-n6-slim, without passing the Dockerfile:

```bash
# Scanning an image without passing the Dockerfile
docker scan docker-goof-n6-slim
```

{% hint style="info" %}
Check out the [Docker Scan documentation](https://docs.docker.com/engine/scan/) for all possible CLI options.
{% endhint %}

Scanning images for Open Source vulnerabilities with Snyk is that easy! When finished, scan results are displayed in the Terminal, along with fix advice.

## Step 4: Review Vulnerability Scan Results

Vulnerabilities are broken up into sections, based on how they were introduced:

### Vulnerable Base Image Packages

Vulnerabilities introduced by the container's base image can be identified by the presence of the `Introduced by your base image` line. (Line 9 below)

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

### User Instruction Vulnerabilities

Some vulnerabilities are introduced by User Instruction in the Dockerfile. Snyk highlights the command that introduced the vulnerability, with the `Introduced in your Dockerfile by` line. (Line 9)

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

### **Vulnerable App Dependencies**

The last kind of vulnerability your images might contain are introduced by your application dependencies. Snyk highlights the package manifest `Target File` that introduced it. (Line 14)

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
Check out the [Snyk Documentation for Info around Container CLI Results](https://support.snyk.io/hc/en-us/articles/360003946937-Understanding-container-CLI-scan-results)
{% endhint %}

## Step 5: Review Base Image Recommendations

Snyk's fix advice helps developers spend less time fixing, and more time developing! One way to tackle vulnerabilities is by choosing a more secure base image. By providing the Dockerfile to `docker scan` , Snyk can suggest other Base Images that can be used in the Dockerfile's `FROM` statement to bring down those vulnerability counts.

These are grouped by how likely they are to be compatible with your application:

* `Minor` upgrades are the most likely to be compatible with little work,
* `Major` upgrades can introduce breaking changes depending on image usage,
* `Alternative` architecture images are shown for more technical users to investigate.

{% hint style="info" %}
These suggestions are not a substitute for proper integration testing. They are intended to help you narrow down potential base image choices.
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

## Step 6: Apply a more Secure Base Image

Let's choose a more secure base image for docker-goof. We'll do this by applying the `Minor` upgrade recommended by Snyk. Change the FROM statement in the Dockerfile:

```bash
# Comment out the old FROM Statement
# FROM node:10.4.0

# Write in the new one
FROM node:10.22

RUN apt-get install -y imagemagick
```

Now build the new Image. To compare results side-by-side with the previous scan, we'll specify a different tag when building the image.

```bash
docker build -t docker-goof:v2 -f Dockerfile .
```

## Step 7: Scan your Image for vulnerabilities with Snyk

Now let's use `docker scan` to scan for vulnerabilities. Once again, pass the `Dockerfile` used to build the image with `--file` to get more robust results.

```bash
# Scanning the docker-goof image and passing the Dockerfile 
docker scan docker-goof:v2 --file=Dockerfile
```

{% hint style="info" %}
Check out the [Docker Scan documentation](https://docs.docker.com/engine/scan/) for all possible CLI options.
{% endhint %}

Continue this cycle of build-scan-push until you're running the most secure base image.

## Recap: Additional Resources & Docker Hub Promotion!

We hope you enjoyed this Lab! In this pattern, we checked for vulnerabilities in Images using the Docker CLI, and saw vulnerabilities introduced by our Base Image, Dockerfile instructions, and application dependencies.

Applying a more secure base image is a great first step toward making your images more secure. As noted above, vulnerabilities can come from your application dependencies and Dockerfile user instructions as well. Check out other courses in the Snyk Academy to learn how Snyk can help you fix and reduce the other vulnerabilities in your images.

As we continue to evolve our Partnership with Docker, we'll keep adding new capabilities that help developers build their container images securely and deploy with confidence. Try out this workflow on your own applications, and let us know what you think!

{% hint style="success" %}
Other courses in the Snyk Academy may require a Snyk Account. Don't forget - new accounts that [Sign in with Docker Hub](https://snyk.co/SnykDockerAcademy) unlock a promotional free tier limit of 200 scans per month!
{% endhint %}
