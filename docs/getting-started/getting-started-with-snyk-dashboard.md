# Snyk 대시보드 시작하기

**Snyk 대시보드의 Pending tasks**

대시보드의 **Pending tasks** 섹션에는 Snyk 조직의 프로젝트와 관련하여 고려해야 할 권장되는 미해결 작업이 표시됩니다.

![](../.gitbook/assets/pending-tasks.png)

이 정보에는 다음과 같은 내용이 포함됩니다.

* 가장 취약한 일부 프로젝트의 취약점을 수정하기 위해 제기될 수 있는 PR(Pull Request)
* (Snyk에 의해 또는 Snyk을 통해) ~~_이미 제기되어 검토를 기다리고 있는 PR_~~

현재 Snyk은 Github의 가장 취약한 프로젝트에 대해서만 PR을 추적하고 플래그를 지정합니다. ~~_다른 SCM을 사용하는 경우__ __**Pending tasks**__에는 이미 제기된 PR이 아니라 제기될 수 있는 PR만 표시됩니다._~~
