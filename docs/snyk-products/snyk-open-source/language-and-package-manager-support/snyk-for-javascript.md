# JavaScript용 Snyk

Snyk을 사용하여 JavaScript 프로젝트를 스캔할 수 있습니다.

### 특징

{% hint style="info" %}
**NOTE**\
요금제에 따라서 해당 기능을 사용하지 못할 수 있습니다.
{% endhint %}

| Package managers / Features | <p>CLI</p><p>support</p> | <p>Git</p><p>support</p> | <p>License</p><p>scanning</p> | Fixing | <p>Runtime</p><p>monitoring</p> |
| --------------------------- | ------------------------ | ------------------------ | ----------------------------- | ------ | ------------------------------- |
| npm                         | ✔︎                       | ✔︎                       | ✔︎                            | ✔      | ✔︎                              |
| Yarn                        | ✔︎                       | ✔︎                       | ✔︎                            | ✔︎     | ✔︎                              |
| Yarn Workspaces             | ✔︎                       | ✔︎                       | ✔                             | ✖️     | ✔︎                              |

### 작동 방식

Snyk이 디펜던시 트리를 구축한 후 [취약점 데이터베이스](https://security.snyk.io)를 사용하여 해당 트리의 모든 패키지에서 취약점을 찾습니다.

{% hint style="info" %}
디펜던시를 스캔하려면 관련 패키지 매니저를 설치하고 프로젝트에 지원되는 매니페스트 파일이 포함되어 있는지 확인하십시오.
{% endhint %}

Snyk이 트리를 분석하고 구축하는 방식은 프로젝트의 언어와 패키지 매니저, 프로젝트 위치에 따라 다릅니다.

자세한 내용은 다음을 참조하십시오.

* [JavaScript 프로젝트에서 Snyk CLI 사용하기](snyk-for-javascript.md#javascript-snyk-cli)
* [JavaScript용 Git 설정](snyk-for-javascript.md#git-settings-for-javascript)

## JavaScript 프로젝트에서 Snyk CLI 사용하기

Snyk에서 트리를 분석하고 구축하는 방식은 프로젝트의 패키지 매니저에 따라 다릅니다.

### npm

Snyk CLI는 npm 6.x, 7.x를 지원합니다.

{% hint style="info" %}
Workspaces npm 7.x은 지원하지 않습니다.
{% endhint %}

구조화된 디펜던시 트리를 구축하기 위해 `package.json` 파일과 `package-lock.json` 파일을 분석합니다. 만약 `package-lock.json` 파일이 누락된 경우, `node_modules` 폴더를 분석합니다.

Snyk은 GNU 패치 유틸리티를 사용하여 이전에 선택한 패치를 적용할 수 있습니다. 패치는 .snyk 정책 파일에 저장됩니다.

**Peer dependencies**는 `peerDependenciesMeta`의 `package.json`파일에서 추가로 설정을 지정하지 않는 이상 npm 7.x에서 기본적으로 스캔됩니다. (npm 6.x에서는 기본적으로 설치가 되어있지 않아 `--peer-dependencies` 명령어 필요)

```
"peerDependenciesMeta": {
        "cache-manager": {
          "optional": true
        },
```

### Yarn

Snyk CLI에서는 Yarn 1, 2를 지원합니다.

구조화된 디펜던시 트리를 구축하기 위해 `package.json` 파일과 `yarn.lock` 파일을 분석합니다. 만약 `yarn.lock` 파일이 누락된 경우, `node_modules` 폴더를 분석합니다.

Snyk은 Yarn v2에서만 ~~_해결을_~~ 지원합니다. Yarn v1에 대해서는 ~~_해결을_~~ 지원하지 않습니다.

### Yarn workspaces

{% hint style="info" %}
Yarn v1 & 2 workspaces 지원은 현재 snyk test, snyk monitor 명령에만 해당됩니다.
{% endhint %}

Yarn workspaces의 경우 `--all-projects` 옵션을 사용하여 다른 프로젝트와 함께 패키지를 테스트 및 모니터링하거나 `--yarn-workspaces` 파라미터를 이용하여 yarn workspace의 프로젝트만 지정하여 스캔합니다. 모든 패키지를 스캔할 때 루트의 lockfile이 참조됩니다. 기본적으로 자동 검색되지 않는 하위 폴더를 찾으려면 `--detection-depth` 매개 변수를 사용합니다.

예제는 다음과 같습니다.\
`snyk test --all-projects --strict-out-of-sync=false --detection-depth=6` 스캔된 workspace에 속하는 패키지를 직접 스캔하고 하위 5개의 디렉토리를 검색하여 다른 프로젝트를 찾습니다.

`snyk test --yarn-workspaces --strict-out-of-sync=false --detection-depth=6` 검색된 workspace에 속하는 Yarn workspace 패키지만 스캔하고 하위 5개의 디렉토리를 검색합니다.

policy path를 제공하여 감지된 모든 workspace에 적용할 ignores/patches를 한 곳에서 관리하는 경우 **.snyk** 정책 파일을 사용할 수 있습니다.

`snyk test --all-projects --strict-out-of-sync=false --policy-path=src/.snyk`

### Lerna

{% hint style="info" %}
현재 Snyk은 Lerna를 지원하지 **않습니다**. 그러나 Lerna 프로젝트가 Yarn Workspaces를 사용하는 경우 표준 Yarn WorkSpaces 지원으로 프로젝트를 스캔할 수 있습니다. 다음 명령어를 통해 Snyk test/monitor를 실행하여 Snyk CLI 통합 차단을 해제할 수 있습니다.
{% endhint %}

각 예제 패키지에 대해 다음 명령어를 수행할 수 있습니다.

`snyk monitor --file=packages/example-package/package.json`

또는 중첩된 \``` package.json` ``파일 스캔을 자동화하는 스크립트를 지정할 수 있습니다.

`ls packages | xargs -I PKG_NAME snyk monitor --file=packages/PKG_NAME/package.json`

### JavaScript의 CLI 파라미터

#### 전제 조건

* 관련 패키지 매니저가 설치되어 있습니다.
* Snyk에서 지원하는 관련 매니페스트 파일을 포함합니다.
* [Snyk CLI](broken-reference)를 설치하고 인증하여 로컬 환경에서 프로젝트를 분석합니다.

JavaScript 프로젝트에 사용하는 패키지 매니저에 따라서 `npm install` 또는 `yarn install`을 실행합니다.

{% hint style="info" %}
snyk test는 로컬에 설치된 모듈을 확인하기 때문에 npm install 또는 yarn install 후에 실행해야 하며, shrinkwrap, npm enterprise 또는 가지고 있는 기타 사용자 지정 설치 로직과 원활하게 작동합니다.
{% endhint %}

**파라미터**

다음 옵션을 사용하여 스캔을 구체적으로 설정할 수 있습니다.

| **Option**                         | <p><strong>Values</strong><br><strong>(default in bold)</strong></p> | **Description**                                                                                                                                                                                                        |
| ---------------------------------- | -------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `--strict-out-of-sync`             | **true**, false                                                      | 동기화되지 않은 lockfile 테스트 방지(프로젝트에 동기화되지 않은 lockfile이 있는 경우 true로 설정하면 테스트 실패)                                                                                                                                             |
| `--fail-on`                        | **all**, upgradable, patchable                                       | <p>다음과 같은 취약점이 있는 경우 테스트가 실패합니다.</p><ul><li>all: 취약점이 포함된 모든 프로젝트</li><li>upgradable: 패키지 업그레이드로 수정할 수 있는 취약점이 포함된 프로젝트</li><li>patchable: 업그레이드 또는 패치로 수정할 수 있는 취약점이 포함된 프로젝트</li></ul>                               |
| `--prune-repeated-subdependencies` | true, **false**                                                      | 큰 프로젝트가 테스트에 실패한 경우 해당 옵션을 사용합니다. 기본 값은 false입니다.                                                                                                                                                                      |
| `--dev`                            | true, **false**                                                      | 개발용 디펜던시를 스캔해야 하는경우 true로 설정합니다.                                                                                                                                                                                       |
| `--yarn-workspaces`                | **n/a**                                                              | <p>lockfile이 root에 있는 Yarn workspace 프로젝트만 스캔하려면 이 옵션을 사용하십시오. 기본적으로 <code>--all-projects</code>으로 Yarn workspace 프로젝트를 자동으로 감지하고 스캔합니다.</p><p>Note: <code>snyk test</code> 및<code>snyk monitor</code> 명령에만 해당됩니다.</p> |
| `--all-projects`                   | **n/a**                                                              | <p>모든 노드 및 기타 프로젝트를 감지하고 스캔하려면 이 플래그를 사용하십시오.</p><p>Note: <code>snyk test</code> 및<code>snyk monitor</code> 명령에만 해당됩니다.</p>                                                                                            |

## JavaScript 프로젝트를 위한 Git services

JavaScript 프로젝트는 Snyk에서 지원하는 모든 Git services에서 가져올 수 있습니다. 가져오기 후 Snyk은 지원하는 매니페스트 파일을 기반으로 프로젝트를 분석합니다.

### npm

npm 6.x, 7.x은 Git Services에서 지원됩니다.

{% hint style="info" %}
Workspaces npm 7.x은 지원되지 않습니다.
{% endhint %}

다음 파일을 기반으로 디펜던시 트리를 빌드합니다.

* `package.json`
* `package-lock.json`

### Yarn

{% hint style="info" %}
Yarn versions 1은 Git Services에서 지원됩니다.
{% endhint %}

다음 파일을 기반으로 디펜던시 트리를 빌드합니다.

* `package.json`
* `yarn.lock`

### Yarn Workspaces

{% hint style="info" %}
**Note**\
Yarn Workspaces에 대한 Git 지원은 2021년 3월 3일 이후 생성된 조직의 모든 프로젝트에 대해 활성화됩니다. 해당 날짜 이전에 생성된 조직에 대해 이 기능을 활성화하려면 support@snyk.io에 문의하십시오. Yarn version 1은 Git Services에서 지원됩니다.
{% endhint %}

Yarn Workspaces의 경우 root의 `package.json` 파일과 root의 `yarn.lock`파일의 `packages` 패턴과 일치하는 `package.json`파일을 스캔합니다.

Fix Pull/Merge Requests는 Yarn Workspaces에 대해 지원되지 않습니다. 수정 조언을 사용하여 PR을 수동으로 생성할 수 있습니다.

commit 상태 확인은 항상 테스트 진행 시 root의 `yarn.lock` 파일과 workspace의 `package.json` 파일을 사용합니다.

{% hint style="info" %}
**Warning**\
귀하의 package.json 파일과 root의 yarn.lock 파일과 동기화되지 않은 경우 프로젝트를 다시 테스트하는 데 문제가 있습니다. Snyk은 이러한 일이 발생하면 프로젝트 페이지에 오류를 표시하고 로그를 가져옵니다.\
lockfile에 표시되지 않는 로컬로 설치된 패키지를 참조하는 경우 JavaScript용 **언어 설정** 페이지에서 **Require package.json and yarn.lock files to be in sync** 설정을 비활성화할 수 있습니다.
{% endhint %}

### JavaScript용 Git 설정

**기본 설정**

Snyk UI에서 다음의 파라미터를 사용하여 JavaScript 기반 프로젝트에 대한 언어 기본 설정을 정의할 수 있습니다.

| Option                                                                         | Description                                                                                                                                                                               |
| ------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Scan and fix devDependencies**                                               | Snyk은 package.json의 'devDependencies' 속성을 읽고 이에 따라 취약점을 보고하고 수정합니다.                                                                                                                       |
| **Require package.json and package-lock.json to be in sync**                   | package.json 및 package-lock.lock 파일이 동기화되지 않은 경우 선택하면 Snyk이 가져오기에 실패합니다.                                                                                                                  |
| **Exclude package-lock.json from being generated when fixing vulnerabilities** | 개인 mirror 또는 레지스트리를 사용하는 경우 Snyk이 npm 레지스트리를 사용하여 lockfile을 업데이트하기 때문에 Snyk에서 생성한 lockfile이 적합하지 않을 수 있습니다. 이 설정을 사용하여 fix pull requests / merge requests에서 lockfile이 생성되는 것을 제한할 수 있습니다. |

### 언어 기본 설정 업데이트

1. 계정에 로그인하고 관리하려는 관련 그룹 및 조직으로 이동합니다.
2. 설정 ![](../../../.gitbook/assets/cog\_icon.png) > **Languages**
3. **Edit settings**를 클릭하여 이 조직의 JavaScript(npm 및 Yarn) 프로젝트에 대한 기본 설정을 구성합니다.
