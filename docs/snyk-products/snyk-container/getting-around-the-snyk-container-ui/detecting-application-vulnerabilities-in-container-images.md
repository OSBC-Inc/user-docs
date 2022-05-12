# 컨테이너 이미지에서 애플리케이션 취약점 탐지

{% hint style="info" %}
Container Registry 통합의 경우 이 기능은 Node, Ruby, PHP, Python, Go binaries 및 Java에 대해 지원합니다. CLI 및 Kubernetes의 경우 이 기능은 Node, Golang 및 Java에 대해 지원합니다.
{% endhint %}

Snyk을 사용하면 한 번의 스캔으로 컨테이너 이미지뿐만 아니라 운영체제에서도 애플리케이션 디펜던시의 취약점을 탐지할 수 있습니다.

컨테이너 레지스트리와 통합하고 프로젝트를 가져오면 이미지를 스캔하고 취약점을 테스트합니다.

### 컨테이너 이미지에서 애플리케이션 취약점 스캔 활성화

1. 컨테이너 레지스트리 통합 설정으로 이동합니다.
2. _**Detect application vulnerabilities**_ 기능을 활성화하고 변경 내용을 저장합니다.

![](../../../.gitbook/assets/detect-app-vulns.png)

컨테이너 레지스트리, Kubernetes 통합을 사용하거나 Docker scan 명령을 통해 이미지를 스캔할 때 기본적으로 `--apps-vulns` 옵션도 사용합니다.

### CLI를 사용하여 취약점 탐지

#### 앱 취약점 옵션

`--app-vulns` 옵션을 사용하여 컨테이너 이미지에서 애플리케이션 디펜던시의 취약점을 탐지합니다.

Java의 경우 옵션을 지정할 때 기본적으로 중첩된 jar의 최상위를 스캔합니다.

#### 중첩된 Jars Depth 옵션

Java 애플리케이션의 경우 `--apps-vulns`를 사용할 때 `--nested-jars-depth=n` 옵션을 사용하여 Snyk이 압축을 풀 중첩된 jar의 수준을 설정할 수 있습니다. 기본값은 1입니다. 예를 들어, 2로 지정하면 Snyk은 jar에 있는 Jar의 압축을 풉니다. 3은 jar의 jar에 있는 Jar의 압축을 풉니다.

사용자는 —nested-jar-depth=0을 사용하여 불필요하다고 생각되는 스캔을 거부할 수 있습니다.

### 취약점 및 라이선스 Issues 보기

기능이 활성화되면 다음을 볼 수 있습니다.

* 컨테이너 이미지에서 감지된 매니페스트 파일의 디펜던시 및 라이선스 Issue
* 운영체제 패키지에서 발견된 취약점

Snyk으로 가져온 이미지는 **Projects** view의 레지스트리 레코드 아래에 나타나 이미지에서 발견된 운영체제 취약점을 표시합니다.

이 기능을 활성화하면 이미지에서 탐지된 중첩된 매니페스트 파일과 해당 취약점 및 라이선스 Issue도 볼 수 있습니다.

![](<../../../.gitbook/assets/mceclip2 (1) (1) (1) (3) (3) (4) (6) (1) (1) (1) (2).png>)

### 자동 스캔

Snyk은 프로젝트 설정을 기준으로 정기적으로 이미지를 스캔하고 운영체제 및 애플리케이션 디펜던시 모두에서 새로운 취약점이 확인되면 설정에 따라 이메일이나 Slack을 통해 업데이트합니다.

각 프로젝트의 설정에서 테스트 빈도를 선택할 수 있습니다.(기본 값은 일일 테스트)

![](<../../../.gitbook/assets/mceclip3 (1).png>)

**지원되는 레지스트리**

이 기능은 다음과 같은 컨테이너 레지스트리에서 지원됩니다.

* [ACR](https://docs.snyk.io/snyk-container/image-scanning-library/acr-image-scanning)
* [Amazon ECR](https://docs.snyk.io/snyk-container/image-scanning-library/ecr-image-scanning)
* [JFrog Artifactory](https://docs.snyk.io/snyk-container/image-scanning-library/jfrog-artifactory-image-scanning)
* [Docker Hub](https://docs.snyk.io/snyk-container/image-scanning-library/docker-hub-image-scanning)
* [GCR](https://docs.snyk.io/snyk-container/image-scanning-library/gcr-image-scanning)

**지원되는 통합**

지원되는 언어는 다음과 같은 통합에서 작동합니다.

| **Language** | **Container Registry** | **CLI** | **Kubernetes** |
| ------------ | ---------------------- | ------- | -------------- |
| Node         | Yes                    | Yes     | Yes            |
| Ruby         | Yes                    |         |                |
| PHP          | Yes                    |         |                |
| Python       | Yes                    |         |                |
| Go Binaries  | Yes                    | Yes     | Yes            |
| Java         | Yes                    | Yes     | Yes            |

***
