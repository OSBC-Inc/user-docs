---
description: 이 문서를 사용하여 JetBrains 플러그인을 시작하십시오.
---

# JetBrains 플러그인

Snyk에는 모든 Snyk 제품을 지원하는 JetBrains IDE용 플러그인이 있습니다: [Snyk Open Source](../../../snyk-products/snyk-open-source/), [Snyk Code](../../../snyk-products/snyk-code/), [Snyk Container](../../../snyk-products/snyk-container/) 및 [Snyk Infrastructure as Code](../../../snyk-products/snyk-infrastructure-as-code/). \
Snyk JetBrains 플러그인은 다음을 포함하여 애플리케이션 보안의 모든 측면을 다룹니다:

* 오픈 소스 종속성의 보안 취약성 (Snyk Open Source).
* 자사 코드의 보안 취약점 및 코드 품질 문제 (Snyk Code).
* Terraform, AWS CloudFormation, Kubernetes 및 Azure Resource Manager와 같은 코드형 인프라의 구성 문제 (ARM) (Snyk IaC)
* Kubernetes 워크로드 파일에서 발견된 컨테이너 이미지의 보안 취약점 (Snyk Container)

{% hint style="info" %}
Snyk JetBrains 플러그인은 JetBrains 마켓플레이스에 설치할 수 있습니다. [https://plugins.jetbrains.com/plugin/10972-snyk-vulnerability-scanner](https://plugins.jetbrains.com/plugin/10972-snyk-vulnerability-scanner).
{% endhint %}

## 지원되는 JetBrains IDE

Snyk은 다음 IDE에서 버전 2020.2의 JetBrains 플러그인 버전을 지원합니다:

* Android Studio
* AppCode
* GoLand
* IntelliJ
* PhpStorm
* PyCharm
* Rider
* RubyMine
* WebStorm

## Snyk JetBrains 플러그인 작동 방식

* 플러그인은 Snyk CLI를 기반으로 하지만 CLI만 기반으로 하는 것은 아닙니다. 플러그인은 Snyk 오픈 소스, Snyk IaC 및 Snyk Container용 CLI의 모든 제품 기능을 지원합니다.
* 플러그인은 백그라운드에서 CLI를 자동으로 다운로드합니다. [인증](jetbrains-plugins.md#authentication)하라는 메시지가 표시됩니다.
* Snyk은 [Snyk Code에서 지원하는 모든 언어를 지원](../../../snyk-products/snyk-code/snyk-code-language-and-framework-support.md)합니다. 모든 IDE(예: RubyMine)에 플러그인을 설치할 수 있습니다. 플러그인이 설치되면 Snyk는 찾은 모든 언어 파일을 분석합니다.
* CLI가 이미 머신에 설치된 경우 플러그인은 제공된 토큰을 사용합니다. 그렇지 않으면 플러그인 인[증 메커니즘](jetbrains-plugins.md#authentication)을 통해 인증 토큰을 제공해야 합니다.

## 플러그인 설치

IDE 플러그인 라이브러리를 사용하여 설치:

1. IDE에서 **Preferences** 창을 엽니다.
2. **Plugins** 탭으로 이동합니다.
3. **Plugins** 탭에서 **Snyk**을 검색합니다.
4. **Snyk vulnerability scanning** 플러그인을 선택하십시오.
5. **Install** 버튼을 클릭합니다.
6. 설치가 완료되면 IDE를 다시 시작합니다.

<figure><img src="../../../.gitbook/assets/spaces_-MdwVZ6HOZriajCf5nXH_uploads_git-blob-eff2d97f427de9d7d33c73231e5a806056705c30_Screen Shot (1).png" alt=""><figcaption><p>Snyk 취약점 스캐닝 플러그인 선택</p></figcaption></figure>

## 구성

### 환경

프로젝트를 분석하기 위해 플러그인은 분석하는 프로젝트 유형에 따라 다음 환경 변수가 필요한 Snyk CLI를 사용합니다.

* `PATH`: 필요한 바이너리의 경로(예: maven)
* `JAVA_HOME`: Java 의존성을 분석하는 데 사용할 JDK의 경로

명령줄에서 JetBrains IDE를 시작하지 않거나 셸 환경을 사용하여 시작하는 스크립트 파일을 생성하지 않는 경우 셸 환경에서만 이러한 변수를 설정하는 것(예: `~/.bashrc` 사용)으로는 충분하지 않습니다.

* On **Windows**, you can set the variables, using the GUI or on the command line using the `setx` tool.
* On **macOS**, the process `launchd` needs to know the environment variables if you want to launch the IDE from Finder directly. Set environment variables for applications launched using Finder by running the `launchctl setenv` command. You can do this start-up or by using a script you launch at user login.\
  **Note:** The provision of environment variables to the macOS UI can change between operating system releases, so it can be easier to create a small shell script that launches the IDE to leverage the shell environment, that can be defined using`~/.bashrc`.
* On **Linux**, updating the file `/etc/environment` can be used to propagate the environment variables to the windows manager and UI.

### Proxy

If you need to use a proxy server to connect to the internet, configure it using the [Jetbrains IDE settings](https://www.jetbrains.com/help/idea/settings-http-proxy.html). The Snyk plugin will use them.

## Authentication

The first time the CLI is needed, the plugin automatically downloads it in the background. There are a few ways to authenticate once the plugin is installed.

After the plugin is installed, you are prompted to authenticate and connect the IDE plugin to Snyk.

![Prompt to authenticate and start testing your code.](../../../.gitbook/assets/Screenshot%202022-02-10%20at%2017.07.52.png)

Click **Test code now**. The plugin relies on the Snyk CLI, which authenticates your machine against the Snyk Web UI.

Click **Authenticate** when prompted by Snyk.

![Prompt to authenticate](../../../.gitbook/assets/screen-shot-2021-09-29-at-4.04.29-pm.png)

When authentication is complete, a confirmation message appears.

![Authenticated confirmation message](../../../.gitbook/assets/screen-shot-2021-09-29-at-4.05.55-pm.png)

The IDE reads and saves the authentication on your local machine.

You can now close the browser window and return to the IDE.

The analysis starts automatically:

![Analysis by JetBrains plugin](../../../.gitbook/assets/Screenshot%202022-02-10%20at%2017.26.44.png)

### Add token manually

1. Produce the token here: [https://app.snyk.io/account](https://app.snyk.io/account)
2. **\[JetBrains IDE] >> Preferences >> Tools >> Snyk**
3. Paste or enter the token under **Connect IDE to Snyk**
4. Click **Apply or OK**

![Connect to Snyk IDE token](../../../.gitbook/assets/screen-shot-2021-09-30-at-8.10.21-am.png)

### Manual authentication

If you are unable to authenticate automatically or by adding the token, run `snyk auth` from the command line and follow the preceding steps to respond to the prompts. If you need help, submit a request to [Snyk support](https://snyk.zendesk.com/agent/dashboard).

![Prompts from authentication using snyk auth](../../../.gitbook/assets/screen-shot-2021-09-29-at-3.57.26-pm.png)

## Run an analysis

{% hint style="info" %}
Make sure your project file, for example, requirements.txt, is saved before running an analysis.
{% endhint %}

To trigger an analysis during your daily coding workflow, click either the run (play) button, or **Run scan**.

![Play button and Run scan link](../../../.gitbook/assets/play-run.png)

## Analysis results: Snyk Open Source

Snyk Open Source analysis shows a list of vulnerabilities and license issues found in the manifest file. For more detailed information select a vulnerability or license issue.

![Display more information for a vulnerability or license issue](../../../.gitbook/assets/results-os.png)

## Analysis results: Snyk Code

Snyk Code analysis shows a list of security vulnerabilities and code issues found in your application code. For more details and examples of fixes on how others fixed the issue, select the security vulnerability or the code security issue:

![Display more information for a vulnerability or code issue](../../../.gitbook/assets/results-code.png)

## Analysis results: Snyk Configuration

Snyk Configuration analysis shows issues in your Terraform, Kubernetes, AWS CloudFormation, and Azure Resource Manager (ARM) code with every scan. Based on the Snyk CLI, the scan is fast and friendly for local development. For more detailed information select an issue.

![Display more information for Snyk Configuration analysis](../../../.gitbook/assets/intellij\_iac\_issues.png)

The Snyk plugin provides information so you can quickly understand and fix the underlying issue:

* **Description:** what the misconfiguration is
* **Impact:** how the misconfiguration could potentially be exploited
* **Path:** which path in the tree the issue occurs
* **Remediation:** how to fix the issue
* **References:** where you can investigate deeper from a variety of sources
* **Ignore:** a button to ignore the issue if applicable

## Analysis results: Snyk Container

The plugin scans Kubernetes configuration files and searches for container images. Vulnerabilities are found fast using the extracted container images and comparative analysis against the latest information from the [Snyk Intel Vulnerability Database](https://security.snyk.io).

Snyk Container analysis shows each of the security vulnerabilities to which your image might be vulnerable. For more detailed information select a vulnerability.

A comparison table is displayed with various severity levels such as critical or high. This shows the difference in vulnerabilities between the current image and the image recommended by Snyk, with the same characteristics sorted by severity. This helps you decide if you want to upgrade your image to the recommended one and increase the level of confidence in the image you are running in production.

![Display more information for Snyk Container analysis](../../../.gitbook/assets/intellij\_container\_vulnerabilites.png)

## How Snyk Container and Kubernetes integration works

The plugin scans your Kubernetes workload files and collects the images used. To troubleshoot whether a plugin is correctly scanning a container image, you can verify:

* Whether the image definition is in the Kubernetes YAML file in the project. Make sure you have the image specified with a YAML value to the YAML image key.
* Whether the container image has been successfully built locally and/or pushed to a container registry. It is also a good practice to verify this before referring to the container image in the Kubernetes YAML file.

If you encounter an error [contact support](https://snyk.zendesk.com/agent/dashboard).

For each image found, perform a test with the Snyk CLI.

* Refer to the [doc](https://docs.snyk.io/products/snyk-container/snyk-cli-for-container-security#testing-an-image) for more information about how Snyk Container performs a test on the image.
* While testing the image the CLI downloads the image if it is not already available locally in your Docker daemon.
* Snyk plans to expand the scope of Container scanning, so if there are more files (like Dockerfiles) or workflows that you want to be supported, submit a feature request [to Snyk support](https://support.snyk.io/hc/en-us/requests/new).

## Filter results

### Filter by severity

Snyk reports critical, high, medium and low severities. You can filter for the severity level you need by selecting the value from the dropdown as shown in the screenshot that follows. By default all levels are selected. You must select at least one.

![Select severity level to report](../../../.gitbook/assets/filter-severity.png)

### Filter by issue type

Snyk reports the following types of issues:

* **Open Source Vulnerabilities**: found in open source dependencies
* **Security Vulnerabilities**: found in your application’s source code
* **Quality Issues**: found in your application source code
* **Configuration Issues**: found in infrastructure as code files
* **Container Vulnerabilities**: found in images sourced from Kubernetes workload files

You can filter for each one of them by selecting the value from the dropdown as shown in the screenshot that follows. By default all three issue types shown are selected.

![Select issue type to support](../../../.gitbook/assets/fillter-issuetype.png)

## Plugin configuration

After the plugin is installed, you can set the following configurations for the plugin, using **Preferences → Tools → Snyk**:

* **Token**: the token that should be used for authentication with Snyk (can be generated through the Account Settings in the Snyk Web UI)
* **Custom endpoint**: custom endpoint for the Snyk Web UI, if needed
* **Ignore unknown CA**: for ignoring the SSL cert, if needed
* **Organization**: the org to run Snyk test against (similar to the `--org=` option in the CLI).
* **Additional parameters**: additional CLI snyk test options you want to use for the test
* **Snyk Open Source vulnerabilities**: analyze the project for open source vulnerabilities through the CLI using Snyk Open Source; enabled by default
* **Snyk Infrastructure as Code issues**: analyze the project for insecure configurations in Terraform and Kubernetes code; enabled by default
* **Snyk Container vulnerabilities**: analyze the project for container vulnerabilities in container images and Kubernetes applications; enabled by default
* **Snyk Code Security issues**: analyze the project for security vulnerabilities in your application code using Snyk Code; enabled by default
* **Snyk Code Quality issues**: analyze the project for quality issues in your application code using Snyk Code; disabled by default

#### Organization setting

This setting allows you to specify an organization slug name to run tests for that organization. The value must match the URL slug as displayed in the URL of your org in the Snyk UI: `https://app.snyk.io/org/[orgslugname]`.

If not specified, preferred organization as defined in your [web account settings](https://app.snyk.io/account) is used to run tests.

### Support and contact information

{% hint style="info" %}
Need more help? [Contact Snyk support](https://support.snyk.io/hc/en-us/requests/new).
{% endhint %}

**Share your experience.**

Snyk continuously strives to improve the plugins experience. Would you like to share with us your feedback about the Snyk JetBrains Plugin? [Schedule a meeting](https://calendly.com/snyk-georgi/45min?month=2022-01).
