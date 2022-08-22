# GitHub - 진행순서 및 기술

## 진행순서 <a href="#flow" id="flow"></a>

1. SCM에서 자격 증명이 액세스할 수 있는 `one`/`some`/`all` org를 가져오고 org 목록을 만듭니다.
2. 가져온/제공된 org 아래에 있는 `one`/`all` 리포지토리를 가져옵니다.
3. 가져온/제공된 리포지토리에 대한 커밋을 가져오고 기여자 목록을 만듭니다.
4. 기여자들의 리포지토리에 대한 커밋의 수를 셉니다.
5. 제외 파일에 지정된 기여자를 제거합니다 (`exclusionFilePath` flag가 설정되고 텍스트 파일에 대해 유효한 경로가 제공된 경우).
6. 결과를 출력합니다.

## 사용된 GitHub API endpoints <a href="#azure-api-endpoints-used" id="azure-api-endpoints-used"></a>

* GitHub에서 org를 가져오려면 다음과 같이 하십시오:\
  `/user/orgs`
* 가져온/제공된 Org 목록과 상관관계가 있는 리포지토리 목록을 가져오려면 다음과 같이 하십시오: `/orgs/{Org}/repos`
* 가져온/제공된 리포지토리 목록에 대한 커밋을 가져오려면 다음과 같이 하십시오:\
  `repos/{Org}/{Repo}/commits?since={threeMonthsDate}`
