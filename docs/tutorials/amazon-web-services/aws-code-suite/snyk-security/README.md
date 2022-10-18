# Snyk Security

## 소개

이 모듈은 이 워크샵에서 생성되는 애플리케이션 및 **Docker** 컨테이너의 **오픈 소스 종속성**을 스캔하도록 설계되었습니다. 이 모듈에 필요한 파일은 이미 생성되어 /modules/snyk 폴더에 있습니다. 아래 단계를 수행하는 동안 복사합니다.

### 배경

**Snyk**은 조직이 오픈 소스 종속성을 찾고 수정하고 방지하고 모니터링하는 데 사용하는 **SaaS** 제품입니다. Snyk는 SDLC(Software Development Lifecycle)에 쉽게 통합할 수 있는 개발자 우선 플랫폼입니다.

At this point of the module, the `Petstore` application is created, so we will look to insert **Snyk** as part of an important security gate during the build process.

This module will demonstrate how to fail a build when high severity issues are found so that fixes can take place.

### Snyk CLI

The Snyk command line interface (CLI) has three key commands for this exercise:

* `snyk auth` which links the CLI to your account and authorizes it to perform tests.
  * We will utilize Amazon's System Manager Parameters to store this token to avoid hard-coding tokens.
  * Alternatively to using **snyk auth**, you can also set an **environment variable** `SNYK_TOKEN` which the CLI will automatically detect.
* `snyk test` performs the actual test and can fail a build
* `snyk monitor` posts a snapshot for continuous monitoring and reporting on the `snyk.io` interface where you created your account.

### 이 Lab의 작업

이 모듈의 목적을 위해 Snyk은 **애플리케이션**이 빌드될 때와 **Docker container**가 생성될 때의 두 가지 주요 프로세스에 삽입됩니다.

이 모듈에는 5개의 섹션이 있습니다:

1. `https://snyk.io/` 에서 테스트용 토큰을 얻습니다.
2. 애플리케이션 스캔 설정
3. Docker 분석 설정
4. 테스트 실행 및 감지된 문제 수정
5. Snyk 대시보드에서 상태 보기
