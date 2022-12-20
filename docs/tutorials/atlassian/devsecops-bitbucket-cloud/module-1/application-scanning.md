# Application Scanning

## 배경

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-opensource-01.png)

오픈 소스 종속성의 취약점에 대한 애플리케이션 스캔은 소스에서 시작됩니다. 이전에 Bitbucket에 Snyk 통합을 활성화하고 첫 번째 프로젝트를 가져왔을 때 [packages.json](https://bitbucket.org/snyk/patterns-library-atlassian-aws/src/master/app/goof/package.json)을 기반으로 한 취약점 수와 각각에 대한 자세한 정보를 확인했습니다.

Snyk에서 결과를 검토하면 취약성에 대한 심각도 및 익스플로잇 성숙도와 같은 컨텍스트를 받을 수 있습니다. 다음과 같은 강력한 기능도 제공됩니다:

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-vuln-details.png)

* 직접 종속성을 업그레이드하거나 취약성을 패치하여 취약성을 수정하는 데 도움이 되도록 [풀 요청을 수정](https://support.snyk.io/hc/en-us/articles/360003891038-Fix-your-vulnerabilities)하십시오.
* 수정 사항의 우선 순위를 효과적으로 지정하는 데 도움이 되는 [우선 순위 점수.](https://snyk.io/blog/snyks-developer-first-prioritization-capabilities/) 1-1000 범위의 점수는 [CVSS](https://www.first.org/cvss/) 점수, 알려진 익스플로잇, 취약점이 얼마나 새로운지, 도달 가능한지 여부를 수정합니다.
* [Jira integration](https://snyk.io/blog/jira-integration/)을사용하면 Jira에서 문제를 만들 수 있습니다.

## 파이프라인에서 애플리케이션 스캐닝

[bitbucket-pipelines.yml](https://bitbucket.org/snyk/patterns-library-atlassian-aws/src/192a4d2412a4330b9f634e9d45a546ec1add61fb/bitbucket-pipelines.yml#lines-15:30) 파일은 Pipelines 빌드 구성을 정의합니다. Pipelines를 처음 사용하는 경우 [여기](https://support.atlassian.com/bitbucket-cloud/docs/get-started-with-bitbucket-pipelines/)에서 시작하는 방법에 대해 자세히 알아볼 수 있습니다.

이 워크숍에서는 워크플로에 매핑된 개별 단계가 포함된 샘플 [bitbucket-pipelines.yml](https://bitbucket.org/snyk/patterns-library-atlassian-aws/src/192a4d2412a4330b9f634e9d45a546ec1add61fb/bitbucket-pipelines.yml#lines-15:30) 파일을 제공했습니다. 애플리케이션을 스캔하고, Docker 이미지를 빌드하고, 컨테이너 이미지를 스캔한 다음 애플리케이션을 Kubernetes 클러스터에 배포합니다. 애플리케이션 검색 단계를 자세히 살펴보겠습니다:

```yaml
scan-app: &scan-app
  - step:
      name: "Scan open source dependencies"
      caches:
        - node
      script:
        - pipe: snyk/snyk-scan:0.4.3
          variables:
            SNYK_TOKEN: $SNYK_TOKEN
            LANGUAGE: "npm"
            PROJECT_FOLDER: "app/goof"
            TARGET_FILE: "package.json"
            CODE_INSIGHTS_RESULTS: "true"
            SEVERITY_THRESHOLD: "high"
            DONT_BREAK_BUILD: "true"
            MONITOR: "false"
```

이 예에서는 파이프라인의 [Snyk Scan](https://bitbucket.org/product/features/pipelines/integrations?p=snyk/snyk-scan) 파이프를 활용하여 애플리케이션 스캔을 수행합니다. [소스](https://bitbucket.org/snyk/snyk-scan)에는 지원되는 모든 변수의 완전한 YAML 정의가 포함되어 있지만 이 스니펫에 포함된 항목만 우리의 목적에 필요합니다.

다음 중 몇 가지를 자세히 살펴보겠습니다:

1. `SNYK_TOKEN`은 **Bitbucket Configuration** 모듈에서 이전에 정의된 리포지토리 변수로 파이프에 전달되고 있습니다.
2. `PROJECT_FOLDER`는 프로젝트가 있는 폴더이며 일반적으로 기본값은 `.`.이지만 이 예에서는 app/goof로 설정하고 이를 파이프라인의 다른 단계에 [아티팩트](https://support.atlassian.com/bitbucket-cloud/docs/use-artifacts-in-steps/)로 전달하고 있습니다.
3. `CODE_INSIGHTS_RESULTS`의 기본값은 false입니다. 그러나 [Snyk 테스트 결과로 Code Insight 보고서를 생성](https://snyk.io/blog/enhanced-security-for-bitbucket-cloud-development/)하려고 하므로 이를 true로 설정했습니다.
4. `SEVERITY_THRESHOLD`는 제공된 수준 이상인 문제를 보고합니다. 기본값은 낮지만 우리의 경우에는 `high`에만 관심이 있으므로 그에 따라 이 변수를 정의했습니다.
5. `DONT_BREAK_BUILD` 기본값은 `false`이며 예상할 수 있습니다. 정상적인 상황에서 찾은 문제가 발생하면 빌드를 중단하고 싶을 것입니다. 그러나 이 학습 연습의 목적을 위해 이를 `true`로 설정합니다.

{% hint style="info" %}
풀 리퀘스트에서 **Snyk 보안 스캔**을 실행하고 [Atlassian Marketplace의 새로운 Snyk Security Connect 앱을 통해](https://marketplace.atlassian.com/apps/1222359/snyk-for-bitbucket-cloud?hosting=cloud\&tab=overview\&utm\_source=partner\&utm\_medium=comarketing\&utm\_campaign=P:marketplace%7CO:ecosystem%7CF:awareness%7CC:campaign%7CH:fy20q4%7CI:synk-bbc%7C) **Code Insights**에서 결과를 볼 수 있습니다. 시작하기 쉽고 몇 번의 클릭만으로 앱을 설치할 수 있습니다.
{% endhint %}
