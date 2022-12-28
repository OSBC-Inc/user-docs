# 앱 등록 및 사용자 인증 구성

이 자습서의 이전 섹션에서는 TypeScript 프로젝트를 설정하고 Express 서버를 추가하고 몇 가지 기본 라우팅을 구성했습니다. 우리는 이전 섹션에서 생성한 프로젝트 위에 빌드할 것이므로 아직 하지 않은 경우 계속하기 전에 이 자습서의 이전 부분을 먼저 완료하는 것이 좋습니다.

## Snyk 앱 생성 및 등록

우리는 지금까지 TypeScript 애플리케이션으로 좋은 진전을 이루었지만 현재로서는 TypeScript 애플리케이션이 전부입니다. Bonified Snyk 앱으로 전환하려면 Snyk의 API를 사용하여 프로젝트를 새 앱으로 등록해야 합니다.

### 전제 조건

* API 권한이 있는 Snyk 계정
* [Snyk API 토큰](https://docs.snyk.io/features/snyk-api-info/authentication-for-api)
* 앱 소유자로 등록될 Snyk 조직의 `orgId`

`orgId` 얻기

`orgId`를 검색하는 방법에는 두 가지가 있습니다. 첫 번째는 Snyk 계정에 로그인하고 ID를 검색하려는 조직의 조직 설정 페이지를 방문하는 것입니다. 조직 설정 페이지의 경로는 다음과 같습니다:

```
https://snyk.io/org/{your-org-name}/manage/settings
```

또는 인증 헤더의 API 토큰을 사용하여 `https://snyk.io/api/v1/orgs` API 끝점을 통해 조직의 `orgId`를 검색할 수도 있습니다. 이 끝점에 대한 자세한 내용은 [여기](https://snyk.docs.apiary.io/#reference/organizations/the-snyk-organization-for-a-request/list-all-the-organizations-a-user-belongs-to)에서 해당 설명서를 참조하십시오.

### Snyk 앱 및 Snyk API 정보

Snyk 앱은 앱을 설치하는 사용자가 액세스 비용을 지불했는지 여부에 관계없이 API에 대한 일급 액세스 권한을 갖습니다. 이 기능을 활용하려면 앱 내에서 API에 액세스할 때 앱이 기존의 https://snyk.io/api/가 아닌 https://api.snyk.io/ 도메인이 있는 API 엔드포인트를 사용해야 합니다.

### Snyk에 앱 등록

새로운 Snyk 앱 등록은 Snyk의 API에 대한 간단한 POST 요청을 통해 수행됩니다. 요청을 수행하기 위해 이 자습서 전체에서 구축한 앱을 확실히 구성할 수 있지만 대신 한 번만 실행할 수 있는 함수를 만들지 않도록 `curl`을 사용하여 직접 요청을 수행합니다.

요청 본문에는 다음 세부 정보가 필요합니다:

* `name`: Snyk 앱의 이름
* `redirectUris`: 최종 사용자 인증 중 허용된 콜백 위치
* `scopes`: Snyk 앱이 사용자에게 부여할 계정 권한

> `scopes`에 대한 참고 사항: 일단 등록되면 Snyk Apps `scopes`는 현재 변경할 수 없습니다. 유일한 방법은 앱 삭제 API 엔드포인트를 사용하여 Snyk [앱을 삭제](https://snykv3.docs.apiary.io/#reference/apps/single-app-management/delete-app)하고 새 Snyk 앱으로 다시 등록하는 것입니다.

**이 글을 쓰는 시점에서 Snyk Apps는 아직 베타 버전입니다. 현재 사용 가능한 범위는 `apps:beta` 1개뿐입니다. 이 범위를 통해 앱은 기존 프로젝트를 테스트 및 모니터링하고 Snyk 조직, 기존 프로젝트, 문제 및 보고서에 대한 정보를 읽을 수 있습니다.**

**Snyk 앱 베타의 제한 사항 중 하나는 Snyk 앱이 등록된 조직에 대한 관리자 액세스 권한이 있는 사용자만 Snyk 앱을 인증할 수 있다는 것입니다.**

API 토큰과 `orgId`를 가지고 터미널에서 다음 명령을 수행하고 필요에 따라 값을 대체합니다. 이 자습서에서는 `redirectUris` 값에 대해 `http://localhost:3000/callback`을 사용합니다.

> Tip: API 토큰 및 기타 암호를 파일에 내보내기 문으로 추가하고 파일을 소싱하여 환경 변수로 설정하면 셸에 직접 입력하는 것을 방지할 수 있습니다.

```bash
curl --include \
     --request POST \
     --header "Content-Type: application/vnd.api+json" \
     --header "Authorization: token <API_TOKEN>" \
     --data-binary "{
       \"name\": \"My Awesome App\",
       \"redirectUris\": [ \"http://localhost:3000/callback\" ],
       \"scopes\": [ \"apps:beta\" ]
       }" \
     'https://api.snyk.io/v3/orgs/<ORG_ID>/apps?version='
```

Snyk의 응답에는 Snyk 앱의 통합을 완료하는 데 필요한 두 가지 중요한 값인 `clientId` 및 `clientSecret`이 포함되어 있습니다. 이 값을 안전한 곳에 저장하십시오. Snyk에서 `clientSecret`을 볼 수 있는 유일한 시간입니다. **주의**: **`clientSecret`을 공개적으로 공유하지 마십시오**. 이는 Snyk로 앱을 인증하는 데 사용됩니다.

이제 Snyk 앱으로 등록했으므로 사용자가 승인할 수 있도록 TypeScript 프로젝트 조정을 시작할 수 있습니다.

## Snyk 앱을 통한 사용자 인증

Snyk 앱에 대한 사용자 인증은 Snyk 앱의 데이터와 일치하는 쿼리 매개변수가 포함된 웹페이지 URL을 통해 수행됩니다. 이 URL의 쿼리 매개변수 값을 교체하고 사용자를 웹 브라우저의 최종 링크로 보내야 합니다. 여기에서 Snyk 앱에 대한 계정 액세스 권한을 부여할 수 있습니다.

액세스가 프로비저닝되면 사용자는 앱의 등록된 `callbackURL`(`http://localhost:3000/callback`으로 정의됨)로 다시 이동됩니다.

기본적으로 앱은 다음과 같은 링크를 생성한 다음 인증할 시간이 되면 사용자를 링크로 보내야 합니다.

```
https://app.snyk.io/oauth2/authorize?response_type=code&client_id={clientId}&redirect_uri={redirectURI}&scope={scopes}&nonce={nonce}&state={state}&version={version}
```

쿼리 매개변수 중 일부는 다소 명확할 수 있지만 살펴보겠습니다. 사용자를 위해 이 URL을 생성하도록 Snyk 앱을 수정하겠습니다.

* `version`: 현재 버전은 [Snyk의 API 문서](https://snykoauth2.docs.apiary.io/#reference/apps/app-authorization/authorize-an-app)에서 찾을 수 있습니다.
* `scopes` 와`redirect_uri`: 이 값은 이전에 등록 명령으로 전송된 값과 일치해야 합니다.
* `state`: 이것은 이 `/authorize` 호출에서 `redirect_uri`의 콜백(예: 사용자 ID)에 대한 앱 특정 상태를 전달하는 데 사용됩니다. [CSRF 공격을 방지](https://datatracker.ietf.org/doc/html/rfc6749#section-10.12)하려면 콜백에서 확인해야 합니다.
* `nonce`: `/authorize`를 호출하기 전에 앱 측의 타임스탬프와 함께 고도로 무작위화된 문자열이 저장된 다음 반환된 액세스 토큰에서 확인됩니다.

연결이 완료되면 사용자는 다음 권한 부여 단계에 필요한 쿼리 문자열 매개 변수 `code` 및 `state`가 추가된 제공된 리디렉션 URI(이 경우 `/callback` 경로)로 리디렉션됩니다.

그 다음 단계는 이전 단계의 응답에서 쿼리 매개변수로 받은 인증 코드를 가져오고 이를 액세스 토큰으로 바꾸는 것입니다. 이를 위해 Snyk 앱은 `https://api.snyk.io/oauth2/token` 토큰 끝점에 대한 POST 요청을 만듭니다. 해당 POST 요청에는 인증 코드, 클라이언트 ID, 클라이언트 비밀 등을 포함하여 요청 본문에 특정 데이터가 필요합니다.

성공하면 해당 POST 요청의 응답에는 Snyk 앱이 인증 사용자를 대신하여 Snyk와 통신하는 데 필요한 모든 것, 즉 **refresh\_token** 및 **액세스 토큰**이 포함됩니다.

액세스 토큰은 향후 API 호출에 사용되며 새로 고침 토큰보다 만료 기간이 훨씬 짧습니다. 갱신 토큰은 만료 시 새 액세스 토큰을 얻기 위해 한 번만 사용할 수 있습니다. 즉, **refresh\_token은 자체 만료 시간이 경과하거나 access\_token을 새로 고치는 데 사용되는 경우 더 이상 사용할 수 없습니다**. 궁극적으로 이는 Snyk 앱이 **refresh\_token** 교환을 수행하기 위해 API를 자주 호출해야 함을 의미합니다.

{% hint style="info" %}
이 두 토큰은 모두 저장하기 전에 암호화해야 합니다!
{% endhint %}

## 사용자 인증을 처리하도록 Snyk 앱 업데이트

Based on the above information, our Snyk App has some new requirements! Let's outline a few things we'll need to do within our TypeScript app to successfully authorize a Snyk user account with our Snyk app:

1. Send API requests and process responses
2. Keep track of data, like token expiry
3. Encrypt & decrypt secret data
4. Turn authorization _codes_ into authorization _tokens_.
5. Refresh those authorization tokens.
6. Handle errors and inform users of authorization success or failure

From here on, we'll be doing quite a lot of refactoring in our Snyk App and we'll be jumping into quite a few different files. To help make the process easier to follow, this tutorial is going to adopt the convention of adding a commented filepath to the first line of code snippets, describing where they belong. In your own code, these comments aren't necessary.

We'll also add quite a few new packages to help address our new requirements. For convenience, go ahead and run the following in the root of your project:

```bash
npm install --save passport \
    passport-oauth2 \
    @snyk/passport-snyk-oauth2 \
    @types/passport \
    @types/uuid \
    express-session \
    axios \
    uuid \
    ejs \
    jwt-decode \
    cryptr \
    "github:dankreiger/lowdb#chore/esm-cjs-hybrid-WITH-LIB" # This allows lowdb to be used with commonjs modules
    luxon;

npm install --save-dev @types/cryptr \
    @types/ejs \
    @types/express-session \
    @types/luxon \
    @types/passport \
    @types/passport-oauth2 \
    @types/uuid
```

### Store data and config in the Snyk App

#### Application configuration

Application config (e.g.: client secrets, api tokens, other config, etc...) should generally be stored securely and kept outside of the App itself. However, for brevity, this tutorial will simply add the configuration info as exportable constants in the `App.ts` file and leave the actual implementation details to you, the reader. These are values that the Snyk App will be references in many different places.

```typescript
// ./src/app.ts

...

import { v4 as uuid4 } from "uuid";

...

export const APP_BASE = "https://app.snyk.io";
export const API_BASE = "https://api.snyk.io";
export const CLIENT_ID = "[replace with your client id]";
export const CLIENT_SECRET = "[replace with your client secret]";
export const ENCRYPTION_SECRET = uuid4();
export const REDIRECT_URI = "https://localhost:3000/callback";
export const TOKEN_URL = "/oauth2/token";
export const AUTHORIZATION_URL = "/oauth2/authorize";
export const SCOPE = "apps:beta";
export const NONCE = uuid4();
export const STATE = true;
...
```

#### Storing data

One of the things we'll want to do is capture some information about the users that authorize our Snyk App. Again, a true implementation is left up to the reader. For the purposes of this tutorial, we'll use the excellent `lowdb`, a small local JSON database with low overhead.

We'll first create a new middleware function in `app.ts` to initialize a `lowdb` database file at `./db/` and tell the `App` constructor to call it.

```typescript
// ./src/app.ts

...
import * as path from "path";
import * as fs from "fs";

...

constructor(controllers: Controller[], port: number) {
  this.app = express();
  this.initDatabaseFile();
  this.initRoutes(controllers);
  this.server = this.listen(3000);
}

...

private initDatabaseFile() {
  try {
    const dbFolder = path.join(__dirname, "../db");
    dbPath = path.join(dbFolder, "db.json");
    console.log(`Using db: ${dbPath}`);
    if (!fs.existsSync(dbPath)) {
      if (!fs.existsSync(dbFolder)) {
        fs.mkdirSync(dbFolder);
      }
    }
  } catch (error) {
    console.error(error);
  }
}

...

export let dbPath: string;
export default App;
```

With the database initialization handled, we'll create some new helper methods to make reading/writing/updating database entries simpler. Because this is a TypeScript project, we'll be creating interfaces or types around the data structures we'll be storing, so we'll create two files: `./src/interfaces/DB.ts` and `./src/util/DB.ts`:

```bash
touch ./src/interfaces/DB.ts
mkdir -p ./src/util
touch ./src/util/DB.ts
```

Populate the interface file with an interface describing each piece of the authorization data we'll be storing, and a wrapping interface we can apply to the entire database:

```typescript
// ./src/interfaces/DB.ts

export interface DB {
  installs: AuthData[];
}

export interface AuthData {
  date: Date;
  userId: string;
  orgId: string;
  access_token: string;
  expires_in: 3600;
  scope: string;
  token_type: string;
  nonce: string;
  refresh_token: string;
}
```

In this tutorial, we'll only need to perform three basic interactions with our database: read, write, and update.

Within the file we created in `./src/util`, create a function for each. Our read function will return a Promise with the database contents, the write function will take an object that matches the `AuthData` interface we just described, and the update function will attempt to rewrite an entry, returning a boolean denoting success or failure.

```typescript
// ./src/util/DB.ts

import { dbPath } from "../app";
import { AuthData, DB } from "../interfaces/DB";
import { Low, JSONFile } from "lowdb";

export async function readFromDb(): Promise<DB> {
  const adapter = new JSONFile<DB>(dbPath);
  const db = new Low<DB>(adapter);
  await db.read();
  // Return existing data or create a new DB
  return db.data ?? buildNewDb();
}

function buildNewDb(): DB {
  return { installs: [] };
}

export async function writeToDb(data: AuthData): Promise<void> {
  const existingData = await readFromDb();
  existingData.installs.push(data);
  // Creates a new DB if one doesn't already exists
  const adapter = new JSONFile(dbPath);
  const db = new Low(adapter);
  db.data = existingData;
  return db.write();
}

export async function updateDb(
  oldData: AuthData,
  newData: AuthData
): Promise<boolean> {
  const adapter = new JSONFile<DB>(dbPath);
  const db = new Low<DB>(adapter);
  await db.read();
  if (db.data == null) {
    return false;
  }
  // After reading check if data exists in the database
  const installs = db.data?.installs || [];

  const index = installs.findIndex((install) => install.date === oldData.date);
  if (index === -1) return false;
  installs[index] = newData;
  // Replace the existing install with new one
  db.data.installs = installs;
  await db.write();
  return true;
}
```

### Prepare for API calls

Earlier, we installed the popular `axios` package to handle API calls. We know that we'll need to make some repetetive calls to the same API, so let's abstract some helper functions to make our code easily re-usable across the project. Create an `APIHelpers.ts` file in the `util` directory.

Before we fill that out, take note that, while we are consistently hitting Snyk's API, we'll likely need to make requests against multiple versions of the API, depending on the endpoint's status in the migration from Snyk API v1 to Snyk API v3. One way we can handle this is by defining a TypeScript Enum and within our functions, swap any necessary query parameters by comparing an argument to the enum's possible values.

Add the following content to a new file, or to `APIHelpers.ts` if you prefer, just make sure to export it for later use!

```typescript
// ./interfaces/API.ts
export const enum APIVersion {
  V1 = "v1",
  V3 = "v3",
}
```

Let's start by adding a single function to simplify our Apps' calls to the Snyk API. The function takes a `tokenType` (either _bearer_ or _token_), the `token` itself, and an `APIVersion` (conveniently corresponding to the enum we just defined).

```typescript
// ./src/util/APIHelpers.ts

import qs from "qs";
import axios, { AxiosInstance } from "axios";
import { API_BASE, CLIENT_ID, CLIENT_SECRET, TOKEN_URL } from "../app";
import { AuthData } from "../interfaces/DB";

export function callSnykApi(tokenType: string, token: string, version: APIVersion): AxiosInstance {
  const contentType = version === APIVersion.V1 ? "application/json": "application/vnd.api+json";

  const axiosInstance = axios.create({
    baseURL: `${API_BASE}/${version}`,
    headers: {
      "Content-Type": contentType,
      Authorization: `${tokenType} ${token}`,
    },
  });

  return axiosInstance;
}
```

Because this function is an `AxiosInstance`, we can easily talk to the API's different endpoints by calling `.get()`, `.post()`, or any other methods usually available to such an object. Handy!

Let's see it in action by defining a second async function to retrieve our Snyk Apps' Organization ID:

```typescript
// ./src/util/APIHelpers.ts

...

export async function getAppOrgID(tokenType: string, accessToken: string): Promise<{ orgId: string }> {
  try {
    const clientId = CLIENT_ID;
    const result = await callSnykApi(tokenType, accessToken, APIVersion.V3)({
      method: "GET",
      url: `/apps/${clientId}/orgs?version=2021-08-11~experimental`,
    });
    // Fetch the first org
    const org = result.data.data[0];
    return {
      orgId: org.id,
    };
  } catch (error) {
    console.error("Error fetching org info: " + error);
    throw error;
  }
}
```

### Make encrypt / decrypt easy

It's a good idea to encrypt the data we'll be pulling out of the API, let's define a small class for doing so. The class has two members:

1. `secret`: The key used to encrypt data
2. `cryptr`: Instance of the Cryptr library

```typescript
// ./src/util/encrypt-decrypt.ts

import Cryptr from "cryptr";

export class EncryptDecrypt {
  private secret: string;
  private cryptr: Cryptr;

  constructor(secret: string) {
    // Uses the passed secret
    this.secret = secret as string;
    // Initialize the Cryptr instance with the secret
    this.cryptr = new Cryptr(this.secret);
  }

  /**
   * Function used to encrypt data
   * @param {String} message to be encrypted
   * @returns {String} encrypter message
   */
  public encryptString(message: string): string {
    return this.cryptr.encrypt(message);
  }
  /**
   * Function used to decrypt data
   * @param  {String} encryptedString to be decrypted
   * @returns {String} decrypted string
   */
  public decryptString(encryptedString: string): string {
    return this.cryptr.decrypt(encryptedString);
  }
}
```

### Configure Passport.js and the Snyk-OAuth2 strategy

We've laid the groundwork, now its time to start actually doing things.

As discussed in a previous section, our app needs to send would-be authorizors to a specific token URL. We'll add an `/auth` route in our Snyk App and add someauthentication middleware to Express. For this, we'll use the excellent [passportjs](https://www.passportjs.org), the [passport-oauth2](https://https/www.passportjs.org/packages/passport-oauth2) authentication strategy, along with Snyk's very own [@snyk/passport-snyk-oauth2](https://www.npmjs.com/package/@snyk/passport-snyk-oauth2). `passport` and its friends handle a large portion of what would otherwise be a lengthy and complicated authentication process.

Because `passport` takes its encapsulation philosophy seriously, we'll need to handle everything else about the auth process. We need to setup an instance of the passport strategy we'll be using. We'll put our database helpers from earlier to use here as well, adding an entry into our database when we receive successful authorization.

It's worth taking the time to go over this file and make sure you've understood everything its doing.

```typescript
// ./util/OAuth2Strategy.ts

import type { Request } from "express";
import axios, { AxiosResponse, AxiosInstance } from "axios";
import OAuth2Strategy, { VerifyCallback } from "passport-oauth2";
import SnykOAuth2Strategy, { ProfileFunc } from "@snyk/passport-snyk-oauth2";
import { v4 as uuid4 } from "uuid";
import jwt_decode from "jwt-decode";
import { EncryptDecrypt } from "../util/encrypt-decrypt";
import { writeToDb } from "../util/db";
import { AuthData } from "../interfaces/db";
import { getAppOrgID } from "../util/APIHelpers";

// This just wraps up the tutorial's app config to avoid writing
// each config variable.
// You'd likely want to parse environment variables or something.
import * as config from "../app";

// Set up a new type definition for the parameters we'll be sending with our auth.
type Params = {
  expires_in: number;
  scope: string;
  token_type: string;
};

// There is more data here but we only care about the nonce
type JWT = { nonce: string };

export function getOAuth2(): SnykOAuth2Strategy {
  const nonce = uuid4();

  // User can pass their own implementation of fetching the profile
  // by providing the profileFunc implementation. Snyk OAuth2 strategy
  // will call this function to fetch the profile associated with request
  const profileFunc: ProfileFunc = function(accessToken: string) {
    return axios.get("https://api.snyk.io/v1/user/me", {
      headers: {
        "Content-Type": "application/json; charset=utf-8",
        Authorization: `bearer ${accessToken}`,
      },
    });
  };

  // Note*: the value of version being manually added
  return new SnykOAuth2Strategy(
    {
      authorizationURL: `${config.APP_BASE}${config.AUTHORIZATION_URL}?version=2021-08-11~experimental`,
      tokenURL: `${config.API_BASE}${config.TOKEN_URL}`,
      clientID: config.CLIENT_ID,
      clientSecret: config.CLIENT_SECRET,
      callbackURL: "http://localhost:3000/callback",
      scope: config.SCOPE,
      scopeSeparator: " ",
      state: true,
      passReqToCallback: true,
      nonce,
      profileFunc,
    },
    async function (
      req: Request,
      access_token: string,
      refresh_token: string,
      params: Params,
      profile: AxiosResponse,
      done: VerifyCallback
    ) {
      try {
        // Notify passport that all work, like the storing
        // of data in the DB, has been completed
        const userId = profile.data.id;
        const decoded: JWT = jwt_decode(access_token);
        if (nonce !== decoded.nonce)
          throw new Error("Nonce values do not match");
        const { expires_in, scope, token_type } = params;

        const { orgId } = await getAppOrgID(token_type, access_token);
        const ed = new EncryptDecrypt(config.ENCRYPTION_SECRET as string);

        await writeToDb({
          date: new Date(),
          userId,
          orgId,
          access_token: ed.encryptString(access_token),
          expires_in,
          scope,
          token_type,
          refresh_token: ed.encryptString(refresh_token),
          nonce,
        } as AuthData);
      } catch (error) {
        return done(error as Error, false);
      }
      return done(null, { nonce });
    }
  );
}
```

### Update Express Middleware

With our passport strategy implemented, modify `app.ts` to setup the `passport` middleware as shown in the next code block. Rather than calling it directly, we'll create a function called `initGlobalMiddlewares()` allowing us to set up a few other middlewares at the same time:

* `express.json()`: Express middleware for handling JSON requests
* `express.urlencoded()`: Express middleware to handle URL encoded calls
* `expressSession`: We use the `express-session` middleware package which is extended by `passport`
* `setupPassport`: Initializes `passport` setup

```typescript
// ./src/app.ts

...

import passport from "passport";
import { getOAuth2 } from "./util/OAuth2Strategy";

...

constructor(controllers: Controller[], port: number) {
  ...
  this.initDatabaseFile();
  this.initGlobalMiddlewares();
  this.initRoutes(controllers);
  ...
}

...

private setupPassport() {
  passport.use(getOAuth2());
  this.app.use(passport.initialize());
  this.app.use(passport.session());
  passport.serializeUser((user: Express.User, done) => {
    done(null, user);
  });
  passport.deserializeUser((user: Express.User, done) => {
    done(null, user);
  });
}

private initGlobalMiddlewares() {
  this.app.use(express.json());
  this.app.use(express.urlencoded({ extended: true }));
  this.app.use(
    expressSession({
      secret: uuid4(),
      resave: false,
      saveUninitialized: true,
    })
  );
  this.setupPassport();
}

...
```

### Handle the authorization and callback routes

The authorization and callback controllers are comparatively simple. Create two new controller files:

```bash
mkdir -p ./src/routes/auth;
mkdir -p ./src/routes/callback;
touch ./src/routes/auth/authController.ts
touch ./src/routes/callback/callbackController.ts
```

The `AuthController` handles authentication of the App via the previously described authorization flow. This is the third step of `passport` setup. Every controller class implements the controller interface which has two members: the path and the router.

This controller handles the `/auth` route, which is what we'll use to send users (via `passport`) to the Snyk website for authorization approval.

```typescript
// ./src/routes/auth/authController.ts

import type { Controller } from "../../interfaces/Controller";
import { Router } from "express";
import passport from "passport";

class AuthController implements Controller {
  // The base URL path for this controller
  public path = "/auth";
  // Express router for this controller
  public router = Router();

  constructor() {
    this.initRoutes();
  }

  /**
   * The /auth route is called to authenticate the App
   * via Snyk using passportjs authenticate method
   */
  private initRoutes() {
    this.router.get(`${this.path}`, passport.authenticate("snyk-oauth2"));
  }
}

export default AuthController;
```

Once a user approves authorization to our Snyk App via the Snyk website, they're kicked back to our callback URI, `/callback`. We'll handle this route similarly, invoking passport again. This is the final step of user authorization.

The `CallbackController` accepts requests on `/callback`, but also creates two sub-routes, `/callback/success` and `/callback/failure`, to handle the different possible outcomes it might receive from Snyk.

```typescript
// ./src/routes/callback/callbackController.ts

import type { Controller } from '../../interfaces/Controller';
import type { NextFunction, Request, Response } from 'express';
import { Router } from 'express';

export class CallbackController implements Controller {
  public path = '/callback';
  public router: Router = Router();

  constructor() {
    this.initRoutes();
  }

  private initRoutes() {
    // Path to handle the result of authentication flow or the callback/redirect_uri
    this.router.get(`${this.path}`, this.passportAuthenticate());
    // Path to handle success, same as what we pass to passport
    this.router.get(`${this.path}`, this.success);
    // Path to handle failure, same as what we pass to passport
    this.router.get(`${this.path}/failure`, this.failure);
  }

  private success(req: Request, res: Response, next: NextFunction) {
    // return res.render('callback');
    return res.send('SUCCESS!');
  }

  private failure(req: Request, res: Response, next: NextFunction) {
    // return next(new HttpException(401, 'Authentication failed'));
  }
}
```

Before we're done, we need to make sure we add a reference to our new controllers in our `index.ts`.

```typescript
// ./src/index.ts

import IndexController from "./routes/index/indexController";
import AuthController from "./routes/auth/authController";
import CallbackController from "./routes/callback/callbackController";
import App from "./app";

new App([
   new IndexController(),
   new AuthController(),
   new CallbackController()],
  3000
);
```

### Refresh token management

If we build and run our Snyk App at this point, hitting the `/auth` route will successfully jump us out to the Snyk authorization portal and, provided we confirm the authorization, we'll get kicked back to our local app's callback route at `/callback`. If we had a very simplistic, one-off use-case, we could end things here. But there's one more piece of the puzzle we should figure out if we're going to keep our user's authorization fresh, that thing is token expiry.

If you ran the app to test things, take a look at database entries. If you've been following along, you should see something like this:

```json
{
  "installs": [
    {
      "date": "2021-12-28T19:15:02.043Z",
      "userId": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
      "orgId": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
      "access_token": "xxxxxxxxxxxxxxxxxxxxxxxxxx",
      "expires_in": 3599,
      "scope": "apps:beta",
      "token_type": "bearer",
      "refresh_token": "yyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyy",
      "nonce": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
    },
  ]
}
```

That `expires_in` value will continue to countdown until 0. If it does, the user will need to re-authorize.

To keep our access token from going stale, we need to make a POST request using our `refresh_token` to get an updated `access_token` as described in the [Snyk Docs](https://docs.snyk.io/features/integrations/snyk-apps/getting-started-with-snyk-apps/set-up-the-refresh-token-exchange).

We can automate this process in our Snyk App by utilizing [Axios interceptors](https://axios-http.com/docs/interceptors) to _intercept_ the requests we make and ensure we have an up-to-date `access_token`.

Create the file `./src/util/interceptors.ts`, importing all the packages, classes, etc... that we'll need at the top:

```typescript
// ./src/util/interceptors.ts

import type { AxiosRequestConfig } from "axios";
import { AuthData } from "../interfaces/DB";
import { DateTime } from "luxon";
import { readFromDb, updateDb } from "./DB";
import { mostRecent } from "../routes/projects/projectsController";
import { EncryptDecrypt } from "./encrypt-decrypt";
import { refreshAuthToken } from "../util/APIHelpers";
import { ENCRYPTION_SECRET } from "../app";
import axios from "axios";
```

We'll add a total of three interceptors.

The first, `refreshTokenReqInterceptor`, will refresh the `auth_token` using the `refresh_token` when the `auth_token` expires. It takes an _AxiosRequestConfig_ request as an argument that can be used in the interceptor for additional checks.

```typescript
// ./src/util/interceptors.ts

...

export async function refreshTokenReqInterceptor(request: AxiosRequestConfig): Promise<AxiosRequestConfig> {
  // Read the latest data(auth token, refresh token and expiry)
  const db = await readFromDb();
  const data = mostRecent(db.installs);
  // If no data then continue with the request
  if (!data) return request;
  // Data used to calculate the expiry
  const expiresIn = data.expires_in;
  const createdDate = data.date;
  // Used npm library luxon to parse the date and calculate expiry
  const parsedCreateDate = DateTime.fromISO(createdDate.toString());
  const expirationDate = parsedCreateDate.plus({ seconds: expiresIn });
  // Check if expired
  if (expirationDate < DateTime.now()) {
    await refreshAndUpdateDb(data);
  }
  return request;
}
```

`refreshTokenRespInterceptor` will be used during request responses and only refresh/retry the token when the response being received is a 401 Unauthorized (this is what Passport returns when things go awry).

```typescript
// ./src/util/interceptors.ts

...

export async function refreshTokenRespInterceptor(error: AxiosError): Promise<AxiosError> {
  const status = error.response ? error.response.status: null;

  // Only refresh & retry the token on 401 Unauthorized, in case the access-token is
  //  invalidated before it expires, such as the signing key being rotated in an emergency.
  if (status === 401) {
    // Read the latest data(auth token, refresh token and expiry)
    const db = await readFromDb();
    const data = mostRecent(db.installs);
    // If no data then fail the retry
    if (!data) return Promise.reject(error);

    const newAccessToken = await refreshAndUpdateDb(data);

    // Use the new access token to retry the failed request
    error.config.headers['Authorization'] = `${data.token_type} ${newAccessToken}`;
    return axios.request(error.config);
  }

  return Promise.reject(error);
}
```

Lastly, `refreshAndUpdateDb` refreshes the access token for a given database record, and updates the database again before returning the newly refreshed token.

```typescript
// ./src/util/interceptors.ts

...

async function refreshAndUpdateDb(data: AuthData): Promise<string> {
  // Create a instance for encryption and decryption
  const eD = new EncryptDecrypt(process.env[Envars.EncryptionSecret] as string);
  // Make request to refresh token
  const { access_token, expires_in, refresh_token, scope, token_type } = await refreshAuthToken(
    eD.decryptString(data.refresh_token),
  );
  // Update the access and refresh token with the newly fetched access and refresh token
  // along with the expiry and other required info
  await updateDb(data, {
    ...data,
    access_token: eD.encryptString(access_token),
    expires_in,
    refresh_token: eD.encryptString(refresh_token),
    token_type,
    scope,
    date: new Date(),
  });

  return access_token;
}
```

With our interceptors defined, the only thing we need to do is update our `callSnykApi` function to utilize them. Interceptors are methods of the `axiosInstance` object, so we'll add them after the `axios.create()` call and before the function's `return`.

```typescript
// ./src/util/APIHelpers.ts
...

import {
  refreshTokenReqInterceptor,
  refreshTokenRespInterceptor,
} from "./interceptors";

...

export function callSnykApi(tokenType: string, token: string, version: APIVersion): AxiosInstance {

  ...

  axiosInstance.interceptors.request.use(
    refreshTokenReqInterceptor,
    Promise.reject
  );
  axiosInstance.interceptors.response.use(
    (response) => response,
    refreshTokenRespInterceptor
  );

  ...

}

...
```

## Wrap-up

If you've made it this far, congratulations! You've learned how to register a Snyk App with Snyk, configure the authorization flow, keep the `auth_token` from getting stale, and set up a great starting point using TypeScript!

In the next module of this tutorial, we'll add a template system and configure our app to show users all of their projects from Snyk in our App.
