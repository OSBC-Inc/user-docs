# .NET용 Snyk

Snyk은 CLI 및 애플리케이션 UI(app.snyk.io)를 통해 취약점에 대한 보안 스캔을 제공합니다.

이 문서는 Snyk을 사용하여 .NET 프로젝트를 스캔하는 방법을 제공합니다.

{% hint style="info" %}
**Note**\
요금제에 따라 기능을 사용하지 못할 수 있습니다.
{% endhint %}

| Package managers / Features                            | CLI support | Git support | License scanning | Fixing | Runtime monitoring |
| ------------------------------------------------------ | ----------- | ----------- | ---------------- | ------ | ------------------ |
| [NuGet](https://www.nuget.org)                         | ✔︎          | ✔︎          | ✔︎               | ✔︎     |                    |
| [Paket](https://fsprojects.github.io/Paket/index.html) | ✔︎          |             |                  |        |                    |

## 작동 방식

트리를 구축한 후에는 [취약점 데이터베이스](https://security.snyk.io)를 사용하여 디펜던시 트리의 모든 패키지에서 취약점을 찾을 수 있습니다.

{% hint style="info" %}
**Note**\
디펜던시를 스캔하려면 먼저 관련 패키지 매니저를 설치했는지, 프로젝트에 지원되는 매니페스트 파일이 포함되어 있는지 확인해야 합니다.
{% endhint %}

Snyk이 트리를 분석하고 빌드하는 방법은 프로젝트의 언어 및 패키지 매니저와 프로젝트 위치에 따라 다릅니다. 자세한 내용은 다음을 참조하십시오.

* [.NET 프로젝트에서 Snyk CLI 사용하기](snyk-for-.net.md#.net-snyk-cli)
* [.NET 프로젝트를 위한 Git Services](snyk-for-.net.md#.net-git-services)

## .NET 프로젝트에서 Snyk CLI 사용하기

### Nuget

#### PackageReference에서 관리하는 디펜던시

우선 `dotnet restore`를 실행하여 .NET 프로젝트의 디펜던시를 복원하고 `snyk test`를 실행하여 **obj/project.assets.json**이 생성되었는지 확인합니다. 빌드 프로젝트에 대한 자세한 내용은 [CLI 시작하기](../../../features/snyk-cli/getting-started-with-the-cli/)를 참조하십시오.

**project.assets.json**으로 지원되는 프로젝트 파일의 예는 다음과 같습니다.

* \*.csproj
* \*.vbproj
* \*.fsproj

**Note:** 프로젝트 파일을 [lockfile](https://docs.microsoft.com/en-us/nuget/consume-packages/package-references-in-project-files#locking-dependencies)과 결합하여 **project.assets.json** 파일을 확인할 수 있습니다.

**packages.config에서 관리하는 디펜던시**

**packages.config**에서 관리하는 디펜던시에 대해 두 가지 접근 방식이 있지만 다음 방식은 가장 정확한 결과를 얻을 수 있어 권장되는 접근 방식입니다.

먼저 `nuget install -OutputDirectory packages`를 실행하여 **packages** 폴더에 디펜던시를 설치하고 `snyk test`를 실행하여 **packages** 디렉토리를 생성했는지 확인합니다.

**packages**에 포함하는 프로젝트 파일은 다음과 같습니다.

* packages.config

**Note:** 이전에 디펜던시를 설치하지 않고 `snyk test`를 실행할 수 있어야 하지만 이로 인해 취약점 결과의 정확도가 떨어집니다.

#### **CLI** 파라미터

이 섹션에서는 Nuget 프로젝트로 작업할 때 사용할 수 있는 CLI 옵션에 대해 설명합니다.

| Option                   | Description                                                                                                                                                                                                                                                                              |
| ------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `--file=.sln`            | 주어진 `.sln` 파일에 포함된 모든 .NET 프로젝트를 테스트합니다. 예: `snyk test --file=myApp.sln`                                                                                                                                                                                                                 |
| `--file=packages.config` | 개별 .NET 프로젝트를 테스트합니다.                                                                                                                                                                                                                                                                    |
| `--packages-folder`      | `packages.config`를 사용하는 경우 디펜던시가 설치된 폴더입니다. 이 폴더에 고유한 이름을 할당한 경우 사용자 정의 경로를 입력해야만 해당 이름을 찾을 수 있습니다. 디펜던시가 있는 폴더 이름을 포함하여 절대 경로 또는 상대 경로를 사용하십시오. 예: `snyk test --packages-folder=../location/to/packages` for Unix OS `snyk test --packages-folder=..\location\to\packages` for Windows. |
| `--assets-project-name`  | Nuget을 사용하여 .NET 프로젝트를 모니터링할 때 `PackageReference`키는 project.assets.json에 표시된 프로젝트 이름을 사용합니다.                                                                                                                                                                                             |

### Paket

#### Paket이 관리하는 디펜던시

Paket을 사용하여 `snyk test`를 실행하려면 **paket.lock** 파일과 **paket.dependencies** 파일이 함께 필요합니다.&#x20;

기타 지원에는 **project.json**(더 이상 권장하지 않음, [Microsoft 설명서](https://docs.microsoft.com/en-us/nuget/archive/project-json) 참조) 파일이 포함됩니다.

디펜던시 트리를 구축하기 위해 Snyk은 **paket.dependencies** 및 **paket.lock** 파일을 분석합니다.

## .NET 프로젝트를 위한 Git Services

.NET 프로젝트는 Snyk이 지원하는 모든 Git Services에서 가져올 수 있습니다.

가져오기가 완료되면 Snyk은 지원되는 매니페스트 파일을 기반으로 프로젝트를 분석한 다음 디펜던시 트리를 빌드하고 다음과 같이 앱에 표시합니다.

![](../../../.gitbook/assets/uuid-c995621c-85c8-c79f-accd-f014e2293921-en.png)

### **Nuget**

가져올 프로젝트를 선택하면 다음 매니페스트 파일을 기반으로 디펜던시 트리를 빌드합니다.

* .NET Core의 경우 **\*.proj** 파일
* .NET Framework의 경우 **\*.proj** 파일 및 **packages.config** 파일

지원하는 프로젝트 파일은 다음과 같습니다.

* \*.csproj
* \*.vbproj
* \*.fsproj

.NET 프로젝트는 여러 프레임워크를 대상으로 할 수 있습니다. Snyk은 각 프레임워크에 대해 별도의 디펜던시 트리를 생성하여 인터페이스에서 별도의 Snyk 프로젝트로 표시합니다. 이러한 방식으로 디펜던시가 사용되는 이유를 이해하고 수정하기 쉬워집니다.

### **Paket**

현재 가져오기 지원이 없습니다.

### .NET용 Git 설정

Snyk UI에서 Snyk이 빌드 디펜던시를 포함하여 전체 프로젝트를 스캔해야 하는지 또는 빌드 디펜던시를 건너뛸지 구성할 수 있습니다.

***

**언어 기본 설정 업데이트**

1. 계정에 로그인하고 관리하려는 관련 그룹 및 조직으로 이동합니다.
2.  설정 ![](../../../.gitbook/assets/cog\_icon.png) > .NET을 클릭합니다.

    Scan build dependencies를 선택하면 Snyk이 모든 개발 디펜던시를 스캔합니다.

## 취약점 수정

Snyk이 프로젝트 내에서 오픈 소스 취약점을 수정하는 데 어떻게 도움이 되는지에 대한 자세한 내용은 [취약점 수정](../../../features/fixing-and-prioritizing-issues/issue-management/remediate-your-vulnerabilities.md)을 참조하십시오.

{% hint style="info" %}
PR 수정 기능은 [SCM](../../../getting-started/scm-git-and-ci-cd-integration-deployment-intro.md) 통합 전체에서만 사용할 수 있습니다.
{% endhint %}

### Fix PR이 지원되는 매니페스트 파일

현재 Nuget을 사용하여 프로젝트 디펜던시를 관리하고 [`PackageReference`](https://docs.microsoft.com/en-us/nuget/consume-packages/package-references-in-project-files) 또는 [`packages.config`](https://docs.microsoft.com/en-us/nuget/reference/packages-config)를 활용하는 경우 실제 수정사항이 있을 때 매니페스트 파일의 디펜던시 버전을 자동으로 업데이트할 수 있습니다. 이러한 방식으로 수정 사항을 쉽게 검토하고 merge할 수 있습니다.

### 디펜던시 분석

.NET 에코시스템에서는 여러 단계의 디펜던시가 존재하며 일부는 정확하게 나타나지만 일부는 개발자에게 완전히 숨겨져 있습니다. 주어진 .NET 애플리케이션의 취약점을 올바르게 식별하려면 이러한 디펜던시를 정확하게 해결해야 합니다.

Snyk CLI와 Github와 같은 소스 코드 관리(SCM) 시스템에서 디펜던시를 다르게 해결합니다.

* CLI에서 `PackageReference`를 사용하여 프로젝트 디펜던시를 관리하는 경우 `obj/project.assets.json` 파일을 스캔합니다. 만약, `packages.config` 파일을 사용하여 디펜던시를 관리하는경우 `package` 디렉토리를 스캔합니다. 이 접근 방식을 사용하면 매우 정확할 수 있습니다.
*   SCM 통합에서 위에서 언급한 생성된 파일을 사용할 수 없기 때문에 스캔은 다른 프로세스를 사용합니다. 이를 극복하기 위해서 NuGet 디펜던시를 따라 [resolution algorithm](https://docs.microsoft.com/en-us/nuget/concepts/dependency-resolution) 디펜던시 트리를 구성합니다.

    **Note**: 런타임 디펜던시("메타 패키지"라고 하는 런타임 환경에서 제공)는 호스트 시스템이 앱을 실행하는 서버와 유사한 런타임 SDK를 사용하는 경우 CLI에서 더 정확하게 해결됩니다.

.NET 자동 수정에 대한 자세한 내용은 [블로그](https://snyk.io/blog/automated-vulnerability-fixes-dot-net-dependencies/)를 참조하십시오.

#### Build-time vs Runtime dependencies

* **Build-time dependency**: 빌드 시간 동안 해결되고 런타임 시 변경할 수 없는 디펜던시로 이해합니다.
* **Runtime dependency**: 설치된 런타임에 대해 해결되어야 하는 런타임 디펜던시를 이해합니다. 예를 들어, .NET framework(<=4)에서 오는 packages / [`System.Net.Http`](https://www.nuget.org/packages/System.Net.Http)에서 찾는 .NET [runtime](https://docs.microsoft.com/en-us/dotnet/core/versions/selection?WT.mc\_id=DOP-MVP-5001511&)(Core 및 .NET5+). 런타임 디펜던시를 meta-packages라고 부르기도 합니다.

### Runtime dependencies를 이용한 취약점 해결

이러한 유형의 취약한 디펜던시를 해결하기 위해 선택할 수 있는 조치가 있습니다. SCM 또는 CLI를 사용하는 경우 다음과 같이 진행합니다.

**SCM**

응용 프로그램이 항상 Microsoft의 최신 패치가 설치된 시스템에서 실행하여 발견된 취약점은 더 이상 프로젝트와 관련이 없을 수 있으므로 이를 [무시하도록 선택](../../../features/fixing-and-prioritizing-issues/issue-management/ignore-issues.md)할 수 있습니다.

**CLI**

애플리케이션이 운영 환경에서 실행될 때 Microsoft에서 항상 최신/명시적 패치를 가져오기 때문에 취약점이 발견되었다고 생각되면 다음을 수행할 수 있습니다.

* 프로덕션 환경에서 애플리케이션이 항상 최신 SDK 패치 버전에서 실행된다면 프로젝트 파일에서 `TargetLatestRuntimePatch`를 `true`로 설정할 수 있습니다. 또한 환경(예: dev, prod)을 최신 런타임 버전으로 업그레이드해야 합니다.

```
<TargetLatestRuntimePatch>true</TargetLatestRuntimePatch>
```

* 런타임이 포함된 [독립형](https://docs.microsoft.com/en-us/dotnet/core/deploying/#publish-self-contained) 앱을 게시하도록 선택할 수 있습니다. 그런 다음 `RuntimeFrameworkVersion`을 프로젝트 파일의 특정 패치 버전으로 설정하십시오. 더 이상 관련이 없다고 생각되는 취약점을 [무시하도록 선택](../../../features/snyk-cli/fix-vulnerabilities-from-the-cli/ignore-vulnerabilities-using-snyk-cli.md)할 수 있습니다.

```
<PropertyGroup>
  <RuntimeFrameworkVersion>5.0.7</RuntimeFrameworkVersion>
</PropertyGroup>
```

## 지원하지 않는 경우

* [`Directory.Build.props`](https://docs.microsoft.com/en-us/visualstudio/msbuild/customize-your-build?view=vs-2022#directorybuildprops-and-directorybuildtargets) 와 [`Directory.Build.targets`](https://docs.microsoft.com/en-us/visualstudio/msbuild/customize-your-build?view=vs-2022#directorybuildprops-and-directorybuildtargets)는 현재 지원하지 않습니다.
* `<ProjectReference>`는 현재 지원하지 않습니다.
* Private dependency 스캔은 SCM 통합을 통해 지원하지 않습니다. Snyk CLI를 사용하여 스캔할 수 있습니다.
