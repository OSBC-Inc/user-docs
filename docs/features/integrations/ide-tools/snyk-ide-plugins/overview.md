---
description: 통합 전략 이해
---

# IDE 플러그인 개요

이 문서에서는 Snyk CLI를 사용하여 Snyk 스캔 결과를 추출하고 IDE 플러그인에서 사용할 수 있도록 하는 방법을 보여줍니다. IDE 플러그인은 백그라운드에서 CLI를 다운로드하고 주기적으로 최신 버전을 확인하고 사용 가능한 경우 다운로드합니다.

Snyk SDK를 사용하면 주기적인 업데이트를 더 쉽게 구현하고 다운로드할 수 있습니다. 이 통합이 개발 중이지만 [Java implementation](https://github.com/jenkinsci/snyk-security-scanner-plugin/blob/master/src/main/java/io/snyk/jenkins/tools/internal/DownloadService.java)을 사용할 수 있습니다.

{% hint style="info" %}
개발자의 컴퓨터에 Snyk CLI가 설치되어 있는지 여부에 관계없이 IDE 사용을 위해 Snyk CLI를 다운로드합니다.
{% endhint %}

Snyk CLI를 사용하려면 인증해야 합니다. 사용자가 이 시스템에서 이전에 인증되었는지 확인하려면 `snyk config get api`를 실행하고 UUID의 반환을 확인하십시오. 필요한 경우 `snyk auth`를 실행하고 프롬프트에 따라 가입 및 로그인합니다. 이 프로세스는 Snyk 토큰을 사용자 컴퓨터에 로컬로 저장합니다. 자세한 내용은 [Snyk에 대한 사용자 인증](../../../snyk-cli/cli-command/undefined.md)을 참조하십시오.

`--json` 옵션과 함께 Snyk CLI `test` 명령을 사용하여 출력을 기계가 읽을 수 있는 형식으로 변환합니다. 프로젝트에서 지원되는 모든 종속성 매니페스트 파일에 대해 `snyk test --file=<manifest file name> --json` 을 실행하고 결과를 구문 분석하고 IDE 사용자 인터페이스 내부의 원하는 위치에 표시해야 합니다.

주기적으로 또는 트리거 이벤트가 발생할 때 `snyk test`를 다시 실행하십시오: 매니페스트 파일이 편집되었거나, 마지막 스캔 이후 하루가 지났으며, 종속성을 명시적으로 다시 설치할 때마다(`mvn install`).

요약하면 단계는 다음과 같습니다.

1. Snyk CLI가 있는지 확인하거나 사용자에게 설치하라는 메시지를 표시합니다(한 번).
2. 사용자가 CLI에 대해 인증되었는지 확인하고 인증되지 않은 경우(한 번) snyk auth를 실행합니다.
3. `snyk test --file=<manifest file name> --json` 출력을 구문 분석하고 IDE 사용자 인터페이스에 통합하여 모든 매니페스트 파일을 스캔합니다.
4. 주기적으로 또는 트리거 이벤트가 발생할 때 스캔을 다시 실행하십시오. [IDE 플러그인으로 스캔](scanning.md#607b2cd8-2fb5-49ee-8473-319a42b8c421)을 참조하십시오.
