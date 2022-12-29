# Parse Payload

다음으로 다른 작업을 추가하고 이름을 **Parse payload**로 지정합니다:

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/zappier-parse-payload-main.png)

**Action Event**로 **Run Javascript**을 선택합니다:

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/zappier-parse-payload-script.png)

아래와 같이 **Input Data** 아래에 **body**를 추가해야 합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/zappier-parse-payload-setup.png)

**Code** 필드에 다음 스니펫을 복사하여 붙여넣습니다.

```javascript
try {
    output = JSON.parse(inputData.body);
} catch (err) {
    output = { err: err.message };
}
```

작업을 테스트합니다:

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/zappier-parse-payload-test.png)
