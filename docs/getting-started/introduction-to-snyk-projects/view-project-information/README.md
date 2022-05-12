# 프로젝트 정보 보기

## 애플리케이션 취약점 보기

Snyk은 프로젝트의 파일에 대한 애플리케이션 취약점과 라이선스 Issue를 표시합니다. 이러한 취약점을 확인하려면 [projects 탭](https://app.snyk.io/projects)으로 이동한 다음 프로젝트와 연결된 파일을 선택하십시오. 예를 들어 애플리케이션 goof의 package.json파일은 다음과 같습니다.

![](../../../.gitbook/assets/application-vuln.png)

항목을 클릭하면 자세한 정보를 확인할 수 있습니다.

![](../../../.gitbook/assets/project-page.png)

* **Header**: 프로젝트 요약 정보를 확인할 수 있습니다. [프로젝트 정보 보기](./)를 참조하십시오.
* **Issue cards**: 발견된 Issue의 요약된 정보를 표시합니다. [Issue card](../issue-card-information.md)를 참조하십시오.
* **Views**:
  * **Overview**: [프로젝트 issues, fixes, dependencies](../view-project-issues-remediations-and-dependencies.md)를 표시합니다.
  * **History**: 최근 4개의 테스트에 대한 기록 스냅샷을 제공합니다. [프로젝트 기록 보기](../view-project-history.md)를 참조하십시오.
  * **Settings**: [프로젝트 설정](../view-project-settings.md)을 표시합니다.

### 프로젝트 요약 정보 보기

![](../../../.gitbook/assets/proj-summ.png)

요약 정보는 다음 내용을 보여줍니다.

* 파일 및 기록 세부 정보:
  * 모니터링되는 저장소의 이름(링크).
  * 모니터링되는 branch 이름.
  * SCM의 프로젝트 파일에 대한 링크.
  * 프로젝트를 Snyk으로 처음 가져온 시간.
  * 파일의 최신 스냅샷을 SCM에서 가져와 테스트한 시간.
* 사전 정의된 [프로젝트 속성](broken-reference) 및 추가적인 [프로젝트 태그](project-tags.md) 메타데이터.
