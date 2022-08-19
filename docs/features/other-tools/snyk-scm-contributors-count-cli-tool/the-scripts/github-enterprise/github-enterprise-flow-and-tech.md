# GitHub Enterprise - 진행순서 및 기술

## 진행순서 <a href="#flow" id="flow"></a>

1. SCM에서 자격 증명이 액세스할 수 있는 `one`/`some`/`all` org(`fetchAllOrgs` flag에 따라)를 가져오고 orgs 목록을 만듭니다.
2. 가져온/제공된 org 아래에 있는 `one`/`all` 리포지토리를 가져옵니다.
3. 가져온/제공된 리포지토리에 대한 커밋을 가져오고 기여자 목록을 만듭니다.
4. 기여자들의 리포지토리에 대한 커밋의 수를 셉니다.
5. 제외 파일에 지정된 기여자를 제거합니다 (`exclusionFilePath` flag가 설정되고 텍스트 파일에 대해 유효한 경로가 제공된 경우).
6. 결과를 출력합니다.

## 사용된 GitHub Enterprise API endpoints <a href="#azure-api-endpoints-used" id="azure-api-endpoints-used"></a>

* GitHub Enterprise에서 org를 가져오려면: `api/v3/organizations` (`fetchAllOrgs` flag가 **설정된** 경우) 또는`api/v3/user/orgs` (`fetchAllOrgs` flag가 **설정되지 않은** 경우)
* 가져온/제공된 org 목록과 상관관계가 있는 리포지토리 목록을 가져오려면:`api/v3/orgs/{Org}/repos`
* 가져온/제공된 리포지토리 목록의 커밋을 가져오려면: `api/v3/repos/{Org}/{Repo}/commits`
