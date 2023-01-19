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

새로운 기본 이미지가 있으면 Snyk Container의 취약성 스캔 결과를 다시 한 번 검토하여 컨테이너 이미지에서 분류해야 할 취약성이 무엇인지 확인할 수 있습니다.

### GitHub Security Code Scanning

이전 section에 표시된 대로 GitHub Security Code Scanning에서 취약성 수를 검토할 수 있습니다.

{% hint style="warning" %}
Results in Security Code Scanning take time to update. You won't see updated vulnerability counts until the CI Workflow completes after code has been merged into `develop`.
{% endhint %}

### Snyk UI

Snyk UI에서 변경 사항이 기본 작업 Branch에 Merge되면 Dockerfile에 대한 결과가 자동으로 업데이트됩니다. 우리가 사용한 기본 이미지를 변경하기만 하면 836개 문제에서 307개 문제로 줄어든 것을 볼 수 있습니다! 이제 우리는 이전의 203개와 달리 35개의 심각도가 높은 취약점만 선별할 수 있습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-container-newbasevulns%20\(1\).png)

## Step 4: 변경 사항을 PROD에 Merge

처리해야 할 뛰어난 취약점이 있지만 전달 속도를 유지하려면 변경 사항을 PROD로 푸시해야 합니다. workload를 안전하게 유지하면서 전달을 진행하는 최선의 노력이기 때문에 우리가 PROD에 Push하는 것에 대해 기분이 좋습니다.

오늘의 작업을 확인하기 위해 `develop`에서 `PROD`로 PR을 열어 봅시다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-container-prprod.png)

모든 확인이 통과되면 계속 진행하여 PR을 Merge합니다. 만세! 우리의 컨테이너는 이제 PROD 준비가 되었습니다!

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-container-prodchecks.png)

#### 잠깐, Snyk Gate는 어떻습니까?

Part 1에서 심각도가 높은 취약점이 PROD Branch에 진입하지 못하도록 하는 Snyk 게이트를 추가했는데 심각도가 높은 취약점이 있는데도 PROD에 Merge할 수 있는 이유는 무엇입니까?

즉, Snyk 게이트에 컨테이너 취약성을 추가하지 않기로 했습니다. 여전히 애플리케이션 취약성을 평가하지만 개발자에게 과도한 부담을 주지 않기 위해 컨테이너 기본 이미지에 대해 구현하지 않기로 결정했습니다.

## 요약 및 다음 단계

이 실습에서는 샘플 애플리케이션을 컨테이너화하고 애플리케이션과 호환되는 가장 안전한 기본 이미지를 사용하고 있는지 확인했습니다. CI Workflow를 통해 Snyk에서 권장하는 기본 이미지가 애플리케이션과 호환되는지 확인했습니다.

또한 보안 코드 스캔 기능을 사용하여 Snyk Container의 결과를 GitHub UI에서 직접 사용할 수 있는 방법도 확인했습니다. 이를 통해 개발자는 GitHub의 UI를 벗어나지 않고도 Snyk 취약성 정보에 액세스할 수 있습니다.

다음 section에서는 이 컨테이너를 오케스트레이션된 환경에 배포할 수 있게 해주는 파일을 도입하여 응용 프로그램과 보안 테스트를 한 단계 더 진행합니다. Snyk Infrastructure as Code를 사용할 준비가 되면 Part 3로 진행하십시오!
