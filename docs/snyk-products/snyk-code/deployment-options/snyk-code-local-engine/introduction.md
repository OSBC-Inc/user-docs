# 소개

### 개요

Snyk Code 로컬 엔진은 Snyk Code 엔진이 완전히 포함된 버전으로, 사용자가 자신의 소스코드를 인터넷에 업로드하지 않아도 됩니다.

이 높은 수준의 아키텍처 다이어그램은 다양한 요소들과 그들의 상호작용을 보여줍니다.

![Snyk Code Local Engine Architecture](<../../../../.gitbook/assets/Screen Shot 2021-11-11 at 2.36.41 PM.png>)

{% hint style="info" %}
스캔만 로컬에서 수행됩니다. 검색 결과가 Snyk에 업로드되어 일반 호스팅된 Snyk UI에서 볼 수 있습니다.
{% endhint %}

### 시스템 요구 사항

Snyk Code 로컬 엔진을 배치하기 위한 핵심 요구 사항은 다음과 같습니다.

* 쿠버네티스 version 1.16.0 - 1.21.5
* **각각** 다음과 같은 사양을 가진 3개의 노드
  * CPU 32 cores
  * RAM 120GB
  * Disk 500 GB (>300GB 임시 저장소)
* Helm 3.5.0
