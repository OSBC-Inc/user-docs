# 통합

## IDE 통합

### JetBrains IDE 플러그인

자세한 내용은 [JetBrains IDE Plugins](../../../features/integrations/ide-tools/jetbrains-plugins.md)를 참조하십시오.

### VS Code IDE 플러그인

자세한 내용은 [Visual Studio Code extension for Snyk Code](../../../features/integrations/ide-tools/visual-studio-code-extension-for-snyk-code.md)를 참조하십시오.

## SCM 통합

### 저장소 모니터링

이 통합을 통해 다음을 수행할 수 있습니다:

* 기존 네이티브 Import 흐름 및 툴을 사용하여 코드 프로젝트 관리
* 소스코드에서 발견된 보안 issues 보기 및 우선 순위 지정
* 프로젝트 재테스트를 실행 및 프로젝트의 히스토리 스냅샷 보기

#### 지원되는 SCM

Snyk Code는 [GitHub](https://docs.snyk.io/integrations/git-repository-scm-integrations/github-integration), [Bitbucket](https://docs.snyk.io/integrations/git-repository-scm-integrations/bitbucket-cloud-integration) , [Azure](https://docs.snyk.io/integrations/git-repository-scm-integrations/azure-repos-integration), [GitLab](https://docs.snyk.io/integrations/git-repository-scm-integrations/gitlab-integration)과 통합됩니다.

#### 지원되는 언어

Snyk Code는 다양한 언어를 지원합니다. 전체 목록은 [언어 및 프레임워크](../snyk-code-language-and-framework-support.md)를 참조하십시오.

### PR 확인

준비 중입니다! 계속 지켜봐 주십시오.

## CI 통합

### Snyk CLI를 사용하여 CI/CD의 테스트 코드

Snyk Code용 [CLI](../../../features/snyk-cli/)(Snyk Command Line Interface)는 로컬 컴퓨터 또는 CI/CD 프로세스에서 코드의 보안 결함을 찾고 수정하는 데 도움이 됩니다.

## API 및 확장성

### 공개 API

코드 프로젝트 및 issues는 [v3 APIs](https://apidocs.snyk.io/?version=2021-11-03%7Eexperimental#overview)에서 쿼리할 수 있습니다.

## 기타 통합

### Jira 통합

Snyk Code를 Jira 인스턴스와 연결하면 개발자가 issue 데이터를 Jira issues로 쉽게 내보낼 수 있습니다.
