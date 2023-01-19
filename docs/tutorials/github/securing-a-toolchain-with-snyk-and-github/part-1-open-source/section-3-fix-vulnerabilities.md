---
description: >-
  보안 게이트가 설치되고 위험에 대해 경고하는 경우 개발 Branch에서 문제를 수정하여 수정 사항을 PROD Branch로 다운스트림할 수
  있습니다.
---

# Section 3: 취약점 수정

Section 1에서 구성한 GitHub Integration을 통해 Snyk은 Pull Request를 열어 종속성을 취약하지 않은 버전으로 업그레이드하여 수정을 가속화할 수 있습니다.

## Step 1: 취약점을 더 자세히 탐색

Snyk에 로그인하고 이전에 가져온 `gh-actions-academy` 프로젝트로 이동합니다. 아래로 스크롤하여 당사의 독점 우선 순위 점수에 따라 정렬된 존재하는 취약점 목록을 확인하십시오. 각 취약점에 대해 Snyk은 다음을 표시합니다:

* 이를 도입한 모듈 및 전이적 종속성의 경우 직접 종속성.
* 경로 및 제안된 수정 사항, 특정 취약 기능에 대한 세부 정보.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-vuln.png)

## Step 2: Fix Pull Request in Snyk 생성

GitHub 통합을 사용할 때 수정 사항이 있는 경우 Snyk는 Pull Request를 통해 취약한 종속성을 취약하지 않은 버전으로 자동 업그레이드할 수 있습니다. 그렇게 하려면 "Fix this vulnerability"을 클릭하십시오.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-fixvuln.png)

다음 화면에서 이 PR로 해결할 문제를 확인할 수 있습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-prconfirm.png)

좋아 보입니다! 계속해서 PR을 엽니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-propen.png)

준비가 되면 GitHub의 PR로 이동하여 파일 diff 보기에서 변경 사항을 검토할 수 있습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-prdiff.png)

CI 검사가 성공적으로 완료된 것을 확인하여 브레이킹 체인지를 도입하지 않았음을 확인합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-prchecks.png)

이제 PR을 Merge하십시오! Branch를 삭제할 수도 있습니다. Snyk으로 돌아가서 `package.json` 파일에 높은 심각도 취약점이 1개 적다는 것을 알 수 있습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-postpr.png)

## Step 3: 나머지 취약점 수정

다른 Pull Request를 통해 깨끗한 `develop` Branch를 빠르게 추적해 봅시다. 이번에는 `all-fixes` Branch에서 `develop`으로 이동합니다.

### 깨끗한 Branch에 도착한 방법

`all-fixes` Branch는 `develop` Branch에 대해 [Snyk Wizard](https://support.snyk.io/hc/en-us/articles/360003851357-Manage-vulnerability-results-with-the-Snyk-CLI-wizard)를 사용하여 생성되었습니다. 이 작업을 직접 수행하려면 저장소를 워크스테이션에 `git clone`하고 이에 대해 snyk Wizard를 실행하십시오. 워크숍을 계속할 수 있도록 변경 사항을 새 Branch로 Push하는 것이 좋습니다.

### Pull Request를 여세요!

`develop`할 `all-fixes`에서 새 Pull Request을 만듭니다. 이것은 몇 가지 변경 사항을 소개합니다.

* `Snyk Wizard`가 만든 변경 사항을 추적하는 데 사용되는 `.snyk` 파일 생성.
* 업데이트된 종속성으로 `package.json` 및 `package-lock.json` 파일이 업데이트되었습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-allfixpr.png)

변경 사항 비교 보기에서 이러한 변경 사항을 탐색하여 자세히 알아볼 수 있습니다. 준비가 되면 Pull Request 생성 및 Merge를 완료합니다.

## Step 4: Step 2에서 생성한 PR을 다시 방문

Section 2의 Pull Requests를 열어 둔 경우 Pull Requests 탭에서 다시 방문할 수 있습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-postfixes.png)

Workflow가 다시 실행되면 이번에는 Snyk Security 게이트 및 CI 작업이 성공적으로 완료되어야 합니다.

{% hint style="warning" %}
오픈 소스 취약점은 매일 공개됩니다. Snyk Gate가 실패하면 이 글이 작성된 이후로 하나 이상의 새로운 높은 심각도 취약점이 공개되었습니다. 이 경우 위의 1단계와 2단계를 반복하여 나머지 문제를 수정하는 Pull Request를 엽니다.
{% endhint %}

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-postfixchecks.png)

변경 사항을 Merge하고 PROD Branch에 오픈 소스 취약점이 없음을 확인하십시오! 🏆

Part 1의 끝까지 왔습니다! 축하합니다! Part 2로 이동하여 Snyk Container가 컨테이너에 패키징할 때 이 애플리케이션을 안전하게 유지하는 데 어떻게 도움이 되는지 알아보십시오.
