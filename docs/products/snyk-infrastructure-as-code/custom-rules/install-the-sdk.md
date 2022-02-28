# SDK 설치

다음 옵션 중 하나를 사용하여 SDK를 설치합니다.

* [Install the SDK with npm](install-the-sdk.md#install-the-sdk-with-npm)
* ​[Install the SDK using the prebuilt binaries​](install-the-sdk.md#install-the-sdk-using-the-prebuilt-binaries)
* [Install the SDK with Homebrew](install-the-sdk.md#install-the-sdk-with-homebrew)
* [​Install the SDK with the Windows Scoop package manager](install-the-sdk.md#install-the-sdk-with-the-windows-scoop-package-manager)
* [Install the SDK with Docker](install-the-sdk.md#install-the-sdk-with-docker)

설치 후 [Getting started](getting-started-with-the-sdk/) 가이드를 통해 Rule 작성을 시작할 수 있습니다.

### npm을 이용하여 SDK 설치

npm을 이용하여 SDK를 설치합니다.

#### 전제 조건

* Node version 10 이상을 사용하여 로컬 환경에 최신 버전의 npm을 설치했는지 확인하세요.

#### **Steps**

로컬에서 사용하기 위해 설치하려면 다음 명령어를 실행합니다.

```
npm install -g snyk-iac-rules
```

설치했으면 SDK를 사용할 준비가 된 것입니다. 다음 명령어를 실행하여 작동하는지 확인하세요.

```
snyk-iac-rules --help
```

### 사전 빌드된 바이너리 파일을 사용하여 SDK 설치

SDK의 사전 빌드된 바이너리 파일을 다운로드하여 사용할 수 있습니다. 사전 빌드된 바이너리를 다운로드하려면 GitHub의 SDK 저장소 페이지에 있는 [**Releases tab**](https://github.com/snyk/snyk-iac-rules/releases)을 방문하세요.

![](../../../.gitbook/assets/screenshot-2021-09-24-at-13.44.36.png)

원하는 바이너리 아카이브를 다운로드한 후 터미널을 열고 다음 명령어를 실행합니다(이러한 명렁어는 Intel 기반 macOS에서 실행 중이며 SDK 버전 `0.0.5`를 다운로드 한다고 가정합니다).

```
$ tar xzf snyk-iac-rules_0.0.5_Darwin_x86_64.tar.gz 
$ sudo mv snyk-iac-rules /usr/local/bin
```

설치가 완료되었는지 확인하려면 다음 명령어를 실행하세요.

```
snyk-iac-rules --help
```

### Homebrew를 이용하여 SDK 설치

macOS 및 Linux 환경에서 Homebrew를 사용하여 SDK를 설치할 수 있습니다. 설치를 위한 저장소는 [Github](https://github.com/snyk/homebrew-tap)에 있습니다.

#### 전제 조건

* macOS 및 Linux 환경에서만 지원합니다.
*   [Homebrew](https://brew.sh/index\_he)가 이미 설치되어 있는지 확인합니다.

    ```
    brew tap snyk/tap
    ```

#### **Steps**

다음과 같이 SDK를 설치합니다.

```
brew install snyk-iac-rules
```

### Windows Scoop package manager를 이용하여 SDK 설치

Wndows 환경에서 Scoop을 사용하여 snyk-iac-rules SDK를 설치할 수 있습니다. 설치를 위한 저장소는 [Github](https://github.com/snyk/scoop-snyk)에 있습니다.

#### 전제 조건

* Windows 환경에서만 지원합니다.
*   [Scoop](https://scoop.sh)이 이미 설치되었는지 확인합니다.

    ```
    scoop bucket add snyk https://github.com/snyk/scoop-snyk
    ```

#### **Steps**

다음과 같이 SDK를 설치합니다.

```
scoop install snyk-iac-rules
```

### Docker를 이용하여 SDK 설치

로컬 디렉토리에 custom rules를 작성하는 동안 Docker를 사용하여 snyk-iac-rules SDK를 설치하고 실행할 수 있습니다. 이미지는[ Docker Hub repo](https://hub.docker.com/r/snyk/snyk-iac-rules)에서 저장합니다.

#### **Prerequisites**

* [Docker](https://docs.docker.com/get-docker/)가 이미 설치되었는지 확인하세요.
* Linux 컨테이너에서만 지원합니다.

#### **Steps**

다음과 같이 Docker 이미지를 pull합니다.

```
docker pull snyk/snyk-iac-rules
```

다음 명령어를 사용하여 SDK를 실행합니다.

```
docker run --rm -v $(pwd):/app snyk/snyk-iac-rules {SDK command}
```

예를 들어 custom rules 템플릿을 생성하려면 다음 명령어를 실행할 수 있습니다.

```
docker run --rm -v $(pwd):/app snyk/snyk-iac-rules template -r {rule_name}
```

### 참고 항목

* [​Getting started with the SDK​](getting-started-with-the-sdk/)
* ​[SDK reference​](sdk-reference.md)
