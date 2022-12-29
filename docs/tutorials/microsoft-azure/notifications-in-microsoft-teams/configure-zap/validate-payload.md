# Validate Payload

다음으로 다른 **Action**을 추가하고 이름을 **Validate payload**로 지정합니다:

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/zappier-validate-payload-main.png)

**Action Event**를 **Run Javascript**으로 정의해 보겠습니다:

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/zappier-validate-payload-script.png)

아래와 같이 **body**와 **signature**를 포함하도록 작업을 구성합니다:

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/zappier-validate-payload-setup.png)

**Code** section에서 다음 스니펫을 복사하여 붙여넣습니다:

```javascript
const crypto = require('crypto');
const secret = "your_secret";

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

Action을 테스트 합니다:

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/zappier-validate-payload-test.png)
