---
description: 환영합니다! 이 랩에서는 Docker Desktop, Docker Hub, GitHub 및 Snyk를 사용하는 워크플로를 보여줍니다.
---

# Docker 및 Snyk으로 보안 컨테이너 구축

## Lab Meta

> 난이도: 입문
>
> 소요시간: 약 30분

이 실습에서는 [Docker Build: Build Secure Containers with Docker and Snyk](https://www.youtube.com/watch?v=RGCHHaYP9Lw)에 표시된 데모를 안내합니다. 세 가지 방법으로 컨테이너화된 애플리케이션을 보호합니다.

1. 먼저 컨테이너가 안전한 **기본 이미지**를 사용하는지 확인합니다.
2. 다음으로 **취약한 애플리케이션 종속성**을 해결합니다.
3. 마지막으로 잘못된 구성에 대한 **배포 매니페스트**를 확인합니다.

### 전제 조건

#### Snyk

이 실습에는 Snyk 계정이 필요합니다. 필요한 경우 [snyk.io에서 무료로 가입](https://snyk.co/SnykDockerAcademy)하세요.

{% hint style="info" %}
스닉이 처음이신가요? Docker Desktop을 설치한 후 `docker scan --login`을 실행하고 Docker ID로 등록하여 Snyk 컨테이너에 대한 스캔 한도가 200인 무료 특별 계층 (일반적으로 100)을 잠금 해제하십시오!
{% endhint %}

{% hint style="info" %}
Snyk은 [오픈 소스 프로젝트에 대한 무제한 테스트](https://snyk.io/blog/snyk-projects-now-free/)를 제공합니다. 우리는 오픈 소스를 사랑합니다!
{% endhint %}

#### Docker

Docker ID가 필요합니다. 필요한 경우 [Docker Hub에 등록](https://hub.docker.com/signup)하십시오. 또한 [Docker Desktop](https://www.docker.com/products/docker-desktop)을 다운로드 및 설치하고 제공되는 [Kubernetes 클러스터를 활성화](https://birthday.play-with-docker.com/kubernetes-docker-desktop/)합니다.

#### GitHub

GitHub 계정이 필요합니다. 필요한 경우 [GitHub에서 무료로 등록](https://github.com/join)하세요. 이 실습에서는 GitHub Actions도 사용합니다. GitHub Actions를 처음 사용하는 경우 [GitHub Actions 소개](https://docs.github.com/en/actions/learn-github-actions/introduction-to-github-actions)는 훌륭한 기본 소개서입니다.

준비가 되면 다음 페이지로 이동하여 시작하세요!
