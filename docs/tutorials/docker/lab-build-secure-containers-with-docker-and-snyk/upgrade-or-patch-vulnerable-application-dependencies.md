---
description: 이제 애플리케이션을 구성하는 오픈 소스 구성 요소의 취약점을 찾아 수정하겠습니다.
---

# 취약한 애플리케이션 종속성 업그레이드 또는 패치

## 선택 사항: 취약한 종속성의 위험

취약한 오픈 소스 구성 요소가 실행 중인 애플리케이션에 도입하는 위험의 예를 보기 위해 이러한 취약성 중 하나를 악용할 것입니다. `exploits`폴더에는 많은 취약한 종속성에 대한 Exploit이 포함되어 있습니다.

실행 중인 애플리케이션에 대해 Exploit을 실행해 보겠습니다. 우리는 st 패키지의 Directory Traversal 취약점이 어떻게 민감한 정보 유출로 이어질 수 있는지 보여줄 것입니다. exploits 폴더로 이동하고 `st-exploits.sh` 파일을 소싱하여 시작합니다.

```
cd exploits && source st-exploits.sh
```

이렇게 하면 Exploit을 보여주기 위해 일련의 별칭이 설정됩니다. 아래에 나와 있습니다.

```
st1="curl $GOOF_HOST/public/about.html"

# Directory listing (not necessary)
st2="curl $GOOF_HOST/public/"

# Failed ../
st3="curl $GOOF_HOST/public/../../../"

# Exploit start
st4="curl $GOOF_HOST/public/%2e%2e/%2e%2e/%2e%2e/"

# Exploit full
st5="curl $GOOF_HOST/public/%2e%2e/%2e%2e/%2E%2E/%2e%2e/%2e%2e/%2e%2e/%2e%2e/%2e%2e/%2e%2e/%2e%2e/etc/passwd"
```

좋은 점은 `/etc/passwd` 파일의 유출된 내용을 볼 수 있는 `st4` 및 `st5`에 있습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/st-exploit.png)

이런. 또한 이것은 단지 하나의 예일 뿐입니다. 이 폴더에 있는 다른 Exploit을 가지고 놀아도 좋습니다. 샘플 애플리케이션은 매우 취약합니다(당분간!).

## 오픈 소스 취약점 수정을 시작하십시오!

Snyk에서 이 취약점과 종속성의 다른 취약점은 `package.json` 파일 아래에 표시됩니다. Snyk은 Pull Requests를 통해 수정을 가속화하여 종속성을 취약하지 않은 버전으로 업그레이드합니다.

{% hint style="info" %}
Dockerfile은 취약성이 적습니다! Snyk은 변경 후 자동으로 다시 테스트했습니다.
{% endhint %}

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-ossproject.png)

## Snyk UI의 취약점 수정

### Step 1: 취약점을 더 자세히 탐색 <a href="#step-1-explore-a-vulnerability-in-more-detail" id="step-1-explore-a-vulnerability-in-more-detail"></a>

`package.json` 프로젝트를 클릭하고 아래로 스크롤하여 [당사의 독점 우선 순위 점수](https://snyk.io/blog/snyk-priority-score/)에 따라 정렬된 취약점 목록을 확인합니다. 각 취약점에 대해 Snyk은 다음을 표시합니다.

* 이를 도입한 모듈과 전이적 종속성의 경우 직접 종속성.
* 경로 및 제안된 수정 사항, 특정 취약 기능에 대한 세부 정보.

첫 번째 취약성인 지퍼 슬립부터 시작하겠습니다. 순서가 가장 높기 때문입니다. **zip-slip**에 대한 익스플로잇은 패치를 적용하기 전에 사용해 보고 싶은 경우 `exploits` 폴더에서도 사용할 수 있습니다.

![](https://gblobscdn.gitbook.com/assets%2F-M3ww0VUnNWDc-FwnwVl%2F-MOHOD925AinvVslRYnk%2F-MOHQWZMgK6Br-LeO6xL%2FSnyk-Vuln.png?alt=media\&token=42d70198-322b-463e-b107-f54c12072ec7)

### Step 2: Snyk에서 Fix Pull Request 생성 <a href="#step-2-create-a-fix-pull-request-in-snyk" id="step-2-create-a-fix-pull-request-in-snyk"></a>

수정 사항을 사용할 수 있으므로 Snyk는 Pull Request를 통해 취약한 종속성을 취약하지 않은 버전으로 자동 업그레이드할 수 있습니다. 그렇게 하려면 "Fix this vulnerability"을 클릭하십시오.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-fixvuln.png)

다음 화면에서 이 PR로 해결할 문제를 확인할 수 있습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-fixpropen.png)

좋아 보입니다! 계속해서 PR을 엽니다. 준비가 되면 GitHub의 PR로 이동하여 파일 diff 보기에서 변경 사항을 검토할 수 있습니다:

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-prdiff.png)

이제 PR을 병합하십시오! Snyk로 돌아가서 `package.json` 파일에 High Severity Vulnerability가 1개 적다는 것을 알 수 있습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-postfixpr.png)

zip-slip Exploit을 시도한 경우 코드를 `git pull`하여 GitHub로 로컬 복사본을 최신 상태로 만들고 Exploit을 다시 시도하세요. 더 이상 작동하지 않는다는 것을 알 수 있습니다.

## Snyk으로 로컬에서 취약점 수정

Fix Pull Requests는 개별 취약점을 수정하는 데 유용하며 Snyk는 취약점에 대한 새로운 수정 사항이 게시될 때 [Pull Requests를 자동으로 열 수 있습니다](https://support.snyk.io/hc/en-us/articles/360006581898-Upgrading-dependencies-with-automatic-PRs). 취약점을 수동으로 수정할 수도 있습니다.

위에서 설명한 `st` 패키지 익스플로잇을 사용합니다. Snyk의 문제 목록을 살펴보고 `Directory Traversal` 취약점을 찾습니다. `st`를 버전 `0.2.5`로 업데이트하면 이 문제가 해결됩니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-fixstvuln.png)

package.json 파일에서 이 변경을 수행하십시오.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/st-fixvuln.png)

이를 악용할 수 없도록 컨테이너를 다시 빌드하고 Kubernetes에 재배포합니다.

```
# Build the new image
docker build $DockerId/goof:dev .

# Push to Docker Hub
docker push $DockerId/goof:dev

# Scale the deployment down and up
kubectl scale deployment goof --replicas=0
kubectl scale deployment goof --replicas=1
```

이제 Exploit을 다시 시도하십시오. 그것은 훌륭하게 실패해야합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/post-stfix.png)

## 선택 사항: 학습한 내용을 사용하여 모든 취약성을 수정합니다.

Fix Pull Requests를 사용하거나 Snyk의 정보를 사용하여 패키지 관리자 매니페스트를 수정하고 수정 사항이 있는 High Severity Vulnerabilities를 제거할 때까지 취약성을 계속 수정하십시오.

도움이 될 수 있는 몇 가지 추가 리소스:

* Snyk IDE Plugins: JetBrains IDE, Eclipse 또는 VS Code를 사용하는 경우 IDE 내에서 바로 취약성을 표시하고 정보를 수정하는 [플러그인](https://support.snyk.io/hc/en-us/sections/360001138118-IDE-tools)을 확인하세요.
* 이와 같은 노드 응용 프로그램의 경우 [Snyk Wizard](https://support.snyk.io/hc/en-us/articles/360003851357-Manage-vulnerability-results-with-the-Snyk-CLI-wizard)를 확인하십시오!

준비가 되면 다음 섹션으로 계속 진행하여 애플리케이션을 배포하는 Kubernetes 매니페스트의 구성 문제를 수정하는 방법을 알아보세요!
