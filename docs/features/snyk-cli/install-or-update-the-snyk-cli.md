# Snyk CLI 설치 또는 업데이트

이 페이지에 설명된 방법을 사용하여 [Snyk CLI](./)를 설치할 수 있습니다.

Snyk CLI를 설치한 후 [인증](cli-3/undefined.md)해야 합니다. 그런 다음 설치 테스트부터 [시작](cli.md)하여 취약점 테스트 및 수정을 시작할 수 있습니다.

## npm 또는 Yarn을 사용하여 Snyk CLI 설치

npm을 사용하여 Snyk CLI를 설치하기 전에 **필수 구성 요소**를 설치했는지 확인하십시오.

* Node 버전 12 이상을 사용하여 로컬 환경에 최신 버전의 npm을 설치합니다.\
  Node를 업데이트하는 단계는[ What version of Node is required for Snyk?](https://support.snyk.io/hc/en-us/articles/360004183317-What-version-of-Node-is-required-for-Snyk-) 를 참조하십시오.
* Alpine Linux에서 Snyk를 실행하려면 먼저 libstdc++를 설치하십시오.\
  자세한 내용은 [How can I use CLI on an Alpine operating system?](https://support.snyk.io/hc/en-us/articles/360001929038) 를 참조하십시오.

그런 다음 **다음 단계에 따라 npm 또는 Yarn으로 설치**합니다:

[Snyk CLI는 npm 패키지로 사용할 수 있습니다](https://www.npmjs.com/package/snyk). Node.js가 로컬에 설치된 경우 npm install `snyk -g`를 실행하여 npm 패키지를 설치할 수 있습니다.

Yarn을 사용하는 경우 `yarn global add snyk`를 실행하여 **설치**합니다.

## 독립 실행형 실행 파일로 설치

[GitHub Releases](https://github.com/snyk/snyk/releases) 를 사용하여 플랫폼용 Snyk CLI의 독립 실행형 실행 파일(macOS, Linux, Windows)을 다운로드합니다.

Snyk는 또한 Snyk CDN(Content Delivery Network)에서 이러한 독립 실행형 실행 파일을 제공합니다. 다운로드 링크는 [https://static.snyk.io/cli/latest/release.json](https://static.snyk.io/cli/latest/release.json)을 참조하십시오. 특정 버전 또는 플랫폼의 예는 다음과 같습니다.

* [https://static.snyk.io/cli/v1.666.0/release.json](https://static.snyk.io/cli/v1.666.0/release.json)
* [https://static.snyk.io/cli/latest/snyk-macos](https://static.snyk.io/cli/latest/snyk-macos)

예를 들어 macOS에서 최신 Snyk CLI를 다운로드하여 실행하려면 다음을 실행할 수 있습니다:

```bash
curl https://static.snyk.io/cli/latest/snyk-macos -o snyk
chmod +x ./snyk
mv ./snyk /usr/local/bin/
```

또한 직접 링크를 사용하여 실행 파일을 다운로드할 수도 있습니다.

* **macOS**: [https://static.snyk.io/cli/latest/snyk-macos](https://static.snyk.io/cli/latest/snyk-macos)
* **Windows**: [https://static.snyk.io/cli/latest/snyk-win.exe](https://static.snyk.io/cli/latest/snyk-win.exe)
* **Linux**: [https://static.snyk.io/cli/latest/snyk-linux](https://static.snyk.io/cli/latest/snyk-linux)
* **Linux/arm64**: [https://static.snyk.io/cli/latest/snyk-linux-arm64](https://static.snyk.io/cli/latest/snyk-linux-arm64)
* **Alpine**: [https://static.snyk.io/cli/latest/snyk-alpine](https://static.snyk.io/cli/latest/snyk-alpine)

{% hint style="warning" %}
Apple M1(darwin/arm64)의 경우 다음을 참조하십시오: [How do I run Snyk CLI on an Apple M1 machine?](https://support.snyk.io/hc/en-us/articles/5022278090397)
{% endhint %}

{% hint style="warning" %}
주의: 이 방법의 단점은 Snyk CLI를 수동으로 최신 상태로 유지해야 한다는 것입니다.
{% endhint %}

## Homebrew로 설치(macOS, Linux)

다음을 실행하여 [Homebrew](https://brew.sh/)로 [Snyk의 탭](https://github.com/snyk/homebrew-tap)에서 Snyk CLI를 설치합니다. 탭은 최신 Snyk CLI 릴리스로 매일 업데이트됩니다.

```bash
brew tap snyk/tap
brew install snyk
```

{% hint style="warning" %}
Apple M1(darwin/arm64)의 경우 다음을 참조하십시오: [How do I run Snyk CLI on an Apple M1 machine?](https://support.snyk.io/hc/en-us/articles/5022278090397)
{% endhint %}

## Scoop을 사용하여 설치 (Windows)

다음과 같이 [Scoop](https://scoop.sh/)을 사용하여 [Snyk의 버킷](https://github.com/snyk/scoop-snyk)에서 Snyk CLI를 설치합니다. 버킷은 최신 Snyk CLI 릴리스로 매일 업데이트됩니다.

```
scoop bucket add snyk https://github.com/snyk/scoop-snyk
scoop install snyk
```

## Docker 이미지의 Snyk CLI

Snyk CLI는 Docker 이미지에서도 실행할 수 있습니다. Snyk는 [snyk/snyk-cli](https://hub.docker.com/r/snyk/snyk-cli) 및 [snyk/snyk](https://hub.docker.com/r/snyk/snyk)에서 여러 Docker 이미지를 제공합니다(자세한 내용은 [GitHub의 snyk/snyk-images](https://github.com/snyk/snyk-images) 참조).

이러한 이미지는 Snyk CLI를 래핑하고 태그에 따라 다양한 프로젝트에 대한 관련 도구가 함께 제공됩니다(예: snyk/snyk-cli를 사용하여 Gradle 프로젝트 스캔):

```bash
docker run -it \
    -e "SNYK_TOKEN=<TOKEN>" \
    -v "<PROJECT_DIRECTORY>:/project" \
    -v "/home/user/.gradle:/home/node/.gradle" \
  snyk/snyk-cli:gradle-5.4 test --org=my-org-name
```

## Snyk 통합의 일부 설치

Snyk은 또한 개발자 도구에 대한 많은 통합을 제공합니다. 이러한 통합은 Snyk CLI를 설치하고 관리합니다. 통합에는 다음이 포함됩니다:

* [Snyk Jenkins plugin](https://github.com/jenkinsci/snyk-security-scanner-plugin)
* [CircleCI Orb](https://github.com/snyk/snyk-orb)
* [Azure Pipelines Task](https://github.com/snyk/snyk-azure-pipelines-task)
* [GitHub Actions](https://github.com/snyk/actions)
* [IntelliJ IDE Plugin](https://github.com/snyk/snyk-intellij-plugin)
* [VS Code Extension](https://marketplace.visualstudio.com/items?itemName=snyk-security.snyk-vulnerability-scanner)
* [Eclipse IDE Extension](https://github.com/snyk/snyk-eclipse-plugin)
* [Maven plugin](https://github.com/snyk/snyk-maven-plugin)

자세한 내용은 [통합](../integrations/) 문서를 참조하세요.
