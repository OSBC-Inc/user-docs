# Snyk Security

## 소개

이 모듈은 이 워크샵에서 생성되는 애플리케이션 및 **Docker** 컨테이너의 **오픈 소스 종속성**을 스캔하도록 설계되었습니다. 이 모듈에 필요한 파일은 이미 생성되어 /modules/snyk 폴더에 있습니다. 아래 단계를 수행하는 동안 복사합니다.

### 배경

**Snyk**은 조직이 오픈 소스 종속성을 찾고 수정하고 방지하고 모니터링하는 데 사용하는 **SaaS** 제품입니다. Snyk는 SDLC(Software Development Lifecycle)에 쉽게 통합할 수 있는 개발자 우선 플랫폼입니다.

모듈의 이 시점에서 `Petstore` 애플리케이션이 생성되므로 빌드 프로세스 동안 중요한 보안 게이트의 일부로 Snyk을 삽입할 것입니다.

이 모듈에서는 심각도가 높은 문제가 발견되면 빌드를 실패하여 수정 사항을 적용하는 방법을 보여줍니다.

### Snyk CLI

Snyk 명령줄 인터페이스(CLI)에는 이 연습을 위한 세 가지 주요 명령이 있습니다.

* CLI를 계정에 연결하고 테스트를 수행할 수 있는 권한을 부여하는 `snyk auth`.
  * 하드 코딩 토큰을 피하기 위해 Amazon's System Manager Parameters를 사용하여 이 토큰을 저장합니다.
  * **snyk 인증**을 사용하는 대신 CLI가 자동으로 감지하는 **환경 변수** SNYK\_TOKEN을 설정할 수도 있습니다.
* `snyk test`는 실제 테스트를 수행하고 빌드에 실패할 수 있습니다.
* `snyk monitor`는 계정을 생성한 `snyk.io` 인터페이스에 대한 지속적인 모니터링 및 보고를 위한 스냅샷을 게시합니다.

### 이 Lab의 작업

이 모듈의 목적을 위해 Snyk은 **애플리케이션**이 빌드될 때와 **Docker container**가 생성될 때의 두 가지 주요 프로세스에 삽입됩니다.

이 모듈에는 5개의 섹션이 있습니다:

1. `https://snyk.io/` 에서 테스트용 토큰을 얻습니다.
2. 애플리케이션 스캔 설정
3. Docker 분석 설정
4. 테스트 실행 및 감지된 문제 수정
5. Snyk 대시보드에서 상태 보기
