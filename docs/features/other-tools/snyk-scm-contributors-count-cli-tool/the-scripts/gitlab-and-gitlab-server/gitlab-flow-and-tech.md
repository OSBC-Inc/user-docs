# GitLab - 진행순서 및 기술

## 진행순서 <a href="#flow" id="flow"></a>

1. GitLab 또는 GitLab Server mode를 설정합니다(url flag를 통해 호스트가 제공되었는지 여부).
2. SCM에서 자격 증명이 액세스할 수 있는 그룹 중 `one`/`some`/`all` 그룹을 가져오고 그룹 목록을 만듭니다.
3. 가져온/제공된 그룹 아래의 프로젝트 중 `one`/`all` 을 가져옵니다.
4. 모니터링되지 않은 리포지토리에 대한 import file을 생성하여 Snyk 계정으로 리포지토리를 쉽게 가져오는 데 사용할 수 있습니다(`importConfDir` flag가 설정된 경우).
5. 가져오거나 제공한 프로젝트에 대한 커밋을 가져오고 기여자 목록을 만듭니다.
6. 기여자에 의한 프로젝트의 커밋의 수를 셉니다.
7. 제외 파일에 지정된 기여자를 제거합니다 (`exclusionFilePath` flag가 설정되고 텍스트 파일에 대한 유효한 경로가 제공된 경우).
8. 결과를 출력합니.

## 사용된 GitLab API endpoints <a href="#bitbucket-cloud-api-endpoints-used" id="bitbucket-cloud-api-endpoints-used"></a>

* To get the groups paths from GitLab if a group/s names were provided: `api/v4/groups?all_available=true&search={groupName}`
* To get the projects from GitLab if a host url was **not** provided: `/api/v4/projects?membership=true`
* To get the projects from GitLab Server if a host url **was** provided: `/api/v4/projects`
* To get the commits for the fetched/provided project/s list: `/api/v4/projects/{ProjectPath}/repository/commits?since=${threeMonthsDate}`
