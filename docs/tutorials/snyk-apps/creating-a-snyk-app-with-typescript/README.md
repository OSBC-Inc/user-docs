# TypeScript로 Snyk 앱 만들기

이 튜토리얼에서는 TypeScript를 사용하여 사용자에게 Snyk 내의 프로젝트 목록을 표시하는 간단한 Snyk 앱을 만듭니다.

## 전제 조건

* NodeJS
* Snyk 계정

## 기본 구성

시작하려면 장치의 어딘가에 프로젝트를 보관할 디렉터리를 만듭니다. 새로 생성된 디렉터리 내에서 응용 프로그램에 대한 `package.json` 매니페스트를 초기화하여 종속성을 추적하고 프로젝트를 이식할 수 있도록 합니다.

이렇게 하려면 `npm init`를 실행하고 프롬프트를 따릅니다. 여기에 원하는 만큼의 정보를 추가할 수 있습니다. 지금은 기본 옵션으로 충분합니다.

종속성 정보를 저장할 위치가 있으므로 `npm`을 사용하여 TypeScript를 개발 종속성으로 설치합니다:

```
npm install typescript --save-dev
```

이 시점에서 TypeScript가 설치되었지만 `tsc` 바이너리에 컴파일 옵션을 제공하려면 구성 파일이 필요합니다. 아래 템플릿을 사용하여 `tsconfig.json`이라는 프로젝트의 루트에 TypeScript 구성 파일을 만듭니다.

```json
{
  "compilerOptions": {
    "target": "es6",
    "module": "commonjs",
    "declaration": true,
    "sourceMap": true,
    "moduleResolution": "node",
    "outDir": "./dist",
    "rootDir": "./src",
    "strict": true,
    "skipLibCheck": true,
    "esModuleInterop": true
  },
  "exclude": [
    "./tests",
    "./dist"
  ]
}
```

우리가 제공한 옵션은 TypeScript에 ES6 JavaScript, 생성할 모듈 코드 유형, 컴파일된 파일에 해당하는 소스 맵을 제공할지 여부 및 몇 가지 편리한 옵션을 내보낼 것을 지시합니다. 가능한 옵션에 대한 전체 개요를 보려면 [https://aka.ms/tsconfig.json](https://aka.ms/tsconfig.json) 을 방문하세요.

이 자습서의 목적을 위해 우리가 설정한 가장 주목할만한 옵션은 `rootDir` 및 `outDir`입니다. 이러한 옵션은 각각 소스 `.ts` 파일과 컴파일된 `.js` 파일이 프로젝트 내에서 어디에 있는지 설명합니다. 설정 값이 참조하는 디렉터리를 만듭니다:

```bash
mkdir ./dist
mkdir ./src
```

### 그것을 시험해보십시오

이제 기본 매개변수가 준비되었으므로 `./src/index.ts` 파일을 생성하여 간단한 Hello World를 생성합니다.

```
const world = 'world';

export function hello(world: string = world): string {
  return `Hello ${world}! `;
}
```

이제 모든 것이 올바르게 연결되었는지 확인할 수 있습니다. `npx tsc`를 실행하여 프로젝트를 컴파일합니다.

모든 것이 성공적이면 프로젝트 트리는 이제 다음과 같아야 합니다:

```
my-snyk-app/
 - dist/
   - index.d.ts
   - index.js
   - index.js.map
 - src/
   - index.ts
 - node_modules/
   - <lots of things here>
 - package-lock.json
 - tsconfig.json
```

`tsc` 프로그램은 소스 TypeScript 파일을 ES6 JavaScript로 컴파일하고 디버깅을 위한 소스 맵을 제공했습니다!

{% hint style="info" %}
컴파일러를 감시 모드로 전환하여 `.ts` 파일에서 변경 사항을 지속적으로 폴링할 수도 있습니다: `npx tsc -w`
{% endhint %}
