# Snyk for JavaScript

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

### How it works

Snyk이 디펜던시 트리를 구축한 후 [vulnerability database](https://snyk.io/vuln)를 사용하여 해당 트리의 모든 패키지에서 취약점을 찾습니다.

{% hint style="info" %}
디펜던시를 스캔하려면 관련 패키지 매니저를 설치하고 프로젝트에 지원되는 매니페스트 파일이 포함 되어있는지 확인하세요.
{% endhint %}

Snyk이 트리를 분석하고 구축하는 방식은 프로젝트의 언어와 패키지 매니저, 프로젝트 위치에 따라 다릅니다.

자세한 내용은 다음을 참조하세요.

* [Snyk CLI tool for JavaScript projects](snyk-for-javascript.md)
* [Git services for JavaScript projects](snyk-for-javascript.md)

## JavaScript 프로젝트에서 Snyk CLI 사용하기

Snyk에서 트리를 분석하고 구축하는 방식은 프로젝트의 패키지 매니저에 따라 다릅니다.

### npm

Snyk CLI는 npm 6.x, 7.x를 지원합니다.

{% hint style="info" %}
Workspaces npm 7.x은 지원하지 않습니다.
{% endhint %}

구조화된 디펜던시 트리를 구축하기 위해 `package.json` 파일과 `package-lock.json` 파일을 분석합니다. 만약 `package-lock.json` 파일이 누락된 경우, `node_modules` 폴더를 분석합니다.

Snyk은 GNU 패치 유틸리티를 사용하여 이전에 선택한 패치를 적용할 수 있습니다. 패치는 Snyk 정책 파일에 저장됩니다.

**Peer dependencies**는 `peerDependenciesMeta`의 `package.json`파일에서 추가로 설정을 지정하지 않는 이상 npm 7.x에서 기본적으로 검색됩니다 (npm 6.x에서는 기본적으로 설치가 되어있지 않아 해당 명령어 필요 `--peer-dependencies`).

```
"peerDependenciesMeta": {
        "cache-manager": {
          "optional": true
        },
```

### Yarn

Snyk CLI에서는 Yarn 1, 2를 지원합니다.

구조화된 디펜던시 트리를 구축하기 위해 `package.json` 파일과 `yarn.lock` 파일을 분석합니다. 만약 `yarn.lock` 파일이 누락된 경우, `node_modules` 폴더를 분석합니다.

Snyk은 Yarn v2에서만 지원을합니다. Yarn v1에 대해서는 지원하지 않습니다.

### Yarn workspaces

{% hint style="info" %}
Yarn v1 & 2 workspaces 지원은 현재 snyk test, snyk monitor 명령에만 해당됩니다.
{% endhint %}

Yarn workspaces의 경우 `--all-projects` 플래그를 사용하여 다른 프로젝트와 함께 패키지를 테스트 및 모니터링하거나 `--yarn-workspaces` 파라미터를 이용하여 yarn workspace의 프로젝트만 지정하여 스캔합니다. 모든 패키지를 스캔할 때 root lockfile이 참조됩니다. `--detection-depth` 파라미터를 사용하여 기본적으로 검색되지 않는 하위 폴더를 찾을 수 있습니다.

Example usage:\
`snyk test --all-projects --strict-out-of-sync=false --detection-depth=6`          검색된 작업 공간에 속하는 패키지를 직접 스캔하고 하위 5개의 티렉토리를 검색하여 다른 프로젝트를 찾습니다.

`snyk test --yarn-workspaces --strict-out-of-sync=false --detection-depth=6`    검색된 작업 공간에 속하는 Yarn workspace 패키지만 스캔하고 하위 5개의 티렉토리를 검색합니다.

policy path를 제공하여 감지된 모든 작업 공간에 적용할 ignores/patches를 한 곳에서 관리하는 경우 **.snyk** 정책 파일을 사용할 수 있습니다.

`snyk test --all-projects --strict-out-of-sync=false --policy-path=src/.snyk`

### Lerna

{% hint style="info" %}
현재 Snyk은 Lerna를 지원하지 **않습니다**. **** 그러나 Lerna 프로젝트가 Yarn Workspaces를 사용하는 경우 표준 Yarn WorkSpaces 지원으로 프로젝트를 스캔할 수 있습니다. 다음 명령어를 통해 Snyk test/monitor를 실행하여 Snyk CLI 통합 차단을 해제할 수 있습니다.
{% endhint %}

각 예제 패키지에 대해 다음 명령어를 수행할 수 있습니다.

`snyk monitor --file=packages/example-package/package.json`

또는 중첩된 \``` package.json` ``파일 스캔을 자동화하는 스크립트를 지정할 수 있습니다.

`ls packages | xargs -I PKG_NAME snyk monitor --file=packages/PKG_NAME/package.json`

### JavaScript의 CLI 파라미터

전제 조건

* 관련 패키지 매니저가 설치되어 있습니다.
* Snyk에서 지원하는 관련 매니페스트 파일을 포함합니다.
* [Snyk CLI](../../../features/snyk-cli/install-the-snyk-cli/)를 설치하고 인증하여 로컬 환경에서 프로젝트를 분석합니다.

JavaScript 프로젝트에 사용하는 패키지 매니저에 따라서 `npm install` 또는 `yarn install,`을 실행합니다.

{% hint style="info" %}
snyk test는 로컬에 설치된 모듈을 확인하기 때문에 npm install 또는 yarn install 후에 실행해야 하며, shrinkwrap, npm enterprise 또는 가지고 있는 기타 사용자 지정 설치 논리와 원할하게 작동합니다.
{% endhint %}

**Parameters**

다음 옵션을 사용하여 스캔을 구체적으로 설정할 수 있습니다.

| **Option**                         | <p><strong>Values</strong><br><strong>(default in bold)</strong></p> | **Description**                                                                                                                                                                                                        |
| ---------------------------------- | -------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `--strict-out-of-sync`             | **true**,false                                                       | 동기화되지 않은 잠금 파일 테스트 방지(프로젝트에 동기화되지 않은 잠금 파일이 있는 경우 true로 설정하면 테스트 실패)                                                                                                                                                   |
| `--fail-on`                        | **all**, upgradable, patchable                                       | <p>다음과 같은 취약점이 있는 경우 테스트가 실패합니다.</p><ul><li>all: 취약점이 포함된 모든 프로젝트</li><li>upgradable: 패키지 업그레이드로 수정할 수 있는 취약점이 포함된 프로젝트</li><li>patchable: 업그레이드 또는 패치로 수정할 수 있는 취약점이 포함된 프로젝트</li></ul>                               |
| `--prune-repeated-subdependencies` | true, **false**                                                      | 큰 프로젝트가 테스트에 실패한 경우 해당 플래그를 사용합니다. 기본 값은 false입니다.                                                                                                                                                                     |
| `--dev`                            | true, **false**                                                      | 개발용 디펜던시를 스캔해야 하는경우 true로 설정합니다.                                                                                                                                                                                       |
| `--yarn-workspaces`                | **n/a**                                                              | <p>lockfile이 root에 있는 Yarn workspace 프로젝트만 스캔하려면 이 플래그를 사용하세요. 기본적으로 <code>--all-projects</code>으로 Yarn workspace 프로젝트를 자동으로 감지하고 스캔합니다.</p><p>Note: <code>snyk test</code> 및<code>snyk monitor</code> 명령에만 해당됩니다.</p> |
| `--all-projects`                   | **n/a**                                                              | <p>모든 노드 및 기타 프로젝트를 감지하고 스캔하려면 이 플래그를 사용하세요.</p><p>Note: <code>snyk test</code> 및<code>snyk monitor</code> 명령에만 해당됩니다.</p>                                                                                             |

## JavaScript 프로젝트를 위한 Git services

JavaScript 프로젝트는 Snyk에서 지원하는 모든 GIt services에서 가져올 수 있습니다. 가져오기 후 Snyk은 지원하는 매니페스트 파일을 기반으로 프로젝트를 분석합니다.

### npm

Git services에서 는 npm 6.x, 7.x를 지원합니다.GIt Services는 npm 6.x, 7.x를 지원합니다.

{% hint style="info" %}
Workspaces npm 7.x is not supported.
{% endhint %}

We build the dependency tree based on these files:

* `package.json`
* `package-lock.json`

### Yarn

{% hint style="info" %}
Yarn versions 1 & 2 are supported in Git services.
{% endhint %}

We build the dependency tree based on these files:

* `package.json`
* `yarn.lock`

### Yarn Workspaces

{% hint style="info" %}
**Note**\
Git support for Yarn Workspaces is enabled for all projects in organisations created after March 3rd 2021. To enable this feature for organisations created before this date please contact support@snyk.io. Yarn version 1 is supported in Git services.
{% endhint %}

For Yarn Workspaces we scan each `package.json` that matches the `packages` pattern from the root level `package.json` and root level `yarn.lock`

Fix Pull/Merge Requests are not supported for Yarn Workspaces. The fix advice can be used to manually generate PRs.

Commit status checks always use the root level `yarn.lock` and workspace `package.json` for tests.

{% hint style="info" %}
**Warning**\
If your `package.json` and root `yarn.lock` are out-of-sync, we will have issues re-testing the projects. Snyk shows errors on project page and import logs when this happens.\
If you reference the locally installed packages which do not appear in a lockfile, you can disable the **Require package.json and yarn.lock files to be in sync** setting, on the **Languages Settings** page for JavaScript.
{% endhint %}

### Git settings for JavaScript

**Preferences**

From the Snyk UI, use these parameters to customize your language preferences for JavaScript-based projects:

| Option                                                                         | Description                                                                                                                                                                                                                                                                                |
| ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Scan and fix devDependencies**                                               | If selected, Snyk reads the \`devDependencies\` property on the package.json and reports & fixes any vulnerabilities accordingly.                                                                                                                                                          |
| **Require package.json and package-lock.json to be in sync**                   | When selected if the package.json and package.lock files are out-of-sync, Snyk fails the import.                                                                                                                                                                                           |
| **Exclude package-lock.json from being generated when fixing vulnerabilities** | If you are using private mirrors or registries, a Snyk generated lockfile might not be appropriate for you because Snyk uses the npm registry to update the lockfile. This setting allows you to opt-out of getting lockfiles generated for you in our fix pull requests / merge requests. |

### Update language preferences

1. Log in to your account and navigate to the relevant group and organization that you want to manage
2. Click on settings ![](../../../.gitbook/assets/cog\_icon.png) > **Languages**
3. Click **Edit settings** for JavaScript to configure preferences for your JavaScript (npm and Yarn) projects in this organization
