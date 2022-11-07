---
description: 다중 통합을 사용하여 코드 및 인프라 구축 및 테스트
---

# Bitbucket Cloud 및 Kubernetes를 사용한 DevOps Pipeline

다중 통합을 사용하여 코드 및 인프라 빌드 및 테스트 이 워크샵에서는 실행 중인 환경에 대한 컨테이너로 코드를 체크아웃, 빌드, 테스트 및 배포하는 파이프라인을 통해 작업합니다. 이 사용 사례는 대부분의 사용자가 접하는 전형이며 워크숍은 Snyk 일상 활동에 어떻게 연결될 수 있는지 보여주기 위해 설계되었습니다.

이 워크샵은 Goof라는 인기 있는 취약한 애플리케이션의 Java 버전으로 시작합니다. Github의 소스는 [https://github.com/snyk-labs/java-goof](https://github.com/snyk-labs/java-goof)이고 우리는 그 과정에서 여러 통합을 강조하는 파이프라인 예제를 통해 작업할 것입니다.

## 학습 목표

실습 예제와 함께 다음 개념을 강조하기 위해 예제를 통해 작업할 것입니다:

* Bitbucket 리포지토리의 코드 기반부터 시작하여 Snyk가 오픈 소스 취약점에 대한 적시 정보를 제공할 수 있도록 합니다.
* Snyk 작동 중인 Atlasssian Bitbucket Pipeline에 통합하여 CI/CD 파이프라인의 일부로 컨테이너 이미지의 취약점을 드러냅니다.
* 실행 중인 환경에 컨테이너를 배포하고 Kubernetes 매니페스트에서 추가 런타임 취약점을 공개합니다.
* 취약점과 익스플로잇 간의 상관관계를 보여드리겠습니다. 그런 다음 수정 사항을 코드에 적용하여 수정 사항을 표시합니다.

## 타겟 고객

이 워크샵은 다음  개발 팀 구성원을 위해 설계되었습니다:

* 코드를 작성하고 시기 적절한 피드백으로 취약점을 수정할 수 있는 개발자.
* 보안 스캔 결과를 사용하여 개발 팀이 보안 수정 사항의 우선 순위를 정하는 데 관심이 있는 보안 팀.
* 잘 실행되고 규정을 준수하는 파이프라인을 적시에 보안과 함께 제공할 책임이  DevOps/DevSecOps 엔지니어.
* Any other member with the shared interest of delivering code with better security.

## 콘텐츠 구조

This workshop is developed in several modules to address the interests of different stages of your team's workflow. As a representative use case, you may find the use cases align very well with your team's structure. If your pipeline operations are different, you should still see how the desired outcomes for each use case still map to your processes.

### 모듈 1 - 개발자 워크스테이션에서 소스 코드 스캔 및 모니터링

In this module, you enable Snyk to automatically scan your repository and quickly provide results to your entire team. This example shows you how you and your team can leverage Snyk to easily create pull requests in your Bitbucket repository.

### 모듈 2 - 컨테이너 이미지 스캔 및 모니터링

Next, you'll enable Snyk to monitor your container images as you prepare them for deliver to AWS ECR. We'll use the feedback to make a change to a base image to address a vulnerability to improve the posture of your container image.

### 모듈 3 - 컨테이너 및 Kubernetes 클러스터 활용

In this module, we'll demonstrate a container exploit and expand the example into a cluster exploit. We'll remediate the vulnerability. This module requires features available to Snyk users in a paid Tier.
