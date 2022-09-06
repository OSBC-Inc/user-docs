# Snyk의 pull 요청 확인

기본적으로 Snyk는 모니터링되는 리포지토리에 제출된 모든 풀 요청을 스캔하여 리포지토리의 매니페스트 파일 수에 관계없이 단일 보안 검사와 단일 라이선스 검사로 그룹화된 결과와 권장 사항을 표시합니다.

{% hint style="info" %}
관리자와 계정 소유자는 조직 및 프로젝트 수준에서 앱의 Snyk PR 테스트 설정을 관리하여 기능이 켜져 있는지(기본적으로 활성화됨) 어떤 조건에서 Snyk가 PR 검사에 실패해야 하는지 구성합니다..
{% endhint %}

{% hint style="warning" %}
현재 Snyk의 pull 요청 검사는 **Dockerfile**과 호환되지 않습니다.
{% endhint %}

## 수표 세부정보 보기

풀 리퀘스트의 라인 중 하나에 대한 테스트가 실패하면 체크 자체가 풀 리퀘스트에서 실패한 것으로 나타납니다. 모든 테스트가 통과하면 확인 자체가 pull 요청에서 성공한 것으로 나타납니다:

![](../../../.gitbook/assets/uuid-08a4b511-c3a4-49ed-1bd2-e234a51c126c-en.jpeg)

모든 매니페스트 파일에 대한 검사 결과를 보려면 인터페이스에서 직접 테스트의 전체 목록과 파일당 결과에 대한 **세부 정보** 링크를 클릭하십시오.

![](../../../.gitbook/assets/uuid-c65f2c6c-d6ad-0fa5-5a0e-6ca0a8f8eeaa-en.jpeg)

이 보기에서 다음과 같은 추가 정보를 보려면 링크를 클릭하십시오.:

* Click the repository link (1) to go back to the Git repository
* Click the Organization link (2) to view all projects in this Snyk organization
* Click the manifest file link (3) to view the Project details page with full details for all vulnerabilities affecting this project
* Click the View test page link (4) to view full details regarding this pull request and the issues preventing the check from passing

![](../../../.gitbook/assets/uuid-617d6ed9-3571-1913-ca32-f30d2f0b3138-en.jpg)

When Snyk tests your pull requests, the following are the possible statuses that can be displayed from this page, in the Results field:

* **Success** - no issues are identified and all checks pass
* **Processing** - this status appears until the Snyk test ends
* **Failure** - when issues are identified that must be fixed in order for the check to pass
* **Error** - an error occurs when your manifest file is out of sync, Snyk couldn't read the manifest file, or Snyk couldn't find the manifest file
* **Canceled** - Snyk test can't run because you've reached your monthly test limit
