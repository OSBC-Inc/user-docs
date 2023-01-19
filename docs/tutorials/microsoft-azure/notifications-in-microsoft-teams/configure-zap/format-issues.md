# Format Issues

다음으로 다른 작업을 만들고 이름을 **Format issues**로 지정합니다:

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/zappier-format-issues-main.png)

**Action Event**로 **Run Javascript**을 선택합니다:

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/zappier-format-issues-script.png)

**Input Data** section에 **body**를 추가해야 합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/zappier-format-issues-setup.png)

스니펫을 복사하여 **Code**필드에 붙여넣기:

```javascript
function formatIssue({ pkgName, pkgVersions, issueData }) {
    return `
    <a href="${issueData.url}">${issueData.title}</a><br/>
    Vulnerability in ${pkgName} (${pkgVersions.join(', ')}). ${issueData.severity} severity.
    `;
}

try {
    const { newIssues } = JSON.parse(inputData.body);
    output = { newIssues: newIssues.map(formatIssue) };
} catch (err) {
    output = { newIssues: [], err: err.message };
}
```

작업을 테스트합니다:

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/zappier-format-issues-test.png)
