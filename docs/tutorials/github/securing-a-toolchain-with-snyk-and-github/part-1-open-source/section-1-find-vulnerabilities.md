---
description: Fork된 Goof 저장소를 Snyk 계정으로 가져와 취약점을 스캔하는 것으로 시작하겠습니다.
---

# Section 1: 취약점 찾기

## Step 1: Snyk의 GitHub Integration 구성

{% hint style="info" %}
Snyk GitHub Integration을 이미 구성한 경우 Step 2 로 계속 진행합니다.
{% endhint %}

먼저 저장소를 가져올 수 있도록 Snyk을 GitHub에 연결해야 합니다. 다음과 같이 하십시오.

1. Snyk.io에 로그인합니다. 아직 [가입](https://snyk.co/SnykGH)하지 않았다면 가입하세요.
2. Integrations -> Source Control -> GitHub로 이동 합니다.
3. Account Credentials을 입력하여 GitHub 계정을 연결하세요.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-gh.png)

## Step 2: Fork된 Goof 저장소를 Snyk으로 가져오기

이제 Snyk이 GitHub 계정에 연결되었으므로 저장소를 Snyk에 프로젝트로 가져옵니다.

1. Projects로 이동합니다.
2. "Add Project"를 클릭한  다음 "GitHub"를 선택합니다.
3. Fork한 저장소를 클릭합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-ghimport.png)

## Step 3: 저장소의 위험 탐색

저장소를 가져올 때 Snyk은 Goof 애플리케이션의 오픈 소스 구성 요소가 선언된 package.json 파일을 찾았습니다. 31개의 높은 심각도를 포함하여 60개의 취약점이 포함되어 있음을 알 수 있습니다! 😳

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-projvulns.png)

취약성 수정을 시작하기 전에 `PROD` Branch에 프로덕션 준비 버전의 코드가 포함되어 있음을 기억하십시오. 다음 섹션에서는 "stop the bleeding"하도록 설계된 Snyk Gate를 구현하여 새로운 취약점이 해당 Branch에 침투하는 것을 방지합니다.
