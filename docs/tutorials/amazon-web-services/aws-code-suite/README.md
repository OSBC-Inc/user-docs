---
title: DevSecOps with Snyk
chapter: true
weight: 1
---

# AWS Code Suite

{% embed url="https://youtu.be/cgsMsHO4Nbc" %}

이 워크숍에서는 AWS CodeCommit, AWS CodeBuild 및 AWS CodePipeline을 사용하여 컨테이너 애플리케이션의 CI/CD 파이프라인에 보안 테스트를 추가하는 방법을 배웁니다. 이 워크샵에 포함된 모듈은 자동화 방식으로 소프트웨어를 커밋, 빌드, 테스트 및 배포하기 위한 단계별 지침을 제공합니다. 또한 몇 가지 기본 보안 테스트와 소프트웨어 개발 수명 주기에서 이를 계측할 위치에 대해서도 배우게 됩니다.

## 목표

* 최신 애플리케이션의 워크플로에 익숙해지기
* CI/CD 파이프라인에 보안 테스트를 추가할 위치 알아보기
* 테스트를 조정하는 데 사용되는 AWS 서비스에 대해 알아보기

## 이번 워크숍에서 다룰 내용

* Cloud9 환경 설정
* AWS CloudFormation을 사용하여 인프라 배포 자동화
* Amazon Elastic Container Service 배포
* AWS CodePipeline, CodeCommit 및 CodeBuild를 사용하여 현대화된 파이프라인 배포 및 사용
* 몇 가지 보안 테스트/스캐닝 도구 계측

## 참조 아키텍처 샘플

이 워크샵이 끝나면 AWS 계정에 다양한 AWS 서비스가 프로비저닝됩니다. 다음 다이어그램은 이러한 서비스 중 일부를 보여주며 샘플 참조 아키텍처로 사용됩니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/aws-pipeline.png)

## 워크샵 순서

이 워크샵에 포함된 각 섹션 또는 모듈은 위에서 참조한 아키텍처를 구축하는 프로세스의 각 단계를 안내하도록 설계되었습니다. 이는 AWS Cloud 9를 시작점으로 저장소 콘텐츠 'git clone'을 사용하여 수행됩니다. 샘플 코드, AWS CloudFormation 템플릿 및 자세한 지침을 포함하여 필요한 모든 것이 제공됩니다. Cloud9 인스턴스의 AWS CLI를 사용하여 CloudFormation 템플릿을 배포하고 환경을 구축합니다.

{% hint style="info" %}
이 워크샵에서 제공되는 예제 및 샘플 코드는 교육용 콘텐츠로 사용하기 위한 것입니다.
{% endhint %}
