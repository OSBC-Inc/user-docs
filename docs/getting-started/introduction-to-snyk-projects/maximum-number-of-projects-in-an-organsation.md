# 조직의 최대 프로젝트 수

Snyk과 함께 사용하는 요금제 유형에 따라 하나의 조직에서 가질 수 있는 프로젝트 수에 제한이 있습니다.

| 요금제                    | 프로젝트 수 |
| ---------------------- | ------ |
| Free                   | 10,000 |
| Team                   | 25,000 |
| Business               | 25,000 |
| Enterprise             | 25,000 |
| Pro (legacy plan)      | 25,000 |
| Standard (legacy plan) | 25,000 |

### 프로젝트 수가 한도에 도달했는지 어떻게 알 수 있습니까?

한도에 도달하면 Snyk은 더 많은 프로젝트를 조직에 가져오는 것을 중단합니다.

Snyk UI에 다음 배너가 표시되면 한도에 도달했음을 알 수 있습니다.

![한도를 초과한 프로젝트 수를 알려주는 배너가 프로젝트 페이지 상단에 표시됩니다.](<../../.gitbook/assets/image (14) (1).png>)

CLI에서 `snyk monitor` 명령은 다음 오류를 반환합니다.

> `Maximum number of projects reached for this organization. You cannot import more projects.`

API에서는 다음 오류를 반환합니다.

```
    "data":{
        "code":400,
        "message":"This organization has 25000 of the maximum 25000 projects. You will not be able to import more projects: https://docs.snyk.io/getting-started/introduction-to-snyk-projects/maximum-number-of-projects-in-an-organsation",
        "errorRef":"5bc3fb50-cbcd-4c15-81f6-b183fc95d10f"
    },
```

~~_이 제한은 Snyk 경험을 보호하기 위한 것입니다._ ~~ 만들 수 있는 조직의 수에는 제한이 없습니다. 이러한 제한에 가까워 지면 더 많은 조직을 만들고 여러 조직에서 프로젝트를 분할이 가능합니다.
