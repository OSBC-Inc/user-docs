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

### Module 1 - Scanning & monitoring application source code

Enable the Snyk Open Source [integration](https://solutions.snyk.io/snyk-academy/open-source/create-source-control-integration) to Bitbucket and [import your SCM project](https://solutions.snyk.io/snyk-academy/open-source/import-scm-project). Understand transitive dependencies and how Snyk can generate automatic pull requests to streamline your process.

### Module 2 - Scanning & monitoring container images

Enable Snyk Container [integration](https://support.snyk.io/hc/en-us/articles/360003916078-Configure-integration-for-Amazon-Elastic-Container-Registry-ECR-) to Amazon Elastic Container Registry (ECR) and [import](https://solutions.snyk.io/snyk-academy/container/container-registry-and-image-import) your container images. Learn how Snyk provides base image ugprade recommendations.

### Module 3 - Scanning & monitoring for insecure Kubernetes configurations

[Install the Snyk controller](https://support.snyk.io/hc/en-us/articles/360011128137-Install-the-Snyk-controller-on-Amazon-Elastic-Kubernetes-Service-Amazon-EKS-) on Amazon Elastic Kubernetes Service (Amazon EKS) and [add workloads for scanning](https://support.snyk.io/hc/en-us/articles/360003947117-Adding-Kubernetes-workloads-for-security-scanning). Understand test results, how to interpret Snyk's [Priority Score](https://support.snyk.io/hc/en-us/articles/360010906897-Snyk-Priority-Score-and-Kubernetes), and how to fix configuration issues.

### Module 4 - Fixing known issues & monitoring

In this module, you will go through guided exercises that demonstrate how to fix for vulnerabilities and insecure configurations. You will apply what you learned in the previous modules and apply fixes to your application, container image, and Kubernetes configuration to secure your application.

{% hint style="info" %}
To make the most effective use of this content, you should be able to run basic Unix commands. You should also possess familiarity with AWS services, basic cloud concepts and general understanding of software development methodologies.
{% endhint %}
