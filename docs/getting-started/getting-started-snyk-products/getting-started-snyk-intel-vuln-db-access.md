# Snyk intel vulnerability DB 액세스 시작하기

## 소개

Snyk의 [vulnerability database](https://snyk.io/product/vulnerability-database/)에는 Snyk 제품이 코드 취약점을 찾고 수정하는데 사용하는 주요한 보안 정보가 포함되어 있습니다.

이미 자체 제품을 보유하고 있는 고객의 경우에는 Snyk의 전문적인 내용과 축적된 내용을 해당 데이터베이스에 대한 액세스를 통해 이점을 가져갈 수 있어 개발 팀이 신뢰할 수 있는 인텔리전스에 액세스하여 오픈 소스 및 컨테이너 코드를 신속하게 보호할 수 있습니다.

## 프로세스 개요

1. Snyk은 회사의 통합을 설정하는데 도움이 됩니다.
2. Snyk은 액세스 지침이 포함된 설명서를 제공합니다.
3. Snyk은 DB 정보를 포함하는 내용을 일반적으로 JSON파일로 전송합니다([sample code](https://snyk.io/partners/api/v4/vulndb/sample.json) 참조) **Note**: 파일을 데이터베이스에 저장하는 것이 좋습니다.
4. 시스템에서 DB 정보를 사용하는 코드를 작성합니다.

## DB 소개

보안 전문가 및 분석가 팀은 Snyk의 보안 데이터베이스를 관리하여 데이터베이스가 높은 정확도를 유지하고 오탐지를 방지할 수 있도록 합니다.

* 데이터베이스의 모든 항목이 분석되고 검증됩니다.
* 새로운 취약점을 발견하기 위한 연구에 투자합니다. [disclosed vulnerability list](https://app.snyk.io/disclosed-vulnerabilities) 참조하세요.

## Database 피드

Snyk의 보안 데이터베이스에는 두 가지 피드가 포함되어 있습니다.

* 애플리케이션 보안 취약점: 해당되는 경우 코드를 포함하여 수동으로 콘텐츠를 선별하고 요약하여 Snyk Open Source를 지원합니다.
* Snyk Container를 지원하는 Linux OS의 취약점.

두 피드 옵션은 직접 라이선스를 받을 수 있습니다.
