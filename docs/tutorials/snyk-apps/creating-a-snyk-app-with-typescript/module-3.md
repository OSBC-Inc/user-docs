# 사용자를 위한 콘텐츠 렌더링

이전 모듈에서는 Snyk 앱 등록, 인증 흐름 설정 및 앱 내 사용자 인증 처리에 대해 다루었습니다. 이러한 모든 주제는 모든 Snyk 앱의 기능에 필수적이지만 모두 "비하인드 스토리" 주제라고 할 수 있습니다.

이 모듈에서는 Snyk 앱으로 승인한 사용자에게 콘텐츠를 표시하는 데 집중하도록 기어를 전환합니다. 구체적으로, 승인되지 않은 사용자에게 클릭할 수 있는 큰 버튼을 표시하고 사용자에게 Snyk의 프로젝트 목록을 승인하고 승인하려고 합니다.

## Snyk 앱에 템플릿 엔진 추가

Express는 콘텐츠를 화면에 완벽하게 인쇄하고 HTML 서버 측 렌더링까지 할 수 있지만 템플릿 엔진을 사용하면 삶이 훨씬 쉬워집니다. 이 자습서에서는 [EJS](https://ejs.co/)를 사용합니다.

먼저 튜토리얼의 이 부분에서 사용할 노드 패키지를 설치합니다:

```bash
npm install --save ejs
```

다음으로 우리는 마지막 모듈에서 생성한 `initGlobalMiddlewares()` 함수를 수정하여 보기 엔진(이 경우 EJS)을 사용하고 싶다고 표현하고 보기 템플릿을 저장할 위치를 알려줍니다. EJS 템플릿을 `./src/views`에 저장하고 공통 파일(예: 이미지, CSS 등)을 `/.src/public`에 보관합니다.

먼저 새 디렉터리를 만듭니다.

```bash
mkdir -p ./src/views/partials
mkdir -p ./src/public
```

이제 `./src/app.ts`를 업데이트할 수 있습니다:

```typescript
// ./src/app.ts
...

class App {

  ...

  private initGlobalMiddlewares() {

    ...

    this.app.set("views", path.join(__dirname, "/views"));
    this.app.set("view engine", "ejs");
    this.app.use('/public', express.static(path.join(__dirname, '/public')));

    ...

  }

  ...

}
```

템플릿을 제공할 각 경로에 대해 해당 컨트롤러를 수정하고 `res.send()`와 같이 더 단순한 것이 아니라 `res.render("<template name>")`을 사용하고 있는지 확인해야 합니다. .

E.g.,

```typescript
...

private initRoutes() {
  this.router.get(`${this.path}`, this.indexPage);
}
private indexPage(req: Request, res: Response, next: NextFunction) {
  // THIS right here is what causes Express to render the EJS template.
  return res.render("index");
}

...
```

그게 전부입니다.

EJS 템플릿은 부분 포함 개념을 지원합니다. 반드시 필요한 것은 아니지만 `./src/views`에 하위 디렉토리를 추가하여 머리글 및 바닥글과 같은 부분 템플릿을 경로 템플릿과 구별하는 것이 좋습니다. 자습서에서는 `./src/views/partials`를 사용하여 이러한 템플릿을 저장합니다.

## 기본 EJS 템플릿

The first template we'll create is a partial, which we'll include in the other templates. This `header.ejs` will be the place we link stylesheets and other information that belongs in the `<head>` of an HTML document.

```ejs
// ./views/partials/header.ejs

<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link rel="preconnect" href="https://fonts.googleapis.com" />
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;500&display=swap" rel="stylesheet" />
    <link href="https://raw.githubusercontent.com/snyk/snyk-apps-demo/main/src/public/css/styles.css" />
    <link rel="shortcut icon" href="https://raw.githubusercontent.com/snyk/snyk-apps-demo/main/src/public/images/snyk_dog.svg" type="image/x-icon" />

    <title>Snyk Apps Tutorial</title>
  </head>
</html>
```

This `index.ejs` template will cover our basic `/` route.

```ejs
// ./views/index.ejs

<%- include('./partials/header.ejs') %>

<body>
  <div class="index-page">
    <img class="index-page__snyk-logo" src="https://github.com/snyk/snyk-apps-demo/raw/main/src/public/images/snykLogoWithDog.svg" alt="snyk-logo" />
    <div class="index-page__card">
      <h1 class="index-page__title">Add Demo App</h1>
      <p class="index-page__description">Authorize this App to connect to your Snyk account.</p>
      <button class="button" onclick="location.href='/auth';">Install App</button>
    </div>
  </div>
</body>
```

`callback.ejs` will render for successful user authorizations.

```ejs
// ./views/callback.ejs

<%- include('./partials/header.ejs') %>
<body>
  <div>
    <h2 class="main__heading">Snyk Apps Tutorial</h2>
  </div>
  <div class="card__30">
    <div class="callback-page__success-box">
      <img class="snyk-con-img" src="https://github.com/snyk/snyk-apps-demo/raw/main/src/public/images/success_check.svg" alt="success" />
        <div>
          <h2 class="callback-page__success-text">Successfully connected to Snyk!</h2>
        </div>
        <button class="button" onclick="location.href='/projects';">List Projects</button>
      </div>
    </div>
  </div>
</body>
```

The above templates should be enough to get you started adding your own templates to any new routes you create. If you intend to continue using EJS, make sure to reference the documentation for information about the features offered.

Rendering content for your Snyk App can be as simple or complex as you'd like it to be. Because we're dealing with JavaScript, the options are very flexible!

## Showing users a list of projects

Now that we've got some basic templates, let's take a look at how we can add some functionality to our Snyk App using a User's Snyk data. For this tutorial, we'll be setting up our app to allow users to view all of their projects within Snyk from within our app.

This is a basic, but easily extendable feature.

We'll need to create:

* A new route controller
* A function (or functions) to pull the project data
* An EJS template for showing the projects

Let's start with the API work. We'll utilize the `callSnykApi()` function we created in the previous module. Since this directly relates to a particular route, we'll store this file with its controller. Following the patteren we've used throughout these tutorial modules, we'll create both files at `./src/routes/projects/`.

```typescript
// ./src/routes/projects/projectsHandler.ts

import { readFromDb } from "../../util/DB";
import { callSnykApi } from "../../util/apiHelpers";
import { EncryptDecrypt } from "../../util/encrypt-decrypt";
import { AuthData } from "../../interfaces/DB";
import { APIVersion } from "../../interfaces/API";
import { ENCRYPTION_SECRET } from "../../app";

/**
 * Get projects handler that fetches all user projects
 * from the Snyk API using user access token. This for
 * example purposes. In production it will depend on your
 * token scopes on what you can and can not access
 * @returns List of user project or an empty array
 */
export async function getProjectsFromApi(): Promise<unknown[]> {
  // Read data from DB
  const db = await readFromDb();
  const data = mostRecent(db.installs);
  // If no data return empty array
  if (!data) return [];

  // Decrypt data(access token)
  const eD = new EncryptDecrypt(ENCRYPTION_SECRET as string);
  const access_token = eD.decryptString(data?.access_token);
  const token_type = data?.token_type;
  // Call the axios instance configured for Snyk API v1
  const result = await callSnykApi(
    token_type,
    access_token,
    APIVersion.V1
  ).post(`/org/${data?.orgId}/projects`);

  return result.data.projects || [];
}

/**
 *
 * @param {AuthData[]} installs get most recent install from list of installs
 * @returns the latest install or void
 */
export function mostRecent(installs: AuthData[]): AuthData | void {
  if (installs) {
    return installs[installs.length - 1];
  }
  return;
}
```

Next we'll write the route controller. Follow the pattern: `./src/routes/projects/projectsController.ts`.

```typescript
// ./src/routes/projects/projectsController.ts

import type { Controller } from "../../interfaces/Controller";
import type { NextFunction, Request, Response } from "express";
import { Router } from "express";
import { getProjectsFromApi } from "./projectsHandler";

export class ProjectsController implements Controller {
  // The base URL path for this controller
  public path = "/projects";
  // Express router for this controller
  public router = Router();

  constructor() {
    this.initRoutes();
  }

  private initRoutes() {
    // The route to render all user projects lists
    this.router.get(`${this.path}`, this.getProjects);
  }

  private async getProjects(req: Request, res: Response, next: NextFunction) {
    try {
      const projects = await getProjectsFromApi();
      return res.render("projects", {
        projects,
      });
    } catch (error) {
      return next(error);
    }
  }
}
```

Whenever we add a new route controller, we need to update `./index.ts` to include it.

```typescript
// ./src/index.ts

import IndexController from "./routes/index/indexController";
import AuthController from "./routes/auth/authController";
import CallbackController from "./routes/callback/callbackController";
import ProjectsController from "./routes/projects/projectsController";
import App from "./app";

new App([
   new IndexController(),
   new AuthController(),
   new CallbackController()
   new ProjectsController()],
  3000
);
```

## Wrap-up

Using the projects API handler and controller we created in this module, you should have all you need to create your own custom code and make your Snyk App do whatever you'd like it to do.

We used the v1 API here, but make sure to keep an eye out on Snyk's V3 API over the next months as more and more features are added, you may find new or more efficient endpoints to use in your Snyk App!
