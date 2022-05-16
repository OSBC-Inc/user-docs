# CircleCI 통합

Snyk은 **Snyk Orb**를 사용하여 [CircleCI](https://circleci.com/)와 통합하여 CI/CD(지속적 통합/지속적 배포) 워크플로우의 일부로 애플리케이션 종속성 및 Docker 이미지에 대한 오픈 소스 보안 취약점을 원활하게 검색합니다.

CircleCI를 사용하면 구성 파일에 추가할 수 있는 바로 사용할 수 있는 명령 그룹([Orbs](https://circleci.com/orbs/))을 사용하여 CI/CD 워크플로우를 쉽게 만들 수 있습니다.

Snyk Orb를 사용하면 구성에 따라 오픈 소스 취약점을 테스트하고 모니터링하기 위해 CI/CD에 Snyk scanning을 빠르게 추가할 수 있습니다. 그런 다음 결과는 CircleCI output view에서 표시되며 [Snyk.io](http://app.snyk.io/)에서도 모니터링할 수 있습니다.

## 시작 방법 <a href="#getting-started" id="getting-started"></a>

Snyk을 사용하여 CircleCI를 처음부터 green build로 시작하는 것은 간단합니다. Snyk Orb에 대한 자세한 내용은 다음 내용을 참조하십시오.

* ​[Snyk Circle CI README](https://circleci.com/orbs/registry/orb/snyk/snyk) - 파라미터 및 샘플 목록을 포함하여 Snyk로 CI/CD를 설정하는 데 필요한 모든 정보가 포함되어 있습니다.
* ​[A Circle CI blog post](https://circleci.com/blog/adding-application-and-image-scanning-to-your-cicd-pipeline/) - Snyk Orb로 보안 파이프라인을 설정하는 방법에 대해 설명합니다.

## CircleCI 통합 구성 <a href="#configure-your-circleci-integration" id="configure-your-circleci-integration"></a>

CircleCI에 프로젝트를 추가하고 구성 파일에 Snyk Orb를 추가하면 빌드가 실행될 때마다 Snyk Orb도 사용되며 다음 작업을 수행합니다.

### Scan <a href="#scan" id="scan"></a>

1. 앱 종속성 또는 컨테이너 이미지에 취약점 또는 라이센싱 문제가 있는지 검색하고 취약점 및 이슈를 나열합니다.
2. Snyk이 취약점을 발견하면(사용자 구성에 따라) 다음 중 하나를 수행합니다.
   * 빌드에 실패합니다
   * 빌드를 완료합니다

### **Monitor** <a href="#monitor" id="monitor"></a>

선택적으로 빌드가 성공적으로 완료되고 Snyk 단계에서 MONITOR가 True로 설정된 경우 Snyk은 Snyk Web UI에서 프로젝트 종속성의 스냅샷을 저장합니다. 여기서 모든 이슈를 표시하는 디펜던시 트리를 확인할 수 있고 기존 앱 버전에서 발견된 새 이슈에 대한 알림을 받을 수 있습니다.

## 전제 조건 <a href="#prerequisites" id="prerequisites"></a>

1. Snyk 계정을 만들고 계정 설정에서 Snyk API 토큰을 검색합니다.
2. 관련 보고서를 CircleCI로 가져옵니다.
3. `Settings -> Security -> Orb security settings`로 이동하여 타사 Obs에 대한 옵트인을 허용하는지 확인합니다.
4. 구성(`config.yml`) 파일이 버전 2.1을 따르는지 확인합니다.
5. 필요한 변수를 CircleCI에 추가합니다(Snyk API 토큰을 `API_TOKEN`으로 포함).

## CircleCI 레지스트리에서 Snyk Orb 세부 정보 가져오기 <a href="#getting-snyk-orb-details-from-the-circleci-registry" id="getting-snyk-orb-details-from-the-circleci-registry"></a>

[Orbs registry](https://circleci.com/orbs/registry/)에서 CircleCI는 다음 이미지와 유사하게 사용자 정의된 사용 가능한 Orb 목록을 직접 표시합니다.

![](https://3099555661-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-MdwVZ6HOZriajCf5nXH%2Fuploads%2Fgit-blob-0772d8d5078d6ffe15a2a0ced44c47929b665706%2Fuuid-10d3ba7f-799b-45a9-5c8e-b2abe9aab955-en.png?alt=media\&token=056399ea-f3b2-417c-b7c8-7f4f32a54f39)

이 목록에서 관련 #Snyk라인을 찾아 클릭하여 예제, 파라미터 및 values가 포함된 Snyk Orb 정보를 확인합니다.

![](https://3099555661-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-MdwVZ6HOZriajCf5nXH%2Fuploads%2Fgit-blob-fc231ba2641aace6ee14f4f7db8ae9b0ca89ffba%2Fuuid-ce212e67-b7ac-3cf7-4772-c84f6897aed9-en.png?alt=media\&token=21308823-93a6-460e-8083-0456db59e1b2)
