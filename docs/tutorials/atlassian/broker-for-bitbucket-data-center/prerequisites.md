---
description: Bitbucket Data Center용 Snyk Broker에 필요한 것
---

# 전제 조건

이 튜토리얼에서는 다음이 있다고 가정합니다:

* 인프라 또는 클라우드에서 실행되는 Bitbucket Data Center
* Snyk 계정

{% hint style="info" %}
Snyk Broker의 기본 요구 사항은 [Snyk Broker](https://docs.snyk.io/features/snyk-broker) 문서에 설명되어 있습니다. 필요한 요구 사항 중 일부를 강조합니다.
{% endhint %}

컨테이너 또는 AWS Quick Start를 포함하여 인프라에 Snyk Broker를 설치하는 몇 가지 옵션이 있습니다.

시작하려면 다음이 필요합니다:

* Snyk의 지원 팀에서 제공하는 사용 중인 특정 유형의 통합에 대한 브로커 토큰. 이 자습서에서는 Bitbucket 서버 연결을 사용합니다. 다른 옵션의 예는 설명서 사이트의 목록을 참조하십시오.
* Bitbucket Data Center 인스턴스에 대한 관리 권한.
* 프로젝트를 가져오기 위한 snyk.io의 권한.
* Snyk Broker의 성공적인 설치. [Snyk 설명서](../../../features/integrations/git-repository-scm-integrations/bitbucket-data-center-server-integration.md)에 설명된 대로 해당 인스턴스의 구성에 대해 다음 정보를 제공했을 것입니다:
  * Bitbucket 사용자 이름
  * Bitbucket 암호
  * Bitbucket 호스트 이름
  * Bitbucket API Endpoint
