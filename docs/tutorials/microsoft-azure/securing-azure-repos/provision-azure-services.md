# Azure 서비스 프로비저닝

## 배경

이 연습의 목적은 Snyk이 [소스 제어 시스템](https://docs.microsoft.com/en-us/azure/devops/user-guide/source-control?view=azure-devops)의 맥락에서 Workload를 보호하는 방법을 보여주는 것입니다. 학습 환경에서 사용하기 위한 기본 패턴을 제공합니다. Azure DevOps에 대해 자세히 알아보고 자세히 알아보려면 Microsoft의 [시작 설명서](https://docs.microsoft.com/en-us/azure/devops/get-started/?view=azure-devops)를 참조하는 것이 좋습니다.

## Azure DevOps Project 생성

우리는 저장소를 포함할 프로젝트를 사용하여 개발 작업을 구성할 것입니다. 다음 단계에서는 [`az devops project create`](https://docs.microsoft.com/en-us/cli/azure/ext/azure-devops/devops/project?view=azure-cli-latest#ext-azure-devops-az-devops-project-create) 명령을 호출하여 팀 프로젝트를 만듭니다.

먼저 다음 명령을 실행하여 프로젝트를 생성해 보겠습니다:

```bash
az devops project create --name MySnykProject --org https://dev.azure.com/myOrganizationName --source-control git --visibility private
```

{% hint style="info" %}
`source control`을 `git`으로 설정하고 저장소를 `private`으로 설정하기 위해 몇 가지 추가 매개 변수를 전달하고 있습니다.
{% endhint %}

성공적으로 완료되면 다음과 유사한 출력이 표시됩니다:

```javascript
{
  "abbreviation": null,
  "capabilities": {
    "processTemplate": {
      "templateName": "Basic",
      "templateTypeId": "<guid>"
    },
    "versioncontrol": {
      "gitEnabled": "True",
      "sourceControlType": "Git",
      "tfvcEnabled": "False"
    }
  },
  "defaultTeam": {
    "id": "<guid>",
    "name": "MySnykProject Team",
    "url": "https://dev.azure.com/myOrganizationName/_apis/projects/<guid>/teams/<guid>"
  },
  "defaultTeamImageUrl": null,
  "description": null,
  "id": "<guid>",
  "name": "MySnykProject",
  "revision": 21,
  "state": "wellFormed",
  "url": "https://dev.azure.com/myOrganizationName/_apis/projects/<guid>",
  "visibility": "private"
}
```

또는 위의 CLI 명령에 `--open` 매개변수를 전달하여 다음 사진과 유사한 기본 웹 브라우저에서 프로젝트를 열 수 있습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/azure\_devops\_02.png)
