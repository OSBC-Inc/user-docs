# Bitbucket Server - 진행순서 및 기술

## 진행순서 <a href="#flow" id="flow"></a>

1. Snyk에서 모니터링되는 프로젝트를 가져옵니다 (`skipSnykMonitoredRepos` flag가 **설정되어 있지 않고** `SNYK_TOKEN` 을 내보낸 경우).
2. SCM에서 자격 증명이 액세스할 수 있는 프로젝트 중 `one`/`some`/`all` 을 가져오고 프로젝트 목록을 생성합니다.
3. 가져온/제공된 프로젝트 아래에 있는 `one`/`all` 리포지토리를 가져옵니다.
4. Snyk에서 모니터링하지 않는 리포지토리를 제거하고 (`skipSnykMonitoredRepos` flag가 **설정되어 있지 않고** `SNYK_TOKEN` 을 내보낸 경우) 리포지토리 목록을 생성합니다.
5. 모니터링되지 않은 리포지토리에 대한 import file을 생성하여 리포지토리를 Snyk 계정으로 쉽게 가져올 수 있습니다(`importConfDir` flag가 설정된 경우).
6. 가져온/제공된 리포지토리에 대한 커밋을 가져오고 기여자 목록을 만듭니다.
7. 기여자들의 리포지토리에 대한 커밋의 수를 셉니다.
8. 제외 파일에 지정된 기여자를 제거합니다 (`exclusionFilePath` flag가 설정되고 텍스트 파일에 대해 유효한 경로가 제공된 경우).
9. 결과를 출력합니다.

## 사용된 Bitbucket Server API endpoints <a href="#bitbucket-cloud-api-endpoints-used" id="bitbucket-cloud-api-endpoints-used"></a>

* 작업영역이 **제공되지 않은 경우** BB Cloud에서 리포지토리를 가져오려면:\
  &#x20;`/rest/api/1.0/repos`
* 작업 공간이 **제공된 경우** BB Cloud에서 리포지토를 가져오려면: `/rest/api/1.0/projects/{Project}/repos`
* 가져온/제공된 리포지토리 목록에 대한 커밋을 가져오려면: `/rest/api/1.0/projects/{Project}/repos/{Repo}/commits`
