# Azure Pipelines 통합

## Azure Pipelines 통합 개요

Snyk은 애플리케이션 및 컨테이너 취약점을 자동으로 찾아 수정함으로써 Azure Pipeline을 포함한 Microsoft Azure 에코시스템 전반의 보안을 지원합니다.

Azure Pipeline에 대한 즉시 사용 가능한 작업을 Azure 인터페이스에서 직접 빠르게 삽입할 수 있으므로 추가 코딩 없이 파이프라인을 사용자 정의하고 자동화할 수 있습니다. 포함된 작업 중에는 Snyk 작업이 있습니다.

일상적인 작업의 일부로 보안 취약성 및 라이센스 문제를 테스트하기 위해 파이프라인에 Snyk 태스크를 포함할 수 있습니다. 이 방법으로 애플리케이션 종속성 및 컨테이너 이미지에 보안 취약점이 있는지 테스트하고 모니터링할 수 있습니다. 테스트가 완료되면 Snyk 인터페이스뿐만 아니라 Azure Pipeline 출력에서 직접 결과를 검토하고 작업할 수 있습니다.

Snyk 보안 스캔 작업은 Snyk 및 Azure DevOps에서 지원하는 모든 언어에 사용할 수 있습니다.

## Snyk 보안 스캔 Task 작동 방식

Snyk 보안 스캔 Task를 파이프라인에 추가한 후 파이프라인이 실행될 때마다 Snyk Task는 다음 작업을 수행합니다.

### **Test**

1. Snyk은 애플리케이션 종속성 또는 컨테이너 이미지에 취약점 및 라이센싱 문제가 있는지 테스트하고 취약점과 이슈를 나열합니다.
2. Snyk이 취약점 또는 라이선스 이슈를 발견하면 구성에 따라 다음 중 하나를 수행합니다.
   * 파이프라인 실패
   * 파이프라인 진행

### **Monitor**

**snyk test**가 완료되면 **snyk monitor**를 수행할 수 있습니다. **snyk monitor**는 프로젝트 종속성의 스냅샷을 [snyk.io](https://snyk.io) 계정에 저장합니다. 여기서 모든 문제가 있는 의존성 트리를 보고 종속성에서 새로운 문제가 발견되면 알림을 받을 수 있습니다.

## Azure pipelines에 Snyk extension 설치

파이프라인 빌드의 일부로 Snyk task을 사용하려면 먼저 [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=Snyk.snyk-security-scan)에서 조직별 Azure DevOps 인스턴스에 extension을 설치하십시오.

### **전제 조건**

* [https://snyk.io/](https://snyk.io)에서 Snyk 계정을 생성합니다.
* 사용자가 이 계정의 소유자인지 또는 관리자인지 확인합니다.

### 진행 단계

1. Snyk 계정에 액세스합니다.
2. free plans를 이용하시려면 **General Account Settings**로 이동하여 개인 API 인증 토큰을 찾아 복사하여 저장하십시오.
3. paid plans의 경우 통합할 조직으로 이동한 다음 **Settings**로 이동하여 새 서비스 계정 토큰을 생성합니다. 복사하여 저장하십시오.
4. Azure DevOps 계정에 액세스하고 **Extensions -> Browse marketplace**로 이동합니다.
5. **Snyk Security Scan** extension을 검색하고 **Get it free**를 클릭합니다.
6. **Project Settings** —> **Pipelines** —> **Service Connections**을 통해 프로젝트에 new **Service Connection**을 생성합니다.
7. **Snyk Authentication** 서비스 연결을 선택합니다.
8. Snyk Authentication 서비스 연결 양식에 **서비스 연결 이름**과 함께 **서버 URL** 및 **Snyk API 토큰**을 입력합니다.
9. **Save**를 클릭하여 새 서비스 연결이 서비스 연결 목록에 나타나는지 확인합니다.

![Create your first service connection](../../../.gitbook/assets/ap\_-\_search.jpg)

![New Snyk authentication service connection](../../../.gitbook/assets/ap\_-\_config.jpg)

## 파이프라인에 Snyk Security Task 추가

### 전제 조건

* 테스트를 진행할 코드에 대한 파이프라인이 저장소 내에 있는지 확인합니다.
* Azure Repos wizard를 사용하여 파이프라인을 생성한 경우 이 파일을 `azure-pipelines.yml`이라고 합니다.
* 이 저장소에 여러 서비스 연결이 있는 경우 파이프라인에 사용할 항목을 Snyk 관리자에게 문의하십시오.
* 컨테이너를 테스트할 때 사용할 추가 기본 이미지 데이터를 위해 Dockerfile을 추가하려면 이미지가 빌드되었는지 확인하십시오.

### 요구 사항

이 확장을 사용하려면 build agent에 Node.js 및 npm이 설치되어 있어야 합니다. 이러한 기능은 기본적으로 모든 Microsoft-hosted build agents에서 사용할 수 있습니다. 그러나 self-hosted build agent를 사용하는 경우 Node.js 및 npm을 명시적으로 활성화하고 해당 에이전트가 [PATH](https://en.wikipedia.org/wiki/PATH\_\(variable\))에 있는지 확인해야 할 수 있습니다. 이 작업은 파이프라인에 SnykSecurityScan 작업을 추가하기 전에 [NodeTool task from Microsoft](https://docs.microsoft.com/en-us/azure/devops/pipelines/tasks/tool/node-js?view=azure-devops) 작업을 사용하여 수행할 수 있습니다.

### 진행 단계

1. 파이프라인을 만들거나 기존 파이프라인을 편집할 때 Snyk Security Scan 태스크를 추가합니다. [Azure Pipelines documentation](https://docs.microsoft.com/en-us/azure/devops/pipelines/?view=azure-devops)를 참조하십시오.
2. Azure에서 취약점을 검색할 파이프라인에 액세스합니다. 편집할 수 있도록 열고 Snyk 작업을 삽입할 지점 바로 앞에 빌드 단계가 포함되어 있는지 확인합니다. 이것은 필수는 아니지만 프로젝트 간의 일관성을 유지하기 위한 사례로 간주됩니다.
3. **assistant**를 열고 Snyk Security Scan 작업을 검색한 후 다음 스크린샷에 표시된 대로 클릭합니다. 구성 패널이 어시스턴트 상단에 열립니다.\
   ![](../../../.gitbook/assets/azure.png)
4. 구성의 필드를 완료합니다. 매개 변수에 대한 자세한 내용은 [Snyk GitHub repo](https://github.com/snyk/snyk-azure-pipelines-task#task-parameters) 또는 이 문서의 다음 섹션인 [Snyk Security Scan task parameters and values](azure-pipelines-integration.md)를 참조하십시오. **Note:** **Snyk이 이슈를 찾을 경우 빌드 실패 옵션**을 선택하면 빌드가 실패하면 파이프라인 작업이 Snyk 태스크에 의해 실패합니다. **Snyk이 이슈를 찾을 경우 빌드 실패 옵션**을 선택 취소하면 Snyk 태스크가 취약점을 테스트하지만 파이프라인 작업이 실패하지는 않습니다. 컨테이너 이미지를 테스트할 때 DockerfilePath 속성을 사용하여 Dockerfile의 경로를 지정하여 기본 이미지의 문제에 대한 추가 정보를 받을 수 있습니다. **컨테이너를 테스트**할 때 기본 이미지 데이터를 추가하기 위해 Dockerfile을 추가하려면 이미지가 빌드되었는지 확인하십시오.
5. **npm publish** 또는 **docker push**같은 배포 단계 전에 커서를 파이프라인 내부에 놓습니다. **Note:** 파이프라인 내에 Snyk Security Scan 태스크의 여러 인스턴스가 있을 수 있습니다. 이 기능은 테스트할 프로젝트 매니페스트 파일이 여러 개 있거나 응용 프로그램과 컨테이너 이미지를 모두 테스트하려는 경우에 유용할 수 있습니다.
6.  구성 패널에서 **Add**를 클릭합니다. 태스크는 다음과 같이 커서가 배치된 파이프라인에 삽입됩니다.

    ```
       - task: SnykSecurityScan@1
         inputs:
           testType: 'app'
           monitorWhen: 'always'
           failOnIssues: true
    ```
7. 파이프라인에 포함되면 파이프라인이 실행될 때마다 태스크가 실행되고 결과가 Azure Pipelines output view에 표시됩니다.

![Azure pipelines output view](../../../.gitbook/assets/uuid-d570e34b-3973-2044-598b-cb89c82a1db0-en.png)

> Snyk 태스크가 빌드에 실패하면 `snyk test`로 인해 빌드가 실패했음을 나타내는 오류 메시지가 결과에 나타납니다.

## Snyk Security Scan 태스크 파라미터 values

이 섹션에서는 Azure Pipelines 통합을 위한 Snyk 태스크 파라미터, Azure Pipelines의 구성 패널에 있는 병렬 구성 필드 및 유효한 values에 대해 설명합니다.

| <p><strong>Configuration field</strong><br>(Parameter)</p>                                               | **Description**                                                                                                                                                                                                                                                                                                                                                              | **Required** | **Default**   | **Type**                                                                          |
| -------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | ------------- | --------------------------------------------------------------------------------- |
| <p><strong>Snyk API token</strong><br><strong>service</strong><br>(ConnectionEndpoint)<br></p>           | <p>Snyk API 토큰이 정의된 Azure DevOps 서비스 연결 endpoint입니다. 관리자는 이를 Azure DevOps 프로젝트 설정 내에서 정의하고 서로 다른 연결을 구분하기 위해 고유한 문자열로 할당합니다. 구성 패널에는 다음과 같은 드롭다운 목록에서 사용 가능한 모든 Snyk 서비스 연결이 표시됩니다.<img src="../../../.gitbook/assets/uuid-9c6a12b4-2c03-2248-ad0e-c7437a35e142-en.png" alt="image3.png"></p><p>드롭다운 목록에서 여러 Snyk 서비스 연결을 사용할 수 있는 경우 작업 중인 파이프라인에 사용할 항목을 관리자에게 문의하십시오.</p> | Yes          | none          | String / Azure Service Connection Endpoint of type SnykAuth / Snyk Authentication |
| <p><strong>What do you want to test</strong> (testType)<br></p>                                          | 이 표의 나머지 부분에 설명된 대로 표시할 동적 필드를 결정합니다.                                                                                                                                                                                                                                                                                                                                        | Yes          | "application" | string: "app" or "container"                                                      |
| **Container Image Name** (dockerImageName)                                                               | <p>테스트할 컨테이너 이미지의 이름입니다.</p><p><strong>What do you want to test</strong>가 <strong>Container Imager</strong>로 설정된 경우 이 동적 필드가 나타납니다.</p><p>컨테이너 이미지를 테스트하는 경우 <strong>Yes</strong>로 설정합니다.</p>                                                                                                                                                                                | Yes          | none          | string                                                                            |
| **Path to Dockerfile** (dockerfilePath)                                                                  | <p><code>dockerImageName</code>에 해당하는 Dockerfile의 경로입니다. </p><p><strong>What do you want to test</strong>가 <strong>Container Imager</strong>로 설정된 경우 이 동적 필드가 나타납니다.<br></p><p>컨테이너 이미지를 테스트하는 경우 <strong>Yes</strong>로 설정합니다.</p>                                                                                                                                           | Yes          | none          | string                                                                            |
| **Custom path to manifest file to test** (targetFile)                                                    | 애플리케이션 유형 테스트에만 적용됩니다. Snyk에서 사용할 매니페스트 파일의 경로입니다. 표준이 아닌 경우에만 제공되어야 합니다. 이 동적 필드는 **What do you want to test**가 **Application**으로 설정된 경우 나타납니다.                                                                                                                                                                                                                             | No           | none          | string                                                                            |
| **Testing severity threshold** (severityThreshold)                                                       | <p>테스트할 때 사용할 심각도 임계값입니다. 기본적으로 모든 심각도 유형의 문제가 발견됩니다.</p><p><strong>Note</strong>: 구성되지 않은 경우 기본 심각도는 <strong>Low</strong>로 설정됩니다.</p>                                                                                                                                                                                                                                       | No           | "Low"         | string: "low" or "medium" or "high"                                               |
| **When to run Snyk Monitor** (monitorWhen)                                                               | **snyk monitor**를 실행하여 애플리케이션 또는 컨테이너 이미지의 의존성 트리를 캡처하고 Snyk 내에서 모니터링합니다.                                                                                                                                                                                                                                                                                                    | Yes          | "always"      | string: "always", "onIssuesFound", or "never"                                     |
| **Fail build if Snyk finds issues** (failOnIssues)                                                       | Snyk에서 발견한 이슈를 기준으로 파이프라인 작업을 실패할지 또는 계속할지 지정합니다.                                                                                                                                                                                                                                                                                                                            | Yes          | true          | boolean                                                                           |
| **Project name in Snyk** (projectName)                                                                   | snyk.io에서 만들 Snyk 프로젝트의 사용자 지정 이름입니다.                                                                                                                                                                                                                                                                                                                                        | No           | none          | string                                                                            |
| **Organization name (or ID) in Snyk** (organization)                                                     | Na이 프로젝트의 테스트 및 모니터링을 수행하는 Snyk 조직의 이름입니다.                                                                                                                                                                                                                                                                                                                                   | No           | none          | string                                                                            |
| **Test (Working) Directory** (testDirectory)                                                             | 대체 작업 디렉토리입니다. 예를 들어 저장소의 루트가 아닌 디렉토리에서 매니페스트 파일을 테스트하려면 해당 디렉토리에 대한 상대 경로를 입력합니다.                                                                                                                                                                                                                                                                                           | No           | none          | string                                                                            |
| <p><strong>Additional command-line args for Snyk CLI (advanced)</strong></p><p>(additionalArguments)</p> | <p>전달할 추가 Snyk CLI 인수입니다. 자세한 내용은 <a href="https://docs.snyk.io/snyk-cli/guides-for-our-cli/cli-reference">CLI reference</a>를 참조하십시오.</p><p><strong>Tip</strong>: 프로젝트를 찾지 못한 경우 <strong>--all-projects</strong>를 모범 사례로 추가합니다.(예: .NET의 경우).</p>                                                                                                                            | No           | none          | string                                                                            |

### **node.js (npm)**기반 애플리케이션을 테스트하는 Snyk 태스크의 예

이 섹션에는 Node.js(npm) 애플리케이션을 테스트할 때 Snyk Security Scan 작업 구성 및 파라미터의 예시가 표시됩니다.

구성 패널은 다음과 같이 나타납니다.

![Snyk Security Scan configuration panel](../../../.gitbook/assets/mceclip0-24-.png)

**add**를 클릭하면 다음과 같이 태스크가 파이프라인에 추가됩니다.

![Snyk Security Scan task added to a pipeline](../../../.gitbook/assets/mceclip1-15-.png)

### 애플리케이션 테스트의 간단한 예시

```
- task: SnykSecurityScan@0
  inputs:
    serviceConnectionEndpoint: 'snykToken'
    testType: 'app'
    monitorWhen: 'always'
    failOnIssues: true
```

### 컨테이너 이미지 파이프라인에 대한 Snyk 태스크 예제

다음은 컨테이너 이미지 파이프라인에 대한 스크립트 내의 Snyk Security Scan 태스크의 예입니다.

가장 일반적인 설정으로 채워지면 Azure의 구성 패널이 다음과 유사하게 나타납니다.

![](../../../.gitbook/assets/mceclip2-5-.png)

다음은 동일한 구성을 파이프라인에 추가한 경우의 예입니다.

![](../../../.gitbook/assets/mceclip3-1-.png)

### 컨테이너 이미지 테스트의 간단한 예제

```
- task: SnykSecurityScan@1
  inputs:
    serviceConnectionEndpoint: 'snykToken'
    testType: 'container'
    dockerImageName: 'goof'
    dockerfilePath: 'Dockerfile'
    monitorWhen: 'always'
    failOnIssues: true
```
