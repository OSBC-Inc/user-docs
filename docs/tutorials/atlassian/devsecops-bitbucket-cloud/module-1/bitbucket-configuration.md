# Bitbucket 구성

## 앱 비밀번호 만들기

Snyk이 저장소에 액세스하고 Snyk의 [Bitbucket Cloud integration](https://support.snyk.io/hc/en-us/articles/360004032097-Bitbucket-Cloud-integration).을 활성화하도록 승인하려면 [앱 비밀번호를 생성](https://support.atlassian.com/bitbucket-cloud/docs/app-passwords/)해야 합니다.

앱 암호를 생성하려면:

1. 왼쪽 하단의 아바타에서 **Personal settings를** 클릭합니다.
2. **Access management**에서 **App passwords**를 클릭합니다.
3. **Create app password**를 클릭합니다.
4. 앱 암호에 암호를 사용할 응용 프로그램과 관련된 이름을 지정합니다.
5. 이 애플리케이션 암호에 부여하려는 특정 액세스 및 권한을 선택하십시오.
6. 생성된 암호를 복사하고 액세스 권한을 부여하려는 애플리케이션에 기록하거나 붙여넣습니다. **암호는 이번 한 번만 표시됩니다.**

다음 권한이 필요합니다:

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/bitbucket-api-token.png)

* Account: `read`
* Team membership: `read`
* Projects: `read`
* Repositories: `read and write`
* Pull requests: `read and write`
* Webhooks: `read and write`

## 리포지토리 변수

You will need to define [repository variables](https://support.atlassian.com/bitbucket-cloud/docs/variables-in-pipelines/#Repository-variables) at the repository level which will later be [referenced in your pipeline](https://support.atlassian.com/bitbucket-cloud/docs/variables-in-pipelines/).

나중에 [파이프라인에서 참조할](https://support.atlassian.com/bitbucket-cloud/docs/variables-in-pipelines/) 저장소 수준에서 [리포지토리 변수](https://support.atlassian.com/bitbucket-cloud/docs/variables-in-pipelines/#Repository-variables)를 정의해야 합니다.

이들은 다음으로 구성됩니다:

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/bitubucket-repo-vars.png)

1. 클러스터의 Amazon EKS 이름: `AWS_EKS_CLUSTER`
2. Snyk 계정 인증을 위한 Snyk API 토큰: `SNYK_TOKEN`
3. AWS Identity & Access Management AWS API와의 안전한 인증 상호 작용을 위한 사용자 [키 및 암호](https://docs.aws.amazon.com/IAM/latest/UserGuide/id\_credentials\_access-keys.html): `AWS_ACCESS_KEY_ID` 및 `AWS_SECRET_ACCESS_KEY`
4. 배포할 AWS 리전: `AWS_DEFAULT_REGION`
5. 저장소의 Amazon ECR [URL](https://docs.aws.amazon.com/AmazonECR/latest/userguide/Registries.html): `AWS_ECR_URI`
6. 컨테이너 이미지 이름: `IMAGE`

{% hint style="info" %}
계정을 생성할 때 [Snyk Service Accounets](https://support.snyk.io/hc/en-us/articles/360004037597-Service-accounts) 및 [AWS IAM 모범 사례](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html)를 사용하는 것이 좋습니다.
{% endhint %}
