---
title: Module 2
chapter: true
weight: 40
---

# Module 2

## Container 보안

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-bitbucket-flow-module-02.png)

2022년까지 [전 세계 조직의 75%](https://snyk.io/blog/putting-container-security-in-the-hands-of-developers/) 이상이 프로덕션에서 컨테이너화된 애플리케이션을 실행할 것입니다(Gartner). 광범위한 채택과 함께 2018년에 보고된 운영 체제 취약성이 4배 증가하면서 컨테이너 취약성이 급증했습니다. 하지만 [개발자의 80%는 개발 중에 컨테이너 이미지를 테스트하지 않는다](https://snyk.io/blog/shifting-docker-security-left/)고 말합니다. 또는 그들은 문제를 파악하는 길을 가는 누군가에게 익숙합니다. 즉, 빠르게 성장하는 비즈니스에서 [컨테이너 보안](https://snyk.io/container-security/)을 확장하는 것은 어려운 일입니다.

## 학습 목표

이 모듈에서는 Snyk를 사용하여 Bitbucket Pipes에서 [빌드 워크플로를 보호](https://snyk.io/blog/secure-your-build-workflow-on-bitbucket-pipes-with-snyk/)하는 방법을 배웁니다. 알려진 취약성에 대해 Linux 기반 컨테이너 프로젝트를 스캔하고 분석하는 것은 보안 취약성을 식별하고 완화하는 데 도움을 주어 환경을 보호하는 중요한 단계입니다. 이 모듈의 연습은 Bitbucket 파이프라인용 Snyk 파이프를 활용하여 기본 이미지에서 다음과 같은 종속성을 스캔하여 [컨테이너를 보호](https://support.snyk.io/hc/en-us/articles/360003946897-Container-security-overview)하는 데 도움이 됩니다.

* 패키지 관리자가 설치하고 관리하는 OS(Operating System) 패키지
* Key Binaries - 패키지 관리자를 통해 설치되지 않은 계층

이러한 결과를 바탕으로 Snyk은 다음을 포함한 수정 조언 및 지침을 제공합니다.

* OS 패키지 및 주요 바이너리의 취약점 원인
* 기본 이미지 업그레이드 세부 정보 또는 이미지 재구축 권장 사항
* 영향을 받는 패키지가 도입된 Dockerfile 계층
* 운영 체제 및 주요 바이너리 패키지의 고정 버전

Lastly, you will enable Snyk's integration for [Amazon Elastic Container Registry (ECR)](https://support.snyk.io/hc/en-us/articles/360003916078-Configure-integration-for-Amazon-Elastic-Container-Registry-ECR-) to continuously scan and monitor your container images.

## Homework: Learn more about Snyk & Container security

* [Container security throughout the SDLC](https://snyk.io/blog/container-security-throughout-the-sdlc/)
* [Everything you wanted to know about addressing security vulnerabilities in Linux-based containers](https://snyk.io/blog/everything-you-wanted-to-know-about-addressing-security-vulnerabilities-in-linux-based-containers/)
* [Protect container images directly from your registries](https://snyk.io/blog/protect-docker-images-directly-from-your-container-registries/)

**Footnotes:**

1. **\*Snyk Blog -** [Putting container security in the hands of developers](https://snyk.io/blog/putting-container-security-in-the-hands-of-developers)
