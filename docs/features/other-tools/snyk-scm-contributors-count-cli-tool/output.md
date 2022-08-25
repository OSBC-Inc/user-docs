---
description: SCM-Contributors-Count 도구를 실행한 결과
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
* `Exclusion Count` - 제공된 제외 파일에 따라 계산되지 않은 기여자 수 입니다.

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
각 리포지토리 이름 옆에 표시 여부, (Private) 또는 (Public) 이 표시됩니다.
{% endhint %}

## 기여자 세부사항

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

* `email` - 기여자의 이메일 입니다.
* `contributionsCount` - 이 기여자가 리포지토리에 기여한 횟수입니다.
* `repoContributedTo` - 이 기여자가 기여한 리포지토리 목록입니다.
* `(duplicate)` - 동일한 사용자가 다른 전자 메일 주소에서 탐지되었음을 나타냅니다. **서로 다른 커밋**으로 간주됩니다.

{% hint style="info" %}
출력이 길 수 있으므로 더 나은 검토 및 구문 분석 옵션을 위해 출력을 파일로 보낼 것을 권장합니다.
{% endhint %}
