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

With the steps above completed, you are ready to [add the public key to Azure DevOps Services](https://docs.microsoft.com/en-us/azure/devops/repos/git/use-ssh-keys-to-authenticate?view=azure-devops\&tabs=current-page#step-2--add-the-public-key-to-azure-devops-servicestfs).

### Git submodules

The source repository containing the sample code and templates we are providing contains a `submodule` that references a dependent project. When you cloned this repository it contained a `.gitmodules` file that points to the `app/redis` directory. This will appear empty until you run a couple of [`git submodule`](https://git-scm.com/book/en/v2/Git-Tools-Submodules) commands.

From the terminal and the working directory for the cloned project, initialize with the following command:

```bash
git submodule init
```

This should output the following:

```
Submodule 'app/redis' (git@github.com:docker-library/redis.git) registered for path 'app/redis'
```

Next, let's update recursively so we clone into our directory all files:

```bash
git submodule update --recursive
```

This should output the following:

```
Cloning into '/Users/you/git/snyk-azure-resources/app/redis'...
Submodule path 'app/redis': checked out '9a598d433acf8fbf3d1f07223c164b3bd7ead3b3'
```

### Cloning the repo

After identifying which repository in our project we will use, we will invoke the [`az repos show`](https://docs.microsoft.com/en-us/cli/azure/ext/azure-devops/repos?view=azure-cli-latest#ext-azure-devops-az-repos-show) command to provide details of a specific Git repository. From the terminal, let's run the following command:

```bash
az repos show --project mySnykProject --repository mySnykProject --query sshUrl --output tsv
```

In the above command, we will query for the `sshUrl` we will need to clone the repo and outputs this as text. We will then pass that value to the [`git remote`](https://git-scm.com/docs/git-remote) command where we are adding `mySnykProject` as a remote repository:

```bash
git remote add azure $(az repos show --project mySnykProject --repository mySnykProject --query sshUrl --output tsv)
```

We can optionally validate this was successful with the by invoking `git remote` once more but this time passing the `-v` option:

```bash
git remote -v
```

You should see output similar to the following:

```
azure    git@ssh.dev.azure.com:v3/myOrganizationName/MySnykProject/MySnykProject (fetch)
azure    git@ssh.dev.azure.com:v3/myOrganizationName/MySnykProject/MySnykProject (push)
origin    git@github.com:myGitHub/snyk-azure-resources.git (fetch)
origin    git@github.com:myGitHub/snyk-azure-resources.git (push)
```

Now, we are ready to run our first [`git push`](https://git-scm.com/docs/git-push) command to update our remote repository:

```bash
git push azure master
```

{% hint style="info" %}
For our example, we will use `master` branch. There are different strategies here such as trunk-based versus feature-driven. These are beyond the scope of this module so we will continue with a simplified approach.
{% endhint %}

You should see output similar to the following:

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

Alternatively, you can view the files in your repo by visiting the Azure DevOps portal:

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/azure\_devops\_03.png)
