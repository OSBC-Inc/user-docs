# 저장소 작업

### 배경

{% hint style="info" %}
아직 수행하지 않은 경우 다음 단계 중 일부를 완료하는 데 필요하므로 이러한 실습에 대한 저장소를 [`clone`](https://github.com/snyk-partners/snyk-azure-resources.git)하거나 [`fork`](https://github.com/snyk-partners/snyk-azure-resources/fork)하는 것이 좋습니다.
{% endhint %}

이 Section에서는 [`az repos list`](https://docs.microsoft.com/en-us/cli/azure/ext/azure-devops/repos?view=azure-cli-latest) 명령을 사용하여 `git clone` URL을 쿼리합니다. 그런 다음 Azure Repo를 업스트림 리포지토리로 추가하고 코드를 `git push`합니다.

### 프로젝트 생성

터미널에서 다음 명령을 실행합니다:

```bash
az repos list --project mySnykProject
```

그러면 다음과 유사한 JSON이 출력됩니다:

```javascript
[
  {
    "defaultBranch": null,
    "id": "<guid>",
    "isFork": null,
    "name": "MySnykProject",
    "parentRepository": null,
    "project": {
      "abbreviation": null,
      "defaultTeamImageUrl": null,
      "description": null,
      "id": "<guid>",
      "name": "MySnykProject",
      "revision": 21,
      "state": "wellFormed",
      "url": "https://dev.azure.com/myOrganizationName/_apis/projects/<guid>",
      "visibility": "private"
    },
    "remoteUrl": "https://myOrganizationName@dev.azure.com/myOrganizationName/MySnykProject/_git/MySnykProject",
    "size": 0,
    "sshUrl": "git@ssh.dev.azure.com:v3/myOrganizationName/MySnykProject/MySnykProject",
    "url": "https://dev.azure.com/myOrganizationName/<guid>/_apis/git/repositories/<guid>",
    "validRemoteUrls": null,
    "webUrl": "https://dev.azure.com/myOrganizationName/MySnykProject/_git/MySnykProject"
  }
]
```

### 저장소에 연결

SSH를 사용하는 것이 좋습니다. 다음 단계는 이를 설정하는 데 필요한 단계를 안내합니다. HTTPS를 사용하도록 선택할 수 있지만 해당 방법으로 연결하는 단계는 제공하지 않습니다. [개인 액세스 토큰으로 액세스를 인증](https://docs.microsoft.com/en-us/azure/devops/organizations/accounts/use-personal-access-tokens-to-authenticate?view=azure-devops\&tabs=preview-page)하거나 [Git Credential Managers를 사용하여 대안을 위해 Azure Repos에 인증](https://docs.microsoft.com/en-us/azure/devops/repos/git/set-up-credential-managers?view=azure-devops)하는 방법에 대해 자세히 알아볼 수 있습니다.

{% tabs %}
{% tab title="SSH 키 생성" %}
사용하려는 SSH 키가 이미 있는 경우 이 Section을 건너뛸 수 있습니다. 그렇지 않으면 다음 단계를 진행하십시오:

터미널에서 다음 명령을 사용하여 [SSH 키를 생성](https://docs.microsoft.com/en-us/azure/devops/repos/git/use-ssh-keys-to-authenticate?view=azure-devops\&tabs=current-page#step-1-create-your-ssh-keys)합니다:

```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

{% hint style="info" %}
Azure Portal에 인증하는 데 사용되는 이메일 주소를 사용합니다.
{% endhint %}

키를 저장할 파일을 입력하라는 메시지가 표시되면 `/Users/you/.ssh/id_rsa`의 기본 파일 위치를 **수락하지 마십시오**. 대신 `/Users/you/.ssh/id_rsa_azure`와 같은 고유한 키 파일 이름을 제공하십시오. 다음으로 보안 암호를 입력하라는 메시지가 표시됩니다.

```
> Enter passphrase (empty for no passphrase): [Type a passphrase]
> Enter same passphrase again: [Type passphrase again]
```
{% endtab %}

{% tab title="ssh-agent에 SSH 키 추가" %}
ssh-agent를 시작합니다:

```bash
eval "$(ssh-agent -s)"
```

ssh-agent에 SSH 비공개 키를 추가합니다:

```bash
ssh-add -K ~/.ssh/id_rsa_azure
```

macOS의 경우 다음 항목을 사용하여 `~/.ssh/config`를 수정합니다:

```
Host ssh.dev.azure.com 
  Hostname ssh.dev.azure.com 
  AddKeysToAgent yes 
  UseKeychain yes 
  IdentityFile ~/.ssh/id_rsa_azure 
  IdentitiesOnly yes
```

마지막으로 SSH 공개 키를 클립보드에 복사합니다. 다음 단계에서 필요합니다:

```bash
pbcopy < ~/.ssh/id_rsa_azure.pub
```
{% endtab %}
{% endtabs %}

위의 단계를 완료하면 [Azure DevOps Services에 공개 키를 추가](https://docs.microsoft.com/en-us/azure/devops/repos/git/use-ssh-keys-to-authenticate?view=azure-devops\&tabs=current-page#step-2--add-the-public-key-to-azure-devops-servicestfs)할 준비가 된 것입니다.

### Git 하위 모듈

우리가 제공하는 샘플 코드와 템플릿이 포함된 소스 저장소에는 종속 프로젝트를 참조하는 `submodule`이 포함되어 있습니다. 이 저장소를 복제하면 `app/redis` 디렉터리를 가리키는 `.gitmodules` 파일이 포함됩니다. 몇 가지 [`git submodule`](https://git-scm.com/book/en/v2/Git-Tools-Submodules) 명령을 실행할 때까지 비어 있는 것으로 나타납니다.

복제된 프로젝트의 터미널 및 작업 디렉터리에서 다음 명령을 사용하여 초기화합니다:

```bash
git submodule init
```

그러면 다음이 출력됩니다:

```
Submodule 'app/redis' (git@github.com:docker-library/redis.git) registered for path 'app/redis'
```

다음으로 재귀적으로 업데이트하여 모든 파일을 디렉터리에 복제합니다:

```bash
git submodule update --recursive
```

그러면 다음이 출력됩니다:

```
Cloning into '/Users/you/git/snyk-azure-resources/app/redis'...
Submodule path 'app/redis': checked out '9a598d433acf8fbf3d1f07223c164b3bd7ead3b3'
```

### 저장소 복제

프로젝트에서 사용할 저장소를 식별한 후 [`az repos show`](https://docs.microsoft.com/en-us/cli/azure/ext/azure-devops/repos?view=azure-cli-latest#ext-azure-devops-az-repos-show) 명령을 호출하여 특정 Git 저장소의 세부 정보를 제공합니다. 터미널에서 다음 명령을 실행해 보겠습니다:

```bash
az repos show --project mySnykProject --repository mySnykProject --query sshUrl --output tsv
```

위의 명령에서 `sshUrl`을 쿼리하여 저장소를 복제하고 이를 텍스트로 출력해야 합니다. 그런 다음 `mySnykProject`를 원격 저장소로 추가하는 [`git remote`](https://git-scm.com/docs/git-remote) 명령에 해당 값을 전달합니다:

```bash
git remote add azure $(az repos show --project mySnykProject --repository mySnykProject --query sshUrl --output tsv)
```

선택적으로 `git remote`를 한 번 더 호출하여 이번에는 `-v` 옵션을 전달하여 이것이 성공했는지 확인할 수 있습니다.

```bash
git remote -v
```

다음과 유사한 출력이 표시되어야 합니다:

```
azure    git@ssh.dev.azure.com:v3/myOrganizationName/MySnykProject/MySnykProject (fetch)
azure    git@ssh.dev.azure.com:v3/myOrganizationName/MySnykProject/MySnykProject (push)
origin    git@github.com:myGitHub/snyk-azure-resources.git (fetch)
origin    git@github.com:myGitHub/snyk-azure-resources.git (push)
```

이제 첫 번째 [`git push`](https://git-scm.com/docs/git-push) 명령을 실행하여 원격 저장소를 업데이트할 준비가 되었습니다:

```bash
git push azure master
```

{% hint style="info" %}
이 예에서는 `master` Branch를 사용합니다. 여기에는 트렁크 기반 대 기능 중심과 같은 다양한 전략이 있습니다. 이것들은 이 모듈의 범위를 벗어나므로 단순화된 접근 방식으로 계속 진행하겠습니다.
{% endhint %}

다음과 유사한 출력이 표시되어야 합니다:

```
Warning: Permanently added the RSA host key for IP address '192.168.1.100' to the list of known hosts.
Enumerating objects: 65, done.
Counting objects: 100% (65/65), done.
Delta compression using up to 16 threads
Compressing objects: 100% (56/56), done.
Writing objects: 100% (65/65), 1.80 MiB | 92.30 MiB/s, done.
Total 65 (delta 6), reused 65 (delta 6)
remote: Storing packfile... done (178 ms)
remote: Storing index... done (76 ms)
To ssh.dev.azure.com:v3/myOrganizationName/MySnykProject/MySnykProject
 * [new branch]      master -> master
```

또는 Azure DevOps 포털을 방문하여 저장소의 파일을 볼 수 있습니다:

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/azure\_devops\_03.png)
