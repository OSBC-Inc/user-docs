# TeamCity 통합

Snyk Security 플러그인을 JetBrains Continuous Integration(CI) 도구인 TeamCity와 통합하여 오픈 소스 취약점 검색을 자동화된 빌드 체인에 직접 포함시킵니다. TeamCity 통합은 빌드의 일부로 프로젝트의 취약점을 검색하는 추가 빌드 단계를 추가합니다. 스캔 후 프로젝트를 Snyk에 푸시하여 지속적인 모니터링을 수행할 수 있습니다.

Snyk 플러그인은 빌드의 일부로 스캔한 다음 TeamCity UI에서 직접 테스트 결과를 표시합니다. 이를 통해 취약점에 대한 수정이 제공되거나 새로운 취약점이 공개됨에 따라 애플리케이션의 보안이 위험한 문제를 보다 빠르고 신속하게 추적, 식별 및 해결할 수 있습니다.

## 지원하는 개발 언어 및 저장소

Snyk은 사용하는 Git 저장소에 관계 없이 모든 TeamCity 프로젝트를 지원합니다.

TeamCity 및 Snyk에서 지원하는 모든 개발 언어는 플러그인으로 취약점을 스캔할 수 있습니다.

## TeamCity 통합의 작동 방식

TeamCity 프로젝트와 함께 Snyk 플러그인을 사용하여 지속적으로 코드를 테스트하고 취약점을 모니터링합니다. 프로젝트와 관련하여 새로 공개된 취약점이 발표될 때 빌드가 손상되고 구성에 따라 관련 알림을 받을 수 있습니다.

1. TeamCity 계정 관리자가 설치할 Snyk 플러그인을 선택합니다.
2. TeamCity는 플러그인 디렉토리의 서버에 플러그인을 설치합니다.
3. 관리자가 플러그인을 사용하도록 설정합니다.
4. 사용자가 프로젝트를 생성하거나 기존 프로젝트를 업데이트하여 Snyk Security를 빌드 단계로 추가합니다.
5. 사용자는 Snyk Security 단계의 구성(API 토큰, 정책 변경 등)을 포함하여 빌드를 구성합니다.
6. Snyk은 빌드에서 구성한 API 토큰을 사용하여 계정을 인증합니다.
7. 사용자가 빌드를 실행합니다.
8. 빌드하는 동안 취약점을 검사하기 전에 정책 구성에 따라 필요에 따라 Snyk installation이 백그라운드에서 확인 및 업데이트됩니다.
9. 그런 다음 Snyk은 프로젝트의 매니페스트 파일을 분석하여 프로젝트 유형을 자동으로 탐지하여 직접 의존성 및 의존성 전이를 찾고 Snyk 취약점 데이터베이스에 대해 프로젝트를 테스트하여 알려진 취약점을 확인합니다.
10. **Snyk Security Report** 탭은 TeamCity의 테스트 결과를 빌드 세부 정보에 표시합니다. 결과는 알려진 이슈의 수와 식별된 관련 의존성 경로의 수를 나타냅니다.
11. 사용자가 이 프로젝트의 **Monitor project on build** 구성 설정을 선택하지 않은 경우 다음과 같은 결과가 나타납니다.
    1. Snyk은 TeamCity의 **Snyk Security Report** 탭에서 모든 취약점 결과 및 세부 정보를 표시합니다.
    2. 프로젝트에서 확인된 취약점에 할당된 심각도에 대해 심각도 임계값이 지정된 경우 TeamCity는 빌드를 중단합니다. 그렇지 않은 경우, TeamCity는 빌드를 완료(성공 또는 실패)까지 계속 실행하고 Snyk 활동이 종료됩니다.
12. 사용자가 **Monitor project on build** 옵션을 구성한 경우 Snyk은 `snyk monitor` 명령을 실행하고나머지 단계를 진행합니다.
    1. Snyk는 프로젝트의 스냅샷을 만들고 프로젝트의 매니페스트 파일을 분석하여 직접 의존성 및 의존성 전이를 찾고 Snyk 취약점 데이터베이스에 대해 프로젝트를 테스트하여 알려진 취약점을 확인합니다.
    2. Snyk이 스냅샷을 Snyk UI로 푸시합니다. 스냅샷에는 프로젝트 상세 내역 및 의존성 계층뿐만 아니라 취약점 결과 및 수정 조언이 표시됩니다.
    3. 프로젝트의 취약점에 할당된 심각도에 대해 심각도 임계값이 지정된 경우 TeamCity는 빌드를 중단합니다.
    4. 스냅샷이 Snyk UI로 푸시되면 Snyk는 새로운 취약점이 공개됨에 따라 프로젝트를 계속 모니터링합니다. 구성에 따라 취약점이 발견되면 즉시 수정 작업을 수행할 수 있도록 Snyk이 전자 메일 또는 Slack을 통해 알려 줍니다.

Snyk 단계로 빌드를 구성하는 방법은 [Team City integration: use Snyk in your build](teamcity-integration-use-snyk-in-your-build/)를 참조하십시오.

## Snyk plugin 설치

다음 단계에 따라 Snyk Security 플러그인을 설치하거나 업그레이드합니다. 설치가 완료되면 프로젝트에 Snyk 단계를 추가할 수 있습니다.

**Note:** 시작하기 전에 Snyk 계정을 등록하십시오.

1. TeamCity 인스턴스에 로그인하여 Snyk Security 플러그인을 설치합니다. 백그라운드에서 **정기적으로 자동 업그레이드**되도록 플러그인 목록을 구성하여 플러그인 업데이트를 주기적으로 확인합니다.
2. [JetBrains Plugins Repository](https://plugins.jetbrains.com/plugin/12227-snyk-security)로 이동하여 Snyk을 검색한 후 Get dropdown 목록에서 TeamCity 설치에 사용할 플러그인을 선택합니다.
3. 프롬프트에 응답하여 **Install**를 클릭합니다.
4. 설치가 끝나고 플러그인이 업로드되었음을 알리는 **Administration Plugins List**가 로드되면 플러그인이 사용하도록 설정되었는지 확인합니다.

![Install plugin from the JetBrains Plugins Repository](../../../../.gitbook/assets/uuid-fe65f4bc-9578-016c-00dd-6ddb97d2ead7-en.png)

통합을 구성하려면 [TeamCity configuration parameters](teamcity-configuration-parameters.md)를 참조하십시오. Snyk 단계로 빌드를 구성하는 방법은 [Team City integration: use Snyk in your build](teamcity-integration-use-snyk-in-your-build/)를 참조하십시오.
