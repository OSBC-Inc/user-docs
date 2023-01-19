# Send Message

마지막으로 **Action**을 만들고 이름을 **Send Channel Message in Microsoft Teams**로 지정합니다:

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/zappier-teams-main.png)

**Microsoft Teams** 앱에 대한 **Send Channel Message**를 선택합니다:

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/zappier-teams-channel.png)

Microsoft Teams 계정 선택:

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/zappier-teams-account.png)

채널을 선택하고 **Message Text Format**에 대해 **Markdown**을 선택합니다:

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/zappier-teams-setup.png)

다음 스니펫을 복사하여 **Message Text** 필드에 붙여넣습니다.

```markup
# New Issue
We found vulnerabilities that affect [{{project__name}}]({{project__browseUrl}}) project in the [{{org__name}}]({{org__url}}).

## Details:
<div class="issue">
  <p>{{newIssues}}</p>
</div>
```

{% hint style="info" %}
Payload에서 매핑된 필드와 일치하도록 필드를 적절하게 업데이트해야 합니다.
{% endhint %}

작업을 테스트합니다:

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/zappier-teams-test.png)
