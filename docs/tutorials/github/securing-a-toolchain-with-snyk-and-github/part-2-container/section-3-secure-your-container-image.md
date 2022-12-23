# Section 3: Container 이미지 보호

이전 Section에서는 Snyk이 컨테이너와 함께 사용하여 한 번에 여러 취약점을 해결할 수 있는 다른 기본 이미지를 제공하는 방법을 살펴보았습니다. 이 Section에서는 컨테이너에 대해 보다 안전한 기본 이미지를 선택합니다. 시작하겠습니다!

## Step 1: GitHub에서 Dockerfile 수정

GitHub에서 저장소로 이동하고 Dockerfile을 클릭하여 엽니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-container-opendockerfile.png)

Edit 아이콘을 클릭하여 GitHub Web Editor를 엽니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-container-dockerfileedit.png)

Dockerfile에서 이전 `FROM` 문을 주석 처리(또는 삭제)하고 Snyk 권장 사항 목록에서 새 문을 추가합니다. 이 예에서는 `node:14-stretch`를 사용합니다. Dockerfile은 이제 다음과 같아야 합니다.

```
#FROM node:6-stretch
FROM node:14-stretch

RUN mkdir /usr/src/goof
RUN mkdir /tmp/extracted_files
COPY . /usr/src/goof
WORKDIR /usr/src/goof

RUN npm update
RUN npm install
EXPOSE 3001
EXPOSE 9229
ENTRYPOINT ["npm", "start"]
```

{% hint style="danger" %}
이것은 교육적인 예입니다. 애플리케이션에서 Node 6에서 Node 14로 업그레이드하는 것이 항상 작동하는 것은 아닙니다. 이 실습 외부에서는 기본 이미지를 선택할 때 애플리케이션과 해당 종속성을 이해해야 합니다. 이와 같은 버전을 건너뛸 때 작동이 보장되지 않기 때문입니다.
{% endhint %}

변경 사항을 Commit할 준비가 되면 이 Commit에 대한 **새 Branch**를 생성하고 `Dockerfile`에 대한 변경 사항을 제안하는 옵션을 선택합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-container-baseimagebranch.png)

다음 보기에서 계속 진행하여 Pull Request를 생성합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-container-baseimagepr.png)

## Step 2: CI 작업이 성공적으로 완료되었는지 확인

Pull Request 보기에서 `build-container` 확인이 성공적으로 완료되었는지 확인하여 애플리케이션과 컨테이너가 새 기본 이미지 위에 성공적으로 빌드되는지 확인하십시오.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-container-baseimageprchecks.png)

준비가 되면 Pull Request를 Merge하여 변경 사항을 `develop`에 적용하고 완료되면 `replace-base-image` Branch를 삭제합니다.

## Step 3: 새로운 Vulnerability Scan 결과 검토

With our new Base Image in place, we can review the vulnerability scan results from Snyk Container once again to see what vulnerabilities we have left to triage in our container image.

### GitHub Security Code Scanning

You can review vulnerability counts in GitHub Security Code Scanning, as shown in the previous section.

{% hint style="warning" %}
Results in Security Code Scanning take time to update. You won't see updated vulnerability counts until the CI Workflow completes after code has been merged into `develop`.
{% endhint %}

### Snyk UI

In the Snyk UI, the results for the Dockerfile update automatically once the changes are merged into the default working branch. We can see that simply by changing the base image we used, we went from 836 issues to 307! Now we only have 35 high severity vulnerabilities to triage, as opposed to the 203 from before.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-container-newbasevulns%20\(1\).png)

## Step 4: Merge the changes to PROD

We have outstanding vulnerabilities to take care of, but we need to push our changes to PROD in order to sustain the pace of delivery. We feel good about what we push to PROD, since it's a best effort progressing delivery while keeping the workload secure.

Let's open a PR from `develop` to `PROD` to check in our work for the day.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-container-prprod.png)

Once all checks pass, go ahead and merge the PR. Hooray! Our container is now PROD-ready!

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-container-prodchecks.png)

#### Wait a minute, what about our Snyk Gate?

In Part 1, we added a Snyk gate that prevents high-severity vulnerabilities from entering our PROD branch, so why can we merge to PROD even though high severity vulnerabilities are present?

In short, we opted to not add container vulnerabilities to the Snyk gate. It still evaluates application vulnerabilities, but in order to not overburden our developers, we opted to not implement it for our container base image.

## Recap & Next Steps

In this Lab we containerized our sample application and ensured we're using the most secure base image available that's compatible with our application. We ensured, with our CI workflows, that the base image recommended by Snyk is compatible with our application.

We also saw how results from Snyk Container can be consumed directly in the GitHub UI using their Security Code Scanning functionality. This allows developers to access Snyk vulnerability information without leaving GitHub's UI.

In the next section, we take our application, and our security testing, a step further by introducing the files that will allow us to deploy this container to an orchestrated environment. When ready to start playing with Snyk Infrastructure as Code, proceed to Part 3!
