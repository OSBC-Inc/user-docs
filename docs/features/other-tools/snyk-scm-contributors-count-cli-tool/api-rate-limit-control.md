# API 속도 제한 제어

## Azure DevOps

Azure DevOps에는 이 [가이드](https://docs.microsoft.com/en-us/azure/devops/integrate/concepts/rate-limits?view=azure-devops)에 설명된 "TSTU" 라는 고유한 방법으로 API 호출 속도를 제한하고 있습니다.

`snyk-scm-contributors-count` 도는 속도 제한을 처리하기 위해 초당 최대 2회의 호출이라는 엄격한 제한을 적용합니다.

## Bitbucket Cloud

Bitbucket Cloud에서 API 속도 제한은 이 [가이드](https://support.atlassian.com/bitbucket-cloud/docs/api-request-limits/)에 설명된 대로 인증된 사용자에 대해 시간당 1,000회 호출입니다.

`snyk-scm-contributors-count` 도구는 속도 제한을 처리하기 위해 시간당 최대 1,000회 호출이라는 엄격한 제한을 적용하고 429회 응답("너무 많은 호출")을 처리하기 위한 추가 규제 메커니즘을 적용합니다.

## Bitbucket Server

Bitbucket Server에서 시스템 관리자는 이 [가이드](https://confluence.atlassian.com/bitbucketserver/improving-instance-stability-with-rate-limiting-976171954.html)에 설명된 대로 API 속도 제한을 완전히 제어할 수 있습니다.

`snyk-scm-contributors-count` 도구는 시간당 최대 1000회 호출에 대한 적당한 제한과 429회의 응답("너무 많은 호출")을 처리하기 위한 추가 규제 메커니즘을 적용합니다.

## GitHub

GitHub에서 API 속도 제한은 이 [가이드](https://docs.github.com/en/developers/apps/building-github-apps/rate-limits-for-github-apps)에 설명된 대로 인증된 사용자에 대해 시간당 5,000회 호출입니다.

`snyk-scm-contributors-count` 도구는 속도 제한을 처리하기 위해 시간당 최대 4,500회 호출이라는 엄격한 제한을 적용하고 429회의 응답("너무 많은 호출")을 처리하기 위한 추가 규제 메커니즘을 적용합니다.

## GitHub Enterprise

Github Enterprise에서 API 속도 제한은 이 [가이드](https://docs.github.com/en/developers/apps/building-github-apps/rate-limits-for-github-apps)에 설명된 대로 인증된 사용자에 대해 시간당 15,000회 호출입니다.

snyk-scm-contributors-count 도구는 속도 제한을 처리하기 위해 시간당 10,800회 호출에 해당하는 초당 최대 3회 호출이라는 엄격한 제한을 적용하고 429회의 응답("너무 많은 호출")을 처리하기 위한 추가 규제 메커니즘을 적용합니다.

## GitLab  GitLab Server

GitLab에서 API 속도 제한은 이 [가이드](https://docs.gitlab.com/ee/user/gitlab\_com/index.html#gitlabcom-specific-rate-limits)와 GitLab Server에 대한 이 [가이드](https://docs.gitlab.com/ee/user/admin\_area/settings/rate\_limits\_on\_raw\_endpoints.html)에 설명된 대로 인증된 사용자에 대한 분당 300회 호출입니다.

`snyk-scm-contributors-count` 도구는 속도 제한을 처리하기 위해 분당 최대 120회 호출이라는 엄격한 제한을 적용하고 429회의 응답("너무 많은 호출")을 처리하기 위한 추가 규제 메커니즘을 적용합니다.

{% hint style="info" %}
GitLab Server에서 API 속도 제어는 [가이드](https://docs.gitlab.com/ee/user/admin\_area/settings/rate\_limits\_on\_raw\_endpoints.html)에 설명된 대로 관리자가 구성할 수 있습니다.
{% endhint %}
