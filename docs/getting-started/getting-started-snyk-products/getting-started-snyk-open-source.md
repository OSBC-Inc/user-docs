# Snyk Open Source 사용하기

Snyk Open Source를 이용하여 코드의 취약점을 검사하고 수정할 수 있습니다.

{% hint style="info" %}
이 프로세스는 Snyk.io UI 및 소스 코드 관리 시스템 사용에 대해 설명합니다. [IDE tool](https://docs.snyk.io/integrations/ide-tools) 또 [CI/CD integration](https://docs.snyk.io/integrations/ci-cd-integrations)을 사용할 수 있습니다. 자세한 내용은 [Integrations](https://docs.snyk.io/integrations)을 참조하세요.
{% endhint %}

### **CLI tool** 사용하기

Snyk CLI tool을 이용하여 Snyk을 시작할 수 있습니다.

```
npm install -g snyk
```

자세한 내용은 [Getting started with the CLI](https://docs.snyk.io/snyk-cli/guides-for-our-cli/getting-started-with-the-cli)를 참조하세요.

#### 전제 조건

Ensure you have:

1. [지원되는 언어 및 패키지 관리자](../../products/snyk-open-source/language-and-package-manager-support/)(예: Java)와 함께 지원되는 [소스 코드 관리 시스템](../../features/integrations/git-repository-scm-integrations/)(예: Github)에서 오픈 소스 패키지를 사용하는 프로젝트.
2. Snyk 계정 ([https://snyk.io/](https://snyk.io)로 이동하여 가입 - 자세한 내용은 [Create a Snyk account](https://docs.snyk.io/getting-started/getting-started-snyk-products) 참).

### 1단계: 소스 제어 통합 추가

{% hint style="info" %}
이미 통합을 설정한 경우 3단계로 이동할 수 있습니다.
{% endhint %}

Snyk에서 프로젝트를 작업할 수 있도록 소스 코드 통합을 진행합니다.

1. Snyk.io에 로그인합니다.
2. **Integrations > Source control**를 선택 합니다.
3. Snyk과 통합할 소스 제어 시스템(예: Github)을 클릭합니다.
4. Snyk 액세스 권한을 부여하기 위해 계정 자격 증명을 입력하거나 Github계정으로 인증을 진행합니다.

자세한 내용은 [DevOps integrations & languages](https://docs.snyk.io/introducing-snyk/introduction-to-snyk/integrations-and-languages)를 참조하세요.

### 2단계: 프로젝트 추가

Add projects to test with Snyk, by choosing repositories for Snyk to test and monitor.

1. Select **Projects** from snyk.io.
2. Select the tool to add the project from (for example GitHub).
3. In **Personal and Organization repositories**, select the repositories to use.
4. Click **Add selected repositories** to import the selected repositories into your projects. This also:
   1. Sets Snyk to run a regular check (daily by default) for vulnerabilities.
   2. Creates a Webhook, so when you change code, Snyk tests your pull / merge requests, to check that new dependencies do not introduce more vulnerabilities.
5. A progress bar appears: click **View log** to see log results.
6. Project import completes.

{% hint style="info" %}
If you encounter any errors during import, see the [Importing projects](https://support.snyk.io/hc/en-us/sections/360000923478-Importing-projects) information.
{% endhint %}

### Stage 3: View vulnerabilities

You can now view vulnerability results for imported projects. The **Projects** tab appears by default after import, showing vulnerability information for project you've imported.

1. Click on an imported project to see vulnerability information for that project, including the number of issues found, grouped by severity level (see screenshot below)
2. Click on an entry to open the issues view for that entry, including the module, where it was introduced, and how to fix it, plus more details about the vulnerability itself:

![](<../../.gitbook/assets/view\_vulns\_\_overview (1).png>)

![](<../../.gitbook/assets/detailed-vuln-information (3) (4) (4) (4) (6) (7) (5) (1) (4).png>)

See [View project information](https://docs.snyk.io/getting-started/introduction-to-snyk-projects/view-project-information) for more details.

### Stage 4: Fix vulnerabilities

For JavaScript, Ruby and Java projects, Snyk can fix your vulnerabilities via fix pull/merge requests:

Navigate to the issues view for a project:

![Screenshot\_2021-04-09\_at\_17.35.25.png](<../../.gitbook/assets/screenshot\_2021-04-09\_at\_17.35.25 (1).png>)

To fix vulnerabilities:

1. Click **Fix this vulnerability** to upgrade (or patch) to fix an individual issue, or click **Fix these vulnerabilities** to to fix multiple issues at once.
2. The **Open a Fix PR** screen opens and indicates the vulnerabilities you selected:
3. Check any additional issues you want to fix, or uncheck items to remove them from the fix. 4. Scroll down to the bottom of the screen and click **Open a Fix PR**. 5. Snyk now actions this PR, then a results screen appears:
4. Optionally, select the **Files changed** tab to see details of the changes made.

![](<../../.gitbook/assets/screenshot\_2021-04-09\_at\_17.46.22 (1).png>)

{% hint style="info" %}
If no package upgrade is available, you may be able to use Snyk patches to fix vulnerabilities.
{% endhint %}

See [Fixing vulnerabilities](https://docs.snyk.io/snyk-open-source/open-source-basics/fixing-vulnerabilities) for more details.

## For more information

See [Snyk Open Source](https://docs.snyk.io/snyk-open-source).
