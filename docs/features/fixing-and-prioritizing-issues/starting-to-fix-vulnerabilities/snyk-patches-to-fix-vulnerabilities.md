# 취약성을 수정하기 위한 Snyk 패치

### Snyk Open Source 시작하기: 패치

때때로 취약점을 해결할 수 있는 직접적인 업그레이드가 없거나 기능상의 이유로 업그레이드가 불가능합니다.(예: 중대한 변경 사항)

이러한 경우 Snyk은 [패치를 사용하여 코드를 보호](https://docs.snyk.io/snyk-cli/secure-your-projects-in-the-long-term/protect-your-code-with-patches)할 수 있습니다. 이 옵션은 로컬로 설치된 `node_modules` 파일을 최소로 수정하여 취약점을 수정합니다. 또한 [snyk protect](https://snyk.io/docs/using-snyk#protect)를 실행할 때 Issue를 패치하도록 정책을 업데이트합니다.

{% hint style="info" %}
**Caution**\
패치는 현재 **Node.js** 프로젝트에만 지원됩니다.
{% endhint %}

패치는 다음과 같은 시나리오에 적용할 수 있습니다.

1. 직접 의존성에 사용할 수 있는 업그레이드가 없는 경우
2. 간접 의존성의 취약점이 없는 버전에 도달하기 위해 직접 의존성을 업그레이드할 방법이 없는 경우
3. 업그레이드로 인해 패키지가 현재 코드베이스와 호환되지 않는 경우

패치는 소스 코드 통합 및 [Snyk CLI](https://support.snyk.io/hc/en-us/articles/360003812578-Our-full-CLI-reference)를 통해 사용할 수 있습니다.&#x20;

## Snyk Open Source: 시작하기: 패치 생성 프로세스

패치는 Snyk에서 생성하고 유지 관리합니다. 패키지 소유자가 Issue를 수정하기 위해 코드를 변경한 경우 패치는 이 공식 수정 사항을 기반으로 하며 외관상 또는 관련 없는 변경 사항을 제거합니다. 패키지 소유자가 아직 취약점을 해결하지 않은 경우 처음부터 패치를 작성합니다.

릴리스하기 전에 패치를 확인하고 이전 버전으로 백포닝하고 패치가 기능을 손상시키지 않았는지 테스트합니다.

패치는 [Snyk의 오픈소스 취약점 데이터베이스](https://github.com/Snyk/vulndb/)의 일부이므로 적용하기 전에 확인할 수 있습니다. 예를 들어 [ms ReDoS 취약점](https://github.com/Snyk/vulndb/tree/master/data/npm/ms/20151024)에 대한 패치입니다. 모든 케이스에 대한 패치가 있는 것은 아닙니다. 누락된 패치가 필요한 경우 알려주십시오.

## Snyk 패치는 언제 어떻게 생성됩니까?

Snyk은 영향이 큰 취약점에 대한 패치를 생성하며, 많은 사용자에게 영향을 미치는 인기 있는 패키지의 심각한 취약점인 경우 패치에 많은 영향을 줍니다.

Snyk Security 팀은 일반적으로 디펜던시에 추가된 수정 사항을 백포팅하여 패치를 생성합니다. 백포팅은 특정 버전의 소프트웨어에 대해 빌드된 수정 사항을 사용하여 해당 소프트웨어의 이전 버전에 적용하는 작업입니다. 기능적으로 동일하지만 취약점에 대한 수정 사항이 적용된 업데이트를 통해 해당 소프트웨어의 이전 버전에 적용합니다. 자세한 내용은 [Backporting Security Fixes](https://access.redhat.com/security/updates/backporting)에 대한 Redhat의 설명을 참조하십시오.

Snyk Security Engineer에 의해 패치가 생성되면 팀원 2명이 패치를 검토합니다. 패치는 다음과 같은 방법으로 테스트됩니다.

1. 패키지는 패키지 자동화 테스트를 사용하여 빌드 및 테스트됩니다.
2. 패치된 패키지를 사용하는 패키지 또는 애플리케이션은 자동화된 테스트를 사용하여 테스트됩니다.
3. 맞춤형 테스트는 Snyk Security 팀이 만들고 실행합니다.

모든 패치는 커뮤니티에서 다운로드 및 검토할 수 있으며 피드백도 환영합니다.

유지 관리되지 않는 패키지의 경우 패치를 생성하고 merge할 프로젝트에 대한 pull request를 생성합니다.

## Snyk CLI를 사용할 때 패치는 어떻게 작동합니까?

`protect` 명령이 `@snyk/protect`로 대체되었습니다. https://github.com/snyk/snyk/tree/master/packages/snyk-protect; [`snyk-protect` 명령에 대한 npm 패키지입니다.](https://www.npmjs.com/package/@snyk/protect) 이 페이지에는 패키지를 사용하고 `snyk protect` 마이그레이션하는 방법이 있습니다.

## 소스 코드 통합을 사용할 때 패치는 어떻게 작동합니까?

패치를 사용하여 취약점을 수정하도록 선택하면 `snyk`이 디펜던시로 추가되고 적용할 패치 목록이 포함된 `.snyk` 파일이 생성됩니다.

`.snyk` 파일에는 `node_modules`의 여러 위치에 표시될 수 있는 디펜던시당 패치의 세부 정보가 포함되어 있습니다. 예시는 다음과 같습니다.

```
'npm:negotiator:20160616':
    - errorhandler > accepts > negotiator:
       patched: '2017-05-05T12:39:16.961Z'
    - negotiator: 
       patched: '2017-05-05T12:39:16.961Z'
```
