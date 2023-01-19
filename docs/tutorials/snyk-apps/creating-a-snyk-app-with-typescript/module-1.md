# Express.js 구성

## 애플리케이션을 제공하도록 Express 설정

지금까지 프로젝트 디렉토리, TypeScript 컴파일러 옵션을 구성하고 `Hello World`를 출력하는 매우 간단한 TypeScript 애플리케이션을 만들었습니다.

이 섹션에서는 `ExpressJS`를 믹스에 추가하여 애플리케이션을 확장하여 애플리케이션을 제공하고 다양한 종류의 요청을 처리하도록 미들웨어를 구성합니다.

### 새 종속성 설치

다음을 실행하여 이 섹션에 필요한 새 패키지를 설치합니다. 차례로 다루겠습니다.

```
npm install --save \
  express \
  express-rate-limit \
  express-session \
  http
```

패키지에 대한 TypeScript 유형 및 인터페이스 정의를 개발 종속성으로 설치합니다:

```
npm install --save-dev \
  @types/express \
  @types/express-rate-limit \
  @types/express-session \
  @types/node
```

### 앱 포함

> 이 자습서에서는 개체 지향 프로그래밍 개념을 사용합니다. OOP에 익숙하지 않다면 이 [MDN 페이지](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Object-oriented\_JS)에서 간단한 입문서를 확인하십시오.

시작하려면 자습서의 이 부분에서 작업할 응용 프로그램 코드를 보관할 새 파일을 만들어 보겠습니다. 간단한 'Hello world' 앱을 구성한 이전 모듈에서 방금 온 경우 `index.ts` 파일을 그대로 두어도 됩니다.

```bash
touch ./src/app.ts
```

새 파일`(./src/app.ts)`의 맨 위에 Express 및 해당 TypeScript 유형/인터페이스 정의에 대한 import 문을 추가한 다음 응용 프로그램을 실행하는 데 필요한 모든 관련 기능 및 구성을 수용할 `App` 클래스를 만듭니다.

클래스의 생성자는 클래스가 인스턴스화될 때 포트 3000에서 Express를 초기화합니다. Express 서버의 실제 시작을 처리할 생성자가 호출할 개인 함수 `listen()`을 만들 것입니다.

하단에 클래스를 내보내는 것을 잊지 마세요. 나중에 필요합니다.

```typescript
import express from 'express';
import type { Application } from 'express';
import type { Server } from 'http';

class App {
  public app: Application;
  private server: Server;

  constructor() {
    this.app = express();
    this.server = this.listen(3000);
  }

  private listen(port: number) {
    this.server = this.app.listen(port, () => {
      console.log(`App listening on port: ${port}`);
    });

    return this.server;
  }

}

export default App;
```

`npx tsc`를 사용하여 새 파일을 테스트하고 `./dist` 디렉터리에 `app.js` 파일이 성공적으로 생성되었는지 확인합니다. 오류가 없으면 훌륭합니다! 경로 추가를 시작할 준비가 되었습니다.

### 기본 경로

Express는 주어진 포트에서 모든 요청을 수신하지만 요청을 받았을 때 무엇을 해야할지 모릅니다. 수신할 수 있는 다양한 유형의 요청을 처리하는 방법을 Express에 알려야 합니다. 이를 구성하는 방법은 애플리케이션의 아키텍처와 적중 시 앱이 응답할 것으로 예상하는 경로/페이지에 따라 크게 달라집니다.

이 자습서에서는 일을 간단하게 유지합니다. 우리의 최종 목표는 Snyk 내에서 사용자에게 프로젝트 목록을 제공하는 것이므로 최소한 두 개의 경로가 필요하다고 가정해 보겠습니다: 초기 연결을 처리하는 인덱스 경로(`/`)와 Snyk의 데이터를 표시하는 프로젝트 경로(`/projects`).

프로젝트를 체계적으로 유지하기 위해 경로 모음을 보관할 `routes` 디렉토리를 만들고 경로에 대한 기본 컨트롤러 파일과 필요한 추가 항목을 포함할 자체 하위 디렉토리를 각 경로에 제공합니다.

이 모듈의 색인 경로에 중점을 둘 것입니다:

```bash
mkdir -p ./src/routes/index
touch ./src/routes/index/indexController.ts
```

인덱스 컨트롤러 작업을 시작하기 전에 컨트롤러 데이터의 공통 모양을 설명하는 [TypeScript 인터페이스](https://www.typescriptlang.org/docs/handbook/interfaces.html) 정의도 만들어야 합니다. 이렇게 하면 컨트롤러의 일관성을 유지하고 컨트롤러에 중요한 것이 누락된 경우 TypeScript가 조기에 경고할 수 있습니다.

경로에 대해 결정한 것과 유사한 분리 패턴을 사용하겠습니다. TypeScript의 인터페이스 정의는 일반적으로 독립적이고 설명적이므로 각 정의에 대한 디렉토리 생성을 건너뛰고 형제로 생성한 모든 인터페이스 파일을 저장합니다.

```bash
mkdir -p ./src/interfaces
touch ./src/interfaces/Controller.ts
```

우리가 만드는 모든 경로 컨트롤러는 최소한 Express에서 경로 값과 라우터를 가져와야 합니다. `./src/interfaces/Controller.ts`를 편집하고 아래 내용으로 채웁니다.

```typescript
import type { Router } from 'express';

export interface Controller {
  path: string;
  router: Router;
}
```

완료되면 편집기에서 경로 컨트롤러 파일(`./src/routes/index/indexController`)을 열고 다음을 추가합니다.

```typescript
import type { Controller } from '../../interfaces/Controller';
import type { Request, Response, NextFunction } from 'express';
import { Router } from 'express';

class IndexController implements Controller {
  public path = '/';
  public router = Router();

  constructor() {
    this.initRoutes();
  }

  private initRoutes() {
    this.router.get(`${this.path}`, this.indexPage);
  }

  private indexPage(req: Request, res: Response, next: NextFunction) {
    return res.send('index route!');
  }
}

export default IndexController;
```

여기에서 우리는 Express 패키지에서 Router 개체뿐만 아니라 소수의 TypeScript 유형/인터페이스 정의를 가져왔습니다.

우리는 '인덱스'를 렌더링하는 `indexPage` 함수로 `/` 요청에 응답하도록 `IndexController`를 설정했지만 App 클래스는 아직 인스턴스화할 때 경로를 등록할 방법이 없습니다. `./src/app.ts` 파일로 돌아가서 `initRoutes()` 함수를 추가해 보겠습니다.

그 동안 컨트롤러 배열과 포트 값을 인수로 사용하도록 앱의 생성자 함수도 수정합니다.

`./src/app.ts`를 편집하고 내용을 다음과 일치하도록 업데이트합니다:

```typescript
import express from 'express';
import type { Application } from 'express';
import type { Server } from 'http';
import type { Controller } from './interfaces/Controller';

class App {
  public app: Application;
  private server: Server;

  constructor(controllers: Controller[], port: number) {
    this.app = express();
    this.initRoutes(controllers);
    this.server = this.listen(port);
  }

  private initRoutes(controllers: Controller[]) {
    controllers.forEach((controller: Controller) => {
      this.app.use('/', controller.router);
    });
  }

  private listen(port: number) {
    this.server = this.app.listen(port, () => {
      console.log(`App listening on port: ${port}`);
    });

    return this.server;
  }

}

export default App;
```

### 익스프레스 서버 실행

지금까지 우리는 인스턴스화될 때 `/`의 요청에 응답하는 Express 서버를 실행하는 App 클래스를 생성했으며 모든 컨트롤러가 동일한 데이터 패턴을 따르도록 인터페이스 정의를 추가했습니다.

프로젝트를 실행하고 사용해 봅시다!

이 시점에서 컴파일된 `./dist/app.js`를 실행하면 흥미로운 일이 발생하지 않습니다. 내보낸 클래스를 실제로 인스턴스화하지 않았기 때문입니다! 이전 모듈에서 `package.json`을 초기화한 위치를 기억하십니까? 이 명령을 수행하는 동안 앱과 관련된 몇 가지 질문이 제시되었습니다. 질문 중 하나는 우리 프로젝트의 진입점이 무엇인지 물었습니다. 따라하면서 기본값을 선택한 경우 `package.json`에서 `index.js`로 설정해야 합니다. 이 진입점은 App 클래스를 인스턴스화할 위치입니다.

`./src/index.ts`(hello world 코드가 있는 곳)를 편집하고 남은 콘텐츠가 있으면 지운 다음 앱 및 기타 필수 개체에 대한 import 문을 추가합니다.

진입점은 `new` 키워드로 App 클래스를 인스턴스화하는 한 가지 작업만 수행합니다.

```typescript
import IndexController from './routes/indexController';
import App from './app';

new App(
  [
    new IndexController()
  ],
  3000
);
```

그게 전부입니다!

`npx tsc`를 사용하여 프로젝트를 빌드한 다음 `node`를 사용하여 컴파일된 진입점을 실행합니다.

```bash
npx tsc && node ./dist/index.js
```

모든 것이 성공적이면 콘솔에 `App listening on port: 3000` 메시지가 표시됩니다.

이제 브라우저에서 http://localhost:3000을 방문하거나 curl을 사용하여 응답을 확인하십시오. `index route!`가 보이면 축하합니다! Express는 애플리케이션을 제공하고 경로에 응답합니다!

이 튜토리얼의 다음 모듈에서는 경로, 인증에 대해 자세히 알아보고 Snyk API 작업을 시작할 것입니다. 거기서 뵙겠습니다!
