# 수정할 Snyk 패치

## 취약점을 수정하기 위한 Snyk 패치

### Snyk 오픈 소스 패치 시작하기

취약점을 해결할 수 있는 직접적인 업그레이드가 없거나 기능상의 이유로 업그레이드가 불가능한 경우가 있습니다(예: 주요 변경 사항).

이러한 경우 Snyk은 [패치로 코드를 보호](../../snyk-cli/secure-your-projects-in-the-long-term/protect-your-code-with-patches.md)하는 데 도움을 줄 수 있습니다. 이 옵션은 취약점을 수정하기 위해 로컬에 설치된 노드 모듈 파일을 최소한으로 수정합니다. 또한 snyk protect\_를 실행할 때 이 문제를 패치하도록 정책을 업데이트합니다.

{% hint style="info" %}
**주의**\
패치는 현재 **Node.js** 프로젝트에만 지원됩니다.
{% endhint %}

패치는 다음 시나리오에 적용할 수 있습니다.:

1. 직접 종속성에 사용할 수 있는 업그레이드가 없는 경우
2. 전이 종속성의 취약성 없는 버전에 도달하기 위해 직접 종속성을 업그레이드할 방법이 없을 때.
3. 업그레이드로 인해 패키지가 현재 코드베이스와 호환되지 않는 경우.

패치는 소스 코드 통합 및 Snyk CLI를 통해 사용할 수 있습니다.

### Snyk CLI를 사용할 때 패치는 어떻게 작동합니까?

Snyk Protect를 사용하여 패치를 적용하여 취약한 Node.js 프로젝트를 수정하면 다음과 같은 일이 발생합니다:

1. [`@snyk/protect`](https://www.npmjs.com/package/@snyk/protect)는 프로젝트의 프로덕션 종속성으로 추가됩니다.
2. npm install 또는 yarn install이 완료되면 `snyk-protect`를 실행하기 위해 postinstall 후크가 추가됩니다.

즉, npm install 또는 yarn install로 프로젝트 종속성을 설치할 때마다 후크가 `snyk-protect`를 트리거하여 필요한 종속성을 실행하고 패치할 수 있으며 완료되면 출력에 성공 메시지가 표시됩니다.

### `@snyk/protect`와 `snyk protect`의 차이점

이전에 Snyk는 snyk 보호 명령을 실행하기 위해 전체 [Snyk CLI `snyk` 패키지](https://www.npmjs.com/package/snyk)를 프로젝트 종속성에 추가했습니다. 패치 적용에 훨씬 더 가볍고 빠른 새로운 독립형 [패키지 `@snyk/protect`](https://github.com/snyk/snyk/tree/master/packages/snyk-protect#snykprotect)를 만들었습니다.

여전히 `snyk` 패키지를 사용하여 패치를 적용하는 경우 [README를 따르거나](https://github.com/snyk/snyk/tree/master/packages/snyk-protect#snykprotect) `npx @snyk/cli-protect-upgrade`를 사용하여 [마이그레이션 스크립트](https://www.npmjs.com/package/@snyk/cli-protect-upgrade)를 실행하여 `@snyk/protect`로 마이그레이션하는 것이 좋습니다.

### 소스 코드 통합을 사용할 때 패치는 어떻게 작동합니까?

패치를 사용하여 취약점을 수정하도록 선택하면 `@snyk/protect`가 종속성으로 추가되고 적용할 패치 목록이 포함된 `.snyk` 파일이 생성됩니다.

`.snyk` 파일에는 `node_modules`의 여러 위치에 나타날 수 있으므로 종속성에 대한 개별 경로별 패치 세부 정보가 포함됩니다. 예를 들면 다음과 같습니다.

```
# Snyk (https://snyk.io) policy file, patches or ignores known vulnerabilities.
version: v1.22.1
ignore: {}
# patches apply the minimum changes required to fix a vulnerability
patch:
  SNYK-JS-LODASH-567746:
    - tap > nyc > istanbul-lib-instrument > babel-types > lodash:
        patched: '2021-02-17T13:43:51.857Z'
```

그러나 `@snyk/protect`는 취약한 종속성의 모든 적용 가능한 인스턴스를 패치하려고 시도하므로 단일 경로만 필요합니다.
