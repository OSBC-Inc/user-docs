# 조직의 최대 프로젝트 수

Snyk과 함께 사용하는 계획 유형에 따라 단일 조직에서 가질 수 있는 프로젝트 수에 제한이 있습니다.

| Plan                   | Number of Projects |
| ---------------------- | ------------------ |
| Free                   | 10,000             |
| Team                   | 25,000             |
| Business               | 25,000             |
| Enterprise             | 25,000             |
| Pro (legacy plan)      | 25,000             |
| Standard (legacy plan) | 25,000             |

### 프로젝트 수 한도에 도달했는지 어떻게 알 수 있습니까?

한도에 도달하면 Snyk은 더 많은 프로젝트를 조직에 가져오는 것을 중지하고 오류 메시지가 나타납니다.

Snyk UI:

![](<../../.gitbook/assets/image (14) (1).png>)

Snyk CLI:

> This organization has 10,000 of the maximum 10,000 projects. You will not be able to import more projects: http://docs.snyk.io/getting-started/introduction-to-snyk-projects/maximum-number-of-projects-in-an-organization

최대 프로젝트 수에 도달하면 CLI가 조직의 새 프로젝트 처리를 중지합니다. 이렇게 하면 부분 가져오기가 남을 수 있습니다. 공간을 비우고 나면 조직에서 더이상 필요로하는 프로젝트를 제거하여 명령을 반복할 수 있으며 나머지 프로젝트는 Snyk으로 가져옵니다.

Snyk API:

```
    "data":{
        "code":400,
        "message":"This organization has 25000 of the maximum 25000 projects. You will not be able to import more projects: https://docs.snyk.io/getting-started/introduction-to-snyk-projects/maximum-number-of-projects-in-an-organsation",
        "errorRef":"5bc3fb50-cbcd-4c15-81f6-b183fc95d10f"
    },
```

이 제한은 Snyk 경험을 보호하기 위한 것입니다. 만들 수 있는 조직의 수에는 제한이 없습니다. 이러한 제한에 가까워 지면 더 많은 조직을 만들고 여러 조직에서 프로젝트를 분할이 가능합니다.
