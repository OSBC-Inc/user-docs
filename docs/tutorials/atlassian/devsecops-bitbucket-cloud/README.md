# Bitbucket Cloud를 사용한 DevSecOps

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/finding-open-source-vulnerabilities-within-the-bitbucket-workflow-.png)

[Snyk](https://snyk.io/) 및 [Atlassian](https://www.atlassian.com/)과 함께 이 실습 가상 워크숍에 참여하여 워크플로 초기에 보안 모범 사례를 구현하여 자동화되고 안전한 [CI(Continuous Integratio)](https://www.atlassian.com/continuous-delivery/continuous-integration) 및 [CD(Continuous Delivery)](https://www.atlassian.com/continuous-delivery) 파이프라인을 구축하는 방법을 안내합니다.

## 환영합니다!

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/mm.png)

귀하는 Mythical 500 회사인 Mythical Mysfits의 최신 멤버로서 이 워크숍을 시작하게 됩니다. 사무실에 온 첫날이고 전임자가 급하게(즉, 수동으로) 그룹 공동 작업을 위해 "엔터프라이즈용" 소프트웨어를 배포했습니다. 동료들에 따르면 [goof](https://github.com/snyk/goof)는 "The BESTest todo app evar"로 엄청난 인기를 얻었습니다. 그러나 당신은 회의적입니다. 다행히 귀사는 최근에 Snyk와 Atlassian Bitbucket Cloud를 구입했습니다!

이 워크숍에서는 [Atlassian Bitbucket](https://www.atlassian.com/software/bitbucket), [Bitbucket Pipelines](https://bitbucket.org/product/features/pipelines) 및 [Snyk](https://snyk.io)를 활용하는 시프트 레프트 보안 패턴을 배웁니다. 이러한 기술을 사용하면 [Amazon EKS(Amazon Elastic Kubernetes Service)](https://aws.amazon.com/eks/) 및 [ECR(Amazon Elastic Container Registry)](https://aws.amazon.com/ecr/)에서 실행되는 컨테이너 기반 워크로드의 스캔을 구현하고 이러한 패턴을 사용하여 보안을 포함하는 특징과 기능을 더 빠른 속도로 릴리스하는 방법을 각 단계에서 구현할 수 있습니다.

## 학습 목표

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-bitbucket-flow.png)

* [SCA(Software Composition Analysis)](https://snyk.io/blog/what-is-software-composition-analysis-sca-and-does-my-company-need-it/)와 개발자 워크플로에서의 중요성을 이해합니다.
* 애플리케이션 오픈 소스 종속성에서 취약점을 발견합니다.
*   Implement Snyk's [container image](https://snyk.io/blog/detecting-vulnerabilities-in-container-images/) scanning in your [Continuous integration](https://aws.amazon.com/devops/continuous-integration/) and

    [Continuous delivery](https://aws.amazon.com/devops/continuous-delivery/) (CI/CD) pipeline.
* [Continuous integration](https://aws.amazon.com/devops/continuous-integration/)과 [Continuous delivery](https://aws.amazon.com/devops/continuous-delivery/) (CI/CD)파이프라인에서 Snyk의 [컨테이너 이미지](https://snyk.io/blog/detecting-vulnerabilities-in-container-images/) 스캐닝을 구현합니다.
* [소스에서 안전하지 않은 Kubernetes 구성을 수정합니다.](https://snyk.io/blog/fix-insecure-kubernetes-configuration/)
* Bitbucket Pipelines용 [Snyk Pipe](https://bitbucket.org/product/features/pipelines/integrations?p=snyk/snyk-scan)를 활용하여 애플리케이션을 보호하십시오.

## 대상 청중

* 개발자
* 보안/애플리케이션 팀
* DevOps/DevSecOps 엔지니어
* 클라우드/솔루션 설계자

## 콘텐츠 구조

이 워크샵에서 다루는 다양한 주제를 특정 모듈로 구성했습니다. 각 모듈은 실습 예제뿐만 아니라 제시된 기술의 이면에 있는 이론에 대한 컨텍스트를 제공합니다.

### 모듈 1 - 애플리케이션 소스 코드 스캔 및 모니터링

Bitbucket에 대한 Snyk 오픈 소스 [통합](https://solutions.snyk.io/snyk-academy/open-source/create-source-control-integration)을 활성화하고 [SCM 프로젝트를 가져옵니다](https://solutions.snyk.io/snyk-academy/open-source/import-scm-project). 전이적 종속성과 Snyk가 자동 풀 요청을 생성하여 프로세스를 간소화하는 방법을 이해합니다.

### 모듈 2 - 컨테이너 이미지 스캔 및 모니터링

ECR(Amazon Elastic Container Registry)에 대한 Snyk 컨테이너 [통합](https://support.snyk.io/hc/en-us/articles/360003916078-Configure-integration-for-Amazon-Elastic-Container-Registry-ECR-)을 활성화하고 컨테이너 [이미지를 가져옵니다](https://solutions.snyk.io/snyk-academy/container/container-registry-and-image-import). Snyk가 기본 이미지 ugprade 권장 사항을 제공하는 방법을 알아보세요.

### 모듈 3 - 안전하지 않은 Kubernetes 구성 스캔 및 모니터링

Amazon EKS(Amazon Elastic Kubernetes Service)에 [Snyk 컨트롤러를 설치하고](https://support.snyk.io/hc/en-us/articles/360011128137-Install-the-Snyk-controller-on-Amazon-Elastic-Kubernetes-Service-Amazon-EKS-) 스캔을 위한 [워크로드를 추가](https://support.snyk.io/hc/en-us/articles/360003947117-Adding-Kubernetes-workloads-for-security-scanning)합니다. 테스트 결과, Snyk의 [우선 순위 점수](https://support.snyk.io/hc/en-us/articles/360010906897-Snyk-Priority-Score-and-Kubernetes) 해석 방법 및 구성 문제 해결 방법을 이해합니다.

### 모듈 4 - 알려진 문제 수정 및 모니터링

이 모듈에서는 취약성 및 안전하지 않은 구성을 수정하는 방법을 보여주는 연습 안내를 진행합니다. 이전 모듈에서 배운 내용을 적용하고 애플리케이션, 컨테이너 이미지 및 Kubernetes 구성에 수정 사항을 적용하여 애플리케이션을 보호합니다.

{% hint style="info" %}
이 콘텐츠를 가장 효과적으로 사용하려면 기본 Unix 명령을 실행할 수 있어야 합니다. 또한 AWS 서비스, 기본 클라우드 개념 및 소프트웨어 개발 방법론에 대한 일반적인 이해에 익숙해야 합니다.
{% endhint %}
