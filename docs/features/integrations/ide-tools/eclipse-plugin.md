---
description: Use this documentation to get started with the Eclipse plugin.
---

# Eclipse plugin

Eclipse 워크플로에 **Snyk Security - Code and Open Source Dependencies**를 설치하여 코드베이스에 병합되기 전에 IDE(통합 개발 환경) 내에서 직접 취약점 및 라이선스 문제를 노출합니다.

Eclipse 플러그인을 설치 및 구성한 후 실행할 때마다 Snyk은 프로젝트의 매니페스트 파일을 스캔하고 다음 작업을 수행합니다.

* 실행 가능한 취약점 및 라이선스 issue 세부 정보를 분석하고 제공합니다.
* 패키지당 결과 기록
* Eclipse UI에서 직접 결과 표시

Snyk Eclipse 플러그인을 사용하면 애플리케이션 보안에 위협이 되는 문제를 추적 및 식별할 수 있으며 이러한 문제가 공유 리포지토리에 추가되는 것을 방지할 수 있습니다.

{% hint style="info" %}
Snyk Eclipse 플러그인은 [Eclipse Marketplace](https://marketplace.eclipse.org/content/snyk-security-scanner)에서 설치할 수 있습니다.
{% endhint %}

## 지원되는 언어 및 리포지토리

Snyk은 Eclipse와 Snyk에서 모두 지원하는 모든 언어를 지원합니다. 또한 Snyk 플러그인은 Snyk Broker 및 온프레미스 솔루션으로 구현할 수 있습니다.

## Snyk Eclipse 플러그인 설치

1. 실행 중인 Eclipse 인스턴스 내에서 Marketplace로 이동합니다.
2. Snyk를 검색하고 Install을 클릭합니다.
3. 라이센스 계약에 동의하라는 메시지가 표시되면 Snyk Security 인증서를 추가하여 설치를 완료합니다.
4. Eclipse 인스턴스를 다시 시작하고 **Eclipse Preferences**로 이동하여 이제 **Snyk Security - Code and Open Source Dependencies**가 목록에 나타나는지 확인합니다.

![Snyk 플러그인 및 설치 버튼을 보여주는 Eclipse Marketplace 검색](../../../.gitbook/assets/uuid-01198b42-f020-2cc5-c20f-93817eeb44a4-en.png)

## 구성

Snyk를 사용하려면 환경 변수와 Snyk 토큰을 플러그인에 제공해야 합니다.

### API 토큰

API 토큰을 제공하려면 [account settings](https://app.snyk.io/account)에서 복사하여 Eclipse 기본 설정 Snyk API 토큰 필드에 붙여넣습니다. **적용 및 닫기**를 클릭하여 분석을 시작합니다.

![Eclipse preferences with Snyk API Token filed and Apply and Close button](../../../.gitbook/assets/uuid-928012b7-8e49-fe6f-4965-77c5db026784-en.png)

### 환경 변수

프로젝트를 분석하기 위해 플러그인은 Snyk CLI를 사용합니다. CLI에는 다음 환경 변수가 필요합니다:

* `PATH`: 필요한 바이너리(예: 메이븐)로 가는 경로입니다. `PATH` 변수는 설정 대화 상자의 `Path` 필드를 사용하여 수동으로 조정할 수도 있습니다.
* `JAVA_HOME`: Java 종속성을 분석하는 데 사용하려는 JDK의 경로
* `http_proxy`  `https_proxy`: 형식의 값을 사용하여 설정`http://username:password@proxyhost:proxyport`.\
  **Note:** 값의 선행 `http://`는 `https_proxy`의 경우 `https://`로 변경되지 않습니다.

명령행에서 Eclipse를 시작하지 않거나 쉘 환경을 사용하여 Eclipse를 시작하는 스크립트 파일을 작성하지 않는 경우 쉘 환경에서만 이러한 변수를 설정하는 것(예: **\~/.bashrc** 사용)으로는 충분하지 않습니다.

* **Windows**에서는 GUI를 사용하여 변수를 설정하거나 [setx](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/setx) 도구를 사용하여 명령줄에서 변수를 설정합니다.
* **macOS**에서 launchd 프로세스는 Finder에서 직접 Eclipse를 시작하기 위해 환경 변수를 알아야 합니다. `launchctl setenv` 명령을 사용하여 이러한 환경 변수를 설정합니다(예: 시작 시 또는 사용자 로그인 시 실행하는 스크립트 사용).\
  **Note:** macOS UI에 대한 환경 변수 제공은 운영 체제 릴리스 간에 변경될 수 있으므로 `~/.bashrc`를 통해 정의할 수 있는 셸 환경을 활용하기 위해 Eclipse 앱을 시작하는 작은 셸 스크립트를 만드는 것이 더 쉬울 수 있습니다.
* **Linux**에서는 `/etc/environment` 파일을 업데이트하여 환경 변수를 Windows 관리자 및 UI로 전파할 수 있습니다.

## Snyk 플러그인을 사용하여 Eclipse 프로젝트 보호

From the Snyk results click the green arrow (![](../../../.gitbook/assets/uuid-aa090aa8-d4fe-eb5d-2505-54a0b1555be9-en.png)) whenever you are ready to scan your projects. Results appear in a short time, and your continue to work as usual in the meantime.

If for any reason you need to stop the scan before the build ends, click the red square(![](../../../.gitbook/assets/uuid-29be01e6-6913-25f8-15ed-a8cf47230fa0-en.png)). If you want to scan only a single project in your workspace, navigate to the Package Explorer panel, right click the root of the project you want to test, and then choose **Snyk test**.

When the scan ends, results and any relevant error messages are displayed from the **Snyk results**, grouped by project similar to the following:

![Results screen for scan with Eclipse plugin](../../../.gitbook/assets/uuid-e868f739-eb55-9bd6-be33-acbb230ec1fa-en.png)

## Work with Snyk results for Eclipse projects

### **Context menu**

Right click menu

Options include:

**Ignore issue**—Hover over the specific issue that you want to ignore for the next 30 days and then access the context menu.

**Snyk test**—Run the Snyk test for the entire workspace.

**Preferences**—Access and update Snyk Vuln Scanner preferences directly from the right click menu.

### **When collapsed**

**Title:** The name of the project.

**Dependency:** A summary of vulnerabilities and the number of affected paths found for each project.

### When expanded

**Title:** The full name of the vulnerability affecting your project, linked to a description and complete details of the vulnerability in the Snyk database, to assist you in resolving the issue.

**Dependency:** The name of the direct dependency package in your project (the package you explicitly installed) that is affected by the vulnerability, either directly or indirectly.

All details appear on a single row and the Dependency (the name of the package explicitly used in the code) and Package (the name of the package that actually contains the vulnerability) columns both display the name of the same package:

{% embed url="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-MdwVZ6HOZriajCf5nXH%2Fuploads%2Fgit-blob-4cdd086d6be47b598fc1a9a52c63023d59cff825%2Fuuid-e7accdc1-7495-e7a5-7a64-2403b066cb03-en.png?alt=media&token=e3bf024a-ba92-4b76-87be-b728d7edf092" %}
Eclipse results details
{% endembed %}

An arrow appears on the row, grouping together all relevant details, similar to the following examples:

{% embed url="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-MdwVZ6HOZriajCf5nXH%2Fuploads%2Fgit-blob-85e429be9a965c2dc534817a648773176a724531%2Fuuid-c71f67d1-80a3-7485-b33b-e602a1a5050e-en.png?alt=media&token=99e95293-bb37-4fed-8388-d9cb56a73092" %}
Eclipse results arrow on row grouping details
{% endembed %}

**Dependency when your project is affected by an indirect vulnerability, collapsed mode:**

{% embed url="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-MdwVZ6HOZriajCf5nXH%2Fuploads%2Fgit-blob-85e429be9a965c2dc534817a648773176a724531%2Fuuid-c71f67d1-80a3-7485-b33b-e602a1a5050e-en.png?alt=media&token=99e95293-bb37-4fed-8388-d9cb56a73092" %}
Collapsed mode, indirect vulnerability
{% endembed %}

Example:

Package X uses Package Y, which in turn uses Package Z.

Package Z contains a Cross-Site Scripting (XSS) vulnerability, indirectly affecting your project.

The Dependency (the name of the package explicitly used in the code) is Package X; the Package field displays Package Z (the name of the package that actually contains the vulnerability).

**Dependency when your project is affected by an indirect vulnerability, expanded mode:**

Click the arrow on the row to expand and view the full path from the direct dependency to the vulnerable package.

{% embed url="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-MdwVZ6HOZriajCf5nXH%2Fuploads%2Fgit-blob-992b169b89e7f3c45782fdeb47b205e3c0a95af8%2Fuuid-35658aaf-3359-80c2-c094-41a34c7863cc-en.png?alt=media&token=53c91ccc-f9bc-4ba7-a55f-8def3aa50d86" %}
Expanded mode, indierct vulnerability
{% endembed %}

On the preceding screen the full path would appear as:

\[Name of Package X]-->\[Name of Package Y]-->\[Name of Package Z]

**Package:** The name of the package in your project that is directly affected by the vulnerability. On the preceding screen:

* The Dependency is indicated as Package X—this is the package the developer explicitly uses in the code
* the Package field displays Package Z, which is the package that contains the vulnerability.

**Fix:** The name of the package if any and the version that it can be upgraded to in order to resolve the issue.

## Support / Contact

{% hint style="info" %}
If you need help, submit a [request](https://support.snyk.io/hc/en-us/requests/new) to Snyk Support.
{% endhint %}

## Share your experience

Snyk continuously strives to improve the Snyk plugins experience. If you would you like to share your feedback about the Snyk Eclipse plugin, [schedule a meeting](https://calendly.com/snyk-georgi/45min?month=2022-01).
