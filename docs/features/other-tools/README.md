# 더 많은 Snyk 도구

## 소개

Snyk은 주요 Snyk 제품 라인에서 해결할 수 없는 특정 문제를 해결하는 데 도움이 되는 도구를 제공합니다.

{% hint style="info" %}
이러한 도구를 사용하려면 채워진 프로젝트가 있는 기존 Snyk 계정이 필요합니다.
{% endhint %}

## 사용 가능한 도구

* [snyk-api-import](https://github.com/snyk-tech-services/snyk-api-import): 강력하고 빠른 방식으로 프로젝트를 Snyk으로 대량 가져옵니다.
* [jira-tickets-for-new-vulns](https://github.com/snyk-tech-services/jira-tickets-for-new-vulns): Snyk 모니터링 프로젝트를 동기화하고 문제에 대한 JIRA 티켓을 auto-open 합니다.
* [snyk-delta](https://github.com/snyk-tech-services/snyk-delta): 두 Snyk snapshot 간의 delta를 가져옵니다.
* [snyk-disallow](https://github.com/snyk-tech-services/snyk-disallow): CI 또는 유사한 시스템에 대한 read|test-only token을 얻기위해 Snyk Group의viewer token을 가져옵니다.
* [snyk-prevent-gh-commit-status](https://github.com/snyk-tech-services/snyk-prevent-gh-commit-status): CI에서 실행된 snyk-delta의 결과 PR의 POST 커밋 상태입니다.
* [snyk-scm-contributors-count](https://github.com/snyk-tech-services/snyk-scm-contributors-count): 지난 90일 동안 커밋이 있는 SCM 저장소의 기여자를 계산합니다. [문서](snyk-scm-contributors-count-cli-tool/)를 참조하십시오.
* [snyk-cr-monitor](https://github.com/snyk-tech-services/snyk-cr-monitor): 테스트할 Docker 저장소를 수집한 다음 결과를 반복하여 여러 작업을 동시에 실행합니다.
* [backstage-plugin-snyk](https://github.com/snyk-tech-services/backstage-plugin-snyk): Snyk의 보안 세부 정보를 표시하는 플러그인입니다.
* [snyk-api-ts-client](https://github.com/snyk-tech-services/snyk-api-ts-client): Snyk API Typescript 클라이언트 입니다.
* [snyk-filter](https://github.com/snyk-tech-services/snyk-filter): Snyk CLI에서 JSON 출력을 가져오고 결과에 사용자 지정 필터링을 적용합니다.
* [snyk-transitive-ignore](https://github.com/snyk-tech-services/snyk-transitive-ignore): 제공된 패키지 목록을 기반으로 Snyk ignore 정책을 동적으로 생성합니다.
* [snyk-user-sync-tool](https://github.com/snyk-tech-services/snyk-user-sync-tool): 사용자 멤버십을 추가, 제거 및 동기화합니다.
* [snyk-licenses-texts](https://github.com/snyk-tech-services/snyk-licenses-texts): 사용된 라이선스, 저작권 및 종속성 데이터를 조직 수준에 따라 제공합니다.
* [snyk-request-manager](https://github.com/snyk-tech-services/snyk-request-manager): Rate controlled and retry enabled request manager to interact with Snyk APIs.
* [snyk2spdx](https://github.com/snyk-tech-services/snyk2spdx): Convert the Snyk CLI output to SPDX format.
* [snyk-repo-issue-tracker](https://github.com/snyk-tech-services/snyk-repo-issue-tracker): A python script / module that allows for generating a changeset of issues between runs against the Snyk project issues API.
*   [snyk-repo-diff:](https://github.com/snyk-tech-services/snyk-repo-diff) Helps answer which repositories aren't monitored by Snyk.

    This works by retrieving a list of all projects in a given Snyk Group (all projects in all orgs belonging to the same Snyk Group) and associating them with a list of repositories found in a given GitHub Organization (see below section on GitLab support),
* [snyk-issues-to-csv](https://github.com/snyk-tech-services/snyk-issues-to-csv): A python script that uses the PySnyk module along with the Pandas modules to collect all issues from the report API and combine them into a single CSV for an entire group.
* [snyk-bulk](https://github.com/snyk-tech-services/snyk-bulk): Recursively scan source repositories for open source vulnerabilities with the Snyk CLI, outside of a build environment.
* [snyk-bulk-action-scripts](https://github.com/snyk-tech-services/snyk-bulk-action-scripts): A collection of scripts to edit integration settings for every organization in a group in Snyk.
* [snyk-deps-to-csv](https://github.com/snyk-tech-services/snyk-deps-to-csv): Collects all dependencies from all orgs in a group and outputs to a CSV file.

## Tool ideas

Do you have an idea for a tool? If so, check out [Snyk Apps](../integrations/snyk-apps/), which provides an opportunity to mold your Snyk experience to suit your specific needs. You can also contact [Snyk Support with questions](https://support.snyk.io/hc/en-us/).
