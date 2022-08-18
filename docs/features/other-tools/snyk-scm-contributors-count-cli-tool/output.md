---
description: SCM-Contributors-Count tool을 실행한 결과
---

# 출력

## Summary

Summary 섹션은 다음과 같이 출력의 시작과 끝에 모두 표시됩니다:

```
#### Summary
Private Repos Contributors Count:: 1
Public Repos Contributors Count: 1
Total Unique Contributors Count for Private and Public repositories: 1
Private Repository Count: 1
Public Repository Count: 1
Total Repository Count: 2
Exclusion Count: 1
```

* `Private Repos Contributors Count` - Private 리포지토리를 찾거나 제공한 고유 기여자의 수 입니다.
* `Public Repos Contributors Count` - Public 리포지토리를 찾거나 제공한 고유 기여자의 수 입니다.
* `Total Unique Contributors Count for Private and Public repositories`- 조사된 모든 리포지토리의 총 고유 기여자 수입니다.
* `Private Repository Count` - 검색된 Private 리포지토리의 수 입니다.
* `Public Repository Count` - 검색된 Public 리포지토리의 수 입니다.
* `Total Repository Count` - 검색된 총 리포지토리의 수 입니다. (public 및 private).
* `Exclusion Count` - 제공된 제외 파일에 따라 계산되지 않은 기여자 수입니다.

## 세부사항

```
### Details:
## Repository List

# Private Repositories:
someOrganization/someRepository(Private)

# Public Repositories:
anotherOrganization/anotherRepository(Public)
```

* `Private Repositories` - 검색된 Private 리포지토리 목록입니다.
* `Public Repositories` - 검색된 Public 리포지토리 목록입니다.

{% hint style="info" %}
각 리포지토리 이름 옆에 표시 여부, (Private) 또는 (Public)가 표시됩니다.
{% endhint %}

## Contributors details

```
## Contributors details
[
    [
        "someUser",
        {
            "email": "someUser@company.io",
            "contributionsCount": 15,
            "reposContributedTo": [
                "someOrganization/someRepository(Private)"
                "anotherOrganization/anotherRepository(Public)"
            ]
        }
    ],
    [
        "anotheruser",
        {
            "email": "anotherUser@company.io",
            "contributionsCount": 11,
            "reposContributedTo": [
                "someOrganization/someRepository(Private)"
            ]
        }
    ],
    [
        "anotheruser(duplicate)",
        {
            "email": "anotherUser@otherCompany.com",
            "contributionsCount": 11,
            "reposContributedTo": [
                "someOrganization/someRepository(Private)"
            ]
        }
    ]
]
```

* `email` - The email of the contributor
* `contributionsCount` - The number of the times this contributor has contributed to the repo/s.
* `repoContributedTo` - A list of the repo/repos to which this contributor has contributed.
* `(duplicate)` - Indicator that the same user has been detected from different email addresses; note that they will be counted as **different committers**.

{% hint style="info" %}
As the output can be long, Snyk recommends sending the output to a file for better review and parsing options.
{% endhint %}
