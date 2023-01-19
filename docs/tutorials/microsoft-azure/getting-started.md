# 시작하기

## 로컬 환경 구성

우리가 수행할 작업의 대부분은 [Azure CLI(Command-Line Interface)](https://docs.microsoft.com/en-us/cli/azure/?view=azure-cli-latest)를 사용하는 것과 관련됩니다. [Windows](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-windows?view=azure-cli-latest), [macOS](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-macos?view=azure-cli-latest) 및 [Linux](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-yum?view=azure-cli-latest)용 Azure CLI 설치에 대한 자세한 설명서는 [Azure 설명서](https://docs.microsoft.com/en-us/azure/)에서 확인할 수 있습니다. 이 예제는 macOS를 기반으로 합니다. 또한 샘플 코드, 템플릿 및 기타 리소스가 이 Workshop의 저장소에서 제공됩니다. 이 연습 전체에서 해당 콘텐츠를 참조하므로 이 [저장소](https://github.com/snyk-partners/snyk-azure-resources)를 [`clone`](https://github.com/snyk-partners/snyk-azure-resources.git)하거나 [`fork`](https://github.com/snyk-partners/snyk-azure-resources/fork)하는 것이 좋습니다.

### 홈브류 설치

아직 없는 경우 [Homebrew를 설치](https://docs.brew.sh/Installation.html)한 후 다음 명령을 사용하여 Azure CLI를 설치합니다.

```bash
brew update && brew install azure-cli
```

### Azure CLI로 인증

설치가 완료되면 CLI에서 Azure 계정에 로그인해야 합니다. 다음 명령을 실행합니다:

```bash
az login
```

CLI는 기본 브라우저를 열고 Azure 로그인 페이지를 로드하려고 시도합니다. 브라우저에서 Azure 계정 자격 증명을 제공하고 인증에 성공하면 브라우저 창에 다음과 같은 응답이 표시됩니다:

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/azure\_cli\_login.png)

또한 터미널에 다음과 유사한 출력이 표시되어야 합니다:

```javascript
[
  {
    "cloudName": "AzureCloud",
    "homeTenantId": "<guid>",
    "id": "<guid>",
    "isDefault": true,
    "state": "Enabled",
    "tenantId": "<guid>",
    "user": {
      "name": "developer@microsoft.com",
      "type": "user"
    }
  }
]
```

문제가 발생하면 [macOS에 Azure CLI 설치](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-macos?view=azure-cli-latest) 설명서 페이지에서 추가 지침을 검토하세요.
