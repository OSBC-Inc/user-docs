# Snyk에 연결

구성의 이 단계에서 인증하라는 메시지가 표시됩니다. Snyk은 인증을 위해 다음 ID 공급자를 지원합니다.

* GitHub
* Bitbucket
* Google
* Azure
* Single sign-on (SSO)

인증에 대한 추가 세부 정보는 [설명서](../../../features/user-and-group-management/authentication/) 페이지에서 찾을 수 있습니다.

{% hint style="info" %}
이 통합은 **무료**라는 점을 강조하는 것이 중요합니다! 귀하의 추가 결제 없이 이 구성의 일부로 무료 계정 생성이 가능합니다.
{% endhint %}

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-codepipeline-07.png)

ID 공급자를 선택하면 앱 **승인**에 대한 확인 메시지를 받게 됩니다. 이것을 한 번 클릭하고 계속하십시오.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-codepipeline-08.png)

다음 단계는 통합 설정을 구성하는 것입니다. 여기에서 스캔 결과가 저장될 **Snyk 조직**과 **취약점 처리** 및 **심각도별**로 **배포를 차단**하는 임계값을 선택합니다. 이러한 설정은 특정 사용 사례 및 조직 정책에 따라 다릅니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-codepipeline-09.png)

For the purpose of this lab, however, we will not block deployments and click **Continue**.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-codepipeline-10.png)

Click **Confirm** to complete the authorization request.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-codepipeline-11.png)

You will notice a confirmation that the connection was successfully established and at this point can click on **Done**.

If at any point in time, you need to revoke the authorization, you can do so by [logging into Snyk](https://app.snyk.io/) and clicking **Revoke** from the list of **Authorized Applications** under **Account Settings** as shown below.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-codepipeline-12.png)

Finally, let's confirm our selections and click **Save** to complete our pipeline configuration.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-codepipeline-13.png)

...and acknowledge the changes.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-codepipeline-14.png)

Let's move on!
