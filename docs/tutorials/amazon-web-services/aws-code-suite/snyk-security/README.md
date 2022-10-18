# Snyk Security

## 소개

This module is designed to introduce scanning **open source dependencies** of the application and the **Docker** container that is created during this workshop. The files required for this module have already been created and reside in the /modules/snyk folder. You will copy these over while following the steps below.

### 배경

**Snyk** is a **SaaS** offering that organizations use to **find, fix, prevent and monitor** open source dependencies. Snyk is a developer first platform that can be easily integrated into the Software Development Lifecycle (SDLC).

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
