# SDK 설치

​Install the SDK using one of these options:다음 항목중 하나를 선택하여 SDK 설치를 진행합니다.

* [Install the SDK with npm](install-the-sdk.md#install-the-sdk-with-npm)
* ​[Install the SDK using the prebuilt binaries​](install-the-sdk.md#install-the-sdk-using-the-prebuilt-binaries)
* [Install the SDK with Homebrew](install-the-sdk.md#install-the-sdk-with-homebrew)
* [​Install the SDK with the Windows Scoop package manager](install-the-sdk.md#install-the-sdk-with-the-windows-scoop-package-manager)
* [Install the SDK with Docker](install-the-sdk.md#install-the-sdk-with-docker)

설치 후에는 규칙 작성을 시작할 수 있습니다. [Getting started](getting-started-with-the-sdk/)를 참조하세요.

### npm을 사용하여 SDK 설치

npm을 사용하여 SDK를 설치합니다.

#### 전제 조건

* node 버전 10 이상을 사용하여 로컬 환경에 최신 버전의 npm을 설치했는지 확인하세요.

#### **Steps**

로컬 사용을 위해 해당 명령을 실행하여 설치합니다.

```
npm install -g snyk-iac-rules
```

설치를 완료하면 SDK를 사용할 준비가 되었습니다. 다음 명령어를 실행하여 SDK 작동을 확인하세요.

```
snyk-iac-rules --help
```

### 사전 빌드된 바이너리를 사용하여 SDK 설치 진행

SDK의 사전 빌드된 바이너리 파일을 다운로드하여 사용할 수 있습니다. 사전 빌드된 바이너리를 다운로드하려면 GitHub의 SDK 리포지토리 페이지에 있는 [**Release**](https://github.com/snyk/snyk-iac-rules/releases) 탭을 방문하세요.

![](../../../.gitbook/assets/screenshot-2021-09-24-at-13.44.36.png)

원하는 바이너리 아카이브를 다운로드한 후 터미널을 열고 다음 명령을 실행합니다(해당 명령은 Intel 기반 macOS에서 실행 중이며 SDK 버전 `0.0.5`를 다운로드하고 있다고 가정합니다).

```
$ tar xzf snyk-iac-rules_0.0.5_Darwin_x86_64.tar.gz 
$ sudo mv snyk-iac-rules /usr/local/bin
```

SDK 설치를 확인하려면 다음과 같이 실행합니다.

```
snyk-iac-rules --help
```

### Homebrew를 사용하여 SDK 설치

macOS 및 Linux 환경에서 Homevrew를 사용하여 SDK를 설치할 수 있습니다. 설치를 위한 저장소는[ GitHub](https://github.com/snyk/homebrew-tap)에 있습니다.

#### 전제 조건

* macOS 및 Linux 환경에서만 지원합니다.
*   [Homebrew](https://brew.sh/index\_he)를 이미 설치한 상태에서 진행합니다.

    ```
    brew tap snyk/tap
    ```

#### 실행 단계

다음과 같이 SDK를 설치합니다.

```
brew install snyk-iac-rules
```

### Windows Scoop 패키지 매니저를 사용하여 SDK 설치

Window 환경에서 Scoop을 사용하여 SDK를 설치할 수 있습니다. snyk-iac-rules 설치를 위한 저장소는[ GitHub](https://github.com/snyk/scoop-snyk)에 있습니다.

#### **Prerequisites**

* Windows 환경에서만 지원합니다.
*   [Scoop](https://scoop.sh)을 이미 설치된상태에서 진행합니다.

    ```
    scoop bucket add snyk https://github.com/snyk/scoop-snyk
    ```

#### 실행 단계

다음과 같이 SDK를 설치합니다.

```
scoop install snyk-iac-rules
```

### Docker를 사용하여 SDK 설치

로컬 디렉터리에 사용자 정의 규칙을 작성하는 동안 Docker를 사용하여 snyk-iac-rules SDK를 설치하고 실행할 수 있습니다. 이미지는 [Docker Hub repo](https://hub.docker.com/r/snyk/snyk-iac-rules)에 저장됩니다.

#### 전제 조건

* 이미 [Docker](https://docs.docker.com/get-docker/)가 설치되어 있는 상태에서 진행합니다.
* Linux 컨테이너에서만 지원합니다.

#### 실행 단계

다음과 같이 Docker 이미지를 가져옵니다.

```
docker pull snyk/snyk-iac-rules
```

다음 명령을 사용하여 SDK를 실행합니다.

```
docker run --rm -v $(pwd):/app snyk/snyk-iac-rules {SDK command}
```

예를 들어, 사용자 지정 규칙 템플릿을 생성하려면 다음과 같이 실행할 수 있습니다.

```
docker run --rm -v $(pwd):/app snyk/snyk-iac-rules template -r {rule_name}
```

### 추가 내용

* [​Getting started with the SDK​](getting-started-with-the-sdk/)
* ​[SDK reference​](sdk-reference.md)
