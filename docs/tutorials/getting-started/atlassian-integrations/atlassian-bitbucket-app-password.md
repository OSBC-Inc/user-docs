---
description: Snyk과 통합할 수 있도록 Bitbucket 애플리케이션 암호 설정
---

# Atlassian Bitbucket 앱 비밀번호

Snyk과 Atlassian Bitbucket을 통합하려면 Atlassian App Password가 필요합니다.

## 앱 비밀번호 만들기

저장소에 액세스하고 Snyk의 [Bitbucket Cloud 통합](https://support.snyk.io/hc/en-us/articles/360004032097-Bitbucket-Cloud-integration)을 활성화하려면 [앱 비밀번호를 만들어야 합니다.](https://support.atlassian.com/bitbucket-cloud/docs/app-passwords/)&#x20;

앱 비밀번호를 생성하려면 다음을 수행하십시오.

1. 우측 상단의 프로필에서 **Personal settings**를 클릭합니다.
2. **Access management**에서 **App passwords**를 클릭합니다.
3. **Create app password**를 클릭합니다.
4. 앱 비밀번호에 비밀번호를 사용할 애플리케이션과 관련된 이름을 지정합니다.
5. 이 애플리케이션 암호에 부여할 특정 액세스 및 권한을 선택합니다.
6. 생성된 비밀번호를 복사하여 액세스 권한을 부여하려는 애플리케이션에 기록하거나 붙여넣습니다. **비밀번호는 이번 한 번만 표시됩니다.**

다음 권한이 필요합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/bitbucket-api-token.png)

* Account: `read`
* Team membership: `read`
* Projects: `read`
* Repositories: `read` 및 `write`
* Pull requests: `read` 및 `write`
* Webhooks: `read` 및 `write`
