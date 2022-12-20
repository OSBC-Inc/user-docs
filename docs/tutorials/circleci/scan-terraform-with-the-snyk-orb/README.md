---
description: >-
  이것은 Snyk Orb가 Terraform 파일에서 잘못된 구성을 쉽게 스캔하는 데 어떻게 도움이 되는지 보여주는 CircleCI
  Academy의 코드형 인프라 101 과정에 대한 추가 모듈입니다.
---

# Snyk Orb로 Terraform 스캔

## Lab Meta

> **난이도**: 중급
>
> **소요 시간:** 15 분

## 소개

Terraform을 사용하면 구성 파일을 작성하는 것처럼 쉽게 클라우드 인프라를 만들고 해체할 수 있습니다. CircleCI Academy의 코드형 인프라 과정에서 Terraform을 사용하여 GKE 클러스터를 만들고 지속적 배포 파이프라인의 일부로 여기에 애플리케이션을 배포하는 워크플로를 만들었습니다.

NSA에 따르면 [잘못된 구성은 클라우드의 가장 큰 취약점입니다](https://www.cloudhesive.com/blog-posts/misconfiguration-top-cloud-vulnerability/). 이 애드온 모듈에서는 안전한 IaC 개발 사례를 강화하기 위해 [Snyk Infrastructure as Code](https://snyk.io/product/infrastructure-as-code-security/)를 워크플로에 추가하여 Terraform 파일이 클러스터 및 클러스터에서 실행 중인 애플리케이션을 위험에 노출시키는 방식으로 구성되지 않도록 합니다. 클라우드 구성 오류로 인해 발생합니다. 시작합니다!

## 전제 조건:

### 권장 사전 작업

이 실습에서는 CircleCI Academy에서 다음 과정을 완료했다고 가정합니다:

{% embed url="https://academy.circleci.com/infrastructure-as-code" %}
CircleCI Academy의 코드형 인프라 101
{% endembed %}

{% embed url="https://academy.circleci.com/orbs-course" %}
CircleCI 아카데미의 오브
{% endembed %}

{% hint style="warning" %}
진행하기 전에 과정을 완료하는 것이 좋습니다.
{% endhint %}

### 샘플 코드

Infrastructure as Code 과정에서 사용된 것과 동일한 코드를 사용합니다. GitHub에서 찾을 수 있습니다.

{% embed url="https://github.com/datapunkz/learn_iac" %}

### Snyk 계정 및 토큰

Snyk Orb를 사용하려면 Snyk 계정이 필요합니다. [Snyk API 토큰을 만든](https://support.snyk.io/hc/en-us/articles/360004008278-Revoking-and-regenerating-Snyk-API-tokens) 다음 해당 값으로 SNYK\_TOKEN이라는 [CircleCI의 환경 변수를 설정](https://circleci.com/docs/2.0/env-vars/#setting-an-environment-variable-in-a-project)합니다.

준비가 되면 다음 페이지로 계속 진행합니다.
