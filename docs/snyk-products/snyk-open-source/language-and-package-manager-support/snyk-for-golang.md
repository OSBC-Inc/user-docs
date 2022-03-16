# Snyk for Golang

Snyk은 [Go Modules](https://golang.org/ref/mod), [dep](https://github.com/golang/dep) 그리고 [govendor](https://github.com/kardianos/govendor)가 관리하는 Go 프로젝트의 테스트 및 모니터링을 지원합니다.

이 문서는 Snyk을 이용하여 Go 프로젝트를 스캔하는 방법을 제공합니다.

### 특징 <a href="#h_01esm3gfnmn0f7art59aek97tm" id="h_01esm3gfnmn0f7art59aek97tm"></a>

{% hint style="info" %}
**Note**\
요금제에 따라서 기능을 사용하지 못할 수 있습니다.
{% endhint %}

| Package managers / Features                       | CLI support | Git support | License scanning | Fixing | Runtime monitoring |
| ------------------------------------------------- | ----------- | ----------- | ---------------- | ------ | ------------------ |
| [Go Modules](https://golang.org/ref/mod)          | ✔︎          | ✔︎          | ✔︎               |        |                    |
| [dep](https://github.com/golang/dep)              | ✔︎          | ✔︎          | ✔︎               |        |                    |
| [govendor](https://github.com/kardianos/govendor) | ✔︎          | ✔︎          | ✔︎               |        |                    |

## **How it works**

트리를 구축한 후에는 [vulnerability database](https://snyk.io/vuln)를 사용하여 디펜던시 트리의 모든 패키지에서 취약점을 찾을 수 있습니다.

{% hint style="info" %}
**Note**\
CLI에서 디펜던시를 스캔하려면 먼저 관련 패키지 매니저를 설치했는지, 프로젝트에 지원되는 매니페스트 파일이 포함되어 있는지 확인해야 합니다.
{% endhint %}

Snyk이 트리를 분석하고 빌드하는 방법은 프로젝트의 언어 및 패키지 매니저와 프로젝트 위치에 따라 다릅니다.

## Go 프로젝트에서 Snyk CLI 사용하기

**Go Modules**

디펜던시 트리를 구축하기 위해 Snyk은 `go list -sjon -deps` 명령어를 사용합니다.

{% hint style="info" %}
**Note**\
Snyk은 프로젝트 소스코드에 대한 전체 액세스 권한이 있으므로 모듈 단계가 아닌 패키지 단계에서 Go Modules 프로젝트를 검색합니다.

취약한 모듈을 사용할 수 있지만 취약한 패키지는 사용할 수 없기 때문에 유용하게 사용할 수 있습니다.
{% endhint %}

Go Modules 프로젝트를 테스트하는 경우 디펜던시를 설치할 필요가 없지만 프로젝트의 root에 `go.mod` 파일이 있어야 할 경우 `go list`는 이 파일과 프로젝트 소스 코드를 사용하여 완전한 디펜던시 트리를 빌드합니다.

{% hint style="info" %}
**Note**\
Go 버전은 **Go list -json -deps** 명령에 대해 다른 결과를 생성합니다. 이 문제는 디펜던시 트리와 Snyk CLI가 찾을 취약점에 영향을 미칠 수 있습니다.
{% endhint %}

**Dep**

디펜던시 트리를 구축하기 위해 Snyk은 `Gopkg.lock` 파일을 분석합니다.

Snyk CLI를 통해 dep 프로젝트를 테스트하려면 디펜던시를 설치해야 하는 경우 `dep ensure`명령어를 실행하십시오.

**Govendor**

디펜던시 트리를 구축하기 위해 Snyk은 `vendor/vendor.json` 파일을 분석합니다.

Snyk CLI를 통해 Govendor 프로젝트를 테스트할 때 디펜던시를 설치해야 하는 경우 `govendor sync`명령어를 실행하십시오.

## Go 프로젝트를 위한 Git Services

### **Go Modules**

{% hint style="info" %}
**Note**\
Git을 통해 가져온 Go Modules 프로젝트의 경우 프로젝트 소스코드에 대한 전체 액세스 권한이 없기 때문에 디펜던시는 패키지 단계가 아닌 모듈 단계에서 해결됩니다.

즉, 소스코드에서 참조된 패키지뿐만아니라 각 모듈에 대한 모든 취약점을 보고하므로 CLI에서 테스트한 프로젝트보다 더 많은 문제(잠재적 오탐지 포함)가 보고될 수 있습니다.
{% endhint %}

디펜던시 트리를 구축하기 위해 Snyk는 선택한 리포지토리의 `go.mod` 파일을 사용하여 `go mod graph` 명령어을 실행합니다.

**Private modules**

Private Git 저장소의 모듈에 의존하는 Go Modules 프로젝트는 private 저장소가 main 프로젝트 저장소와 동일한 Git 조직에 있는 경우에 지원됩니다.

다른 Git 조직의 저장소에서 개인 모듈이 있는 프로젝트 가져오기는 실패할 것입니다. 다른 Git 조직들의 private 모듈 의존성에 대한 지원은 향후 계획되어 있습니다.

Private modules은 GitHub 및 Bitbucket Cloud에서 지원됩니다. GitLab 및 Bitbucket Server는 현재 지원되지 않습니다.

**Broker**

새로운 [Snyk Broker](https://docs.snyk.io/integrations/snyk-broker/broker-introduction) 클라이언트를 통해 가져온 프로젝트는 예상대로 작동합니다.

2020년 12월 30일 이전에 생성된 기존 클라이언트에 지원을 추가하려면 [pull request](https://github.com/snyk/broker/pull/299/files) 변경 사항에 따라 `go.mod` 및 `go.sum`을 `accept.json`파일에 추가해야 합니다.

브로커를 통해 통합된 개인 Go Modules(저장소)을 사용하는 경우 각 개인 모듈에 `Go.mod` 파일이 정의되어 있어야 합니다.

**Dep**

디펜던시 트리를 구축하기 위해 Snyk은 선택한 저장소의 `Gopkg.lock`파일을 분석합니다.

**Govendor**

디펜던시 트리를 구축하기 위헤 Snyk 은 선택한 저장소의 `vendor/vendor.json`파일을 분석합니다.
