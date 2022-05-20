# Webhook tutorial

{% hint style="info" %}
**공식** Snyk API는 [https://snyk.docs.apiary.io/#](https://snyk.docs.apiary.io)에서 구할 수 있습니다.
{% endhint %}

## 통합 예시

우선 [Zapier](https://zapier.com)에서 새 Zap을 생성해야 합니다.

### 트리거

요청 헤더에 액세스하려면 **"Catch Raw Hook"** 트리거를 만들어야 합니다. 요청 페이로드가 문자열로 제공된다는 단점이 있으며 이를 JSON으로 파싱해야 합니다.

![](<../../../.gitbook/assets/spaces\_-MdwVZ6HOZriajCf5nXH\_uploads\_git-blob-6540b1e64ce63e413bb1b4d68515d08d7f63ef3b\_untitled (1).png>)

요청을 보낼 수 있는 경우 Webhook URL을 제공합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/untitled-1%20\(1\).png)

제공된 URL이 있는 API를 통해 Snyk에서 Webhook을 생성해야 합니다.

```
POST /api/v1/org/{orgId}/webhooks HTTP/2
> Host: snyk.io
> Authorization: token {authToken}
> Content-Type: application/json
| {
|   "url": "https://hooks.zapier.com/hooks/catch/9002958/oemlgkz/",
|   "secret": "my-secret-string"
| }
```

API는 거의 생성된 Webhook으로 응답합니다.

```
< HTTP/2 200 
< Content-Type: application/json
| {
|   "id": "{webhookId}",
|   "url": "https://hooks.zapier.com/hooks/catch/9002958/oemlgkz/",
| }
```

Zapier's trigger를 테스트하기 위해 webhook을 호출할 수 있습니다.

```
> POST /api/v1/org/{orgId}/webhooks/{webhookId}/ping HTTP/2
> Host: snyk.io
> Authorization: token {authToken}
> Content-Type: application/json
```

list 및 map 필드에서 ping 요청을 선택할 수 있습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/untitled-2%20\(1\).png)

### Action (payload 확인)

payload를 검증하려면 JS Action을 생성해야 합니다.

**"Code by Zapier" → "Run Javascript"**

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/untitled-3%20\(1\).png)

우리는 `headers['X-Hub-Signature']`와 페이로드 문자열을 스니펫 변수에 매핑해야 한다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/untitled-4%20\(1\).png)

다음 스니펫에서는 `isValid: boolean`을 Zap의 필드에 소개합니다.s.

{% hint style="info" %}
Replace `my-secret-string` string with a webhook's secret string.
{% endhint %}

```javascript
const crypto = require('crypto');
const secret = "my-secret-string";

function makeSignature(body, secret) {
  const hmac = crypto.createHmac('sha256', secret);
  hmac.update(body, 'utf8');

  return `sha256=${hmac.digest('hex')}`;
}

try {
  const body = JSON.parse(inputData.body);
  const { project, org, group, newIssues } = body;

  output = { 
    isValid: inputData.signature === makeSignature(inputData.body, secret)
  };
} catch (err) {
  output = { isValid: false, err: err.message };
}
```

스니펫을 테스트합니다. `isValid === true`인지 확인하십시오.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/untitled-5%20\(1\).png)

### Action (payload 파싱)

Zapier가 이해할 수 있는 문자열에서 payload를 파싱하는 다른 작업을 만들어 보겠습니다.

동일한 JS Action을 생성해야 합니다.

**"Code by Zapier" → "Run Javascript"**는 다음과 같은 필드 매핑을 포함합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/untitled-6%20\(1\).png)

다음과 같은 JS snippet이 있습니다.

```
try {
  output = JSON.parse(inputData.body);
} catch (err) {
  output = { err: err.message };
}
```

request payload를 분석하여 Zap의 변수에 매핑합니다.

### Action (issues 형식)

새로운 이슈들이 오브젝트 목록으로 제공되는데, 안타깝게도 Zapier는 그 형식을 잘 이해하지 못하고 오히려 문자열 목록을 좋아합니다. 따라서 `newIssues`를 `string[]`로 변환해야 합니다.

JS Action을 하나 더 만들어 보겠습니다.

**"Code by Zapier" → "Run Javascript"**를 실행하고 다음 스니펫을 붙여넣습니다.

```
function formatIssue({ pkgName, pkgVersions, issueData }) {
  return `
  <a href="${issueData.url}">${issueData.title}</a><br/>
  Vulnerability in ${pkgName} (${pkgVersions.join(', ')}). ${issueData.severity} severity.
`;
}

try {
  const { newIssues, ...body } = JSON.parse(inputData.body);

  output = { ...body, newIssues: newIssues.map(formatIssue) };
} catch (err) {
  output = { newIssues: [], err: err.message };
}
```

### Action (filter)

이제 제공되는 모든 필드를 사용하여 이벤트와 관련하여 원하는 모든 작업을 결정할 수 있습니다.

필터링하려면 **"Filter by Zapier"** 앱을 만들어야 합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/untitled-7%20\(1\).png)

이제 필터링할 방법을 선택할 수 있습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/untitled-8%20\(1\).png)

### Action (notification 전송)

위의 작업을 통해 필요한 모든 필드에 액세스할 수 있으며 notification template을 작성할 수 있습니다. 다음 경우에는 이메일을 활용한 방법을 안내합니다. 다른 방법으로도 진행이 가능합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/untitled-9%20\(1\).png)

### Result

알림은 다음과 같습니다.
