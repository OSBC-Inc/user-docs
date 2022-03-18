# Swift 및 Objective-C (CocoaPods)용 Snyk

Snyk은 CLI 및 애플리케이션 UI(app.snyk.io)를 통해 취약점에 대한 보안 스캔을 제공합니다.

이 문서는 Snyk을 사용하여 CocoaPods 프로젝트를 스캔하는 방법을 제공합니다.

### 특징

{% hint style="info" %}
요금제에 따라서 기능을 사용하지 못할 수 있습니다.
{% endhint %}

| Package managers / Features | CLI support | Git support | License scanning | Fixing | Runtime monitoring |
| --------------------------- | ----------- | ----------- | ---------------- | ------ | ------------------ |
| Cocoapods                   | ✔︎          | ✔︎          | ✔︎               |        |                    |

### 작동 방식

트리를 구축한 후에는 [취약점 데이터베이스](https://security.snyk.io)를 사용하여 디펜던시 트리의 모든 패키지에서 취약점을 찾을 수 있습니다.

{% hint style="info" %}
**Note**\
디펜던시를 스캔하려면 먼저 관련 패키지 매니저를 설치했는지, 프로젝트에 지원되는 매니페스트 파일이 포함되어 있는지 확인해야 합니다.
{% endhint %}

Snyk이 트리를 분석하고 빌드하는 방법은 프로젝트의 언어 및 패키지 매니저와 프로젝트 위치에 따라 다릅니다.

### CocoaPods 프로젝트에서 Snyk CLI 사용하기

Snyk은 CocoaPods 프로젝트를 스캔하고 Podfile 및 Podfile.lock 파일을 검사합니다. 이후 프로젝트의 모든 직접적이고 심층적인 디펜던시의 특정 버전을 취약점 데이터베이스와 비교하여 그에 따라 프로젝트 디펜던시 트리를 구축합니다.

### **CLI parameters for Swift and Objective-C**

#### 전제 조건

* Snyk CLI를 사용하기 전에 관련 패키지 매니저를 설치하십시오.
* 테스트 진행 이전에 Snyk에서 지원하는 관련 매니페스트 파일을 포함합니다.
* [Snyk CLI](../../../features/snyk-cli/install-the-snyk-cli/)를 설치하고 인증하여 로컬 환경에서 프로젝트 분석을 시작합니다.

#### **Parameters**

CLI 에서 Swift 및 Objective-C 프로젝트로 작업할 때 다음과 같이 동기화되지 않은 lockfile 테스트를 방지할 수 있습니다.

| Option                  | Description                                     |
| ----------------------- | ----------------------------------------------- |
| `--strict-out-of-sync=` | 동기화되지 않은 lockfile 테스트를 방지합니다. 기본값은 **true**입니다. |

### CocoaPods 프로젝트를 위한 Git Servicess

CocoaPods 프로젝트를 스캔하고 Podfile 및 Podfile.lock 파일을 검사합니다. 이후 프로젝트의 모든 직접적이고 심층적인 디펜던시의 특정 버전을 취약점 데이터베이스와 비교하여 그에 따라 프로젝트 디펜던시 트리를 구축합니다.

**Git services**

CocoaPods에서 관리하는 Swift 및 Objective-C 프로젝트는 Snyk이 지원하는 모든 Git 저장소에서 가져올 수 있습니다. 프로젝트를 테스트하기 위해 Podfile 및 Podfile.lock 파일을 분석합니다.
