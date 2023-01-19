# Module 1

## Visual Studio Code용 Red Hat 종속성 분석 확장

확장 프로그램을 [설치](https://marketplace.visualstudio.com/items?itemName=redhat.fabric8-analytics\&ssr=false#overview)한 후 VSCode 내에서 매니페스트 파일(pom.xml / package.json / requirements.txt)을 열거나 편집하면 Snyk로 애플리케이션을 스캔하여 종속성의 보안 취약성을 식별합니다. **VSCode File 탐색기** 또는 **VSCode File 편집기**에서 매니페스트 파일(pom.xml/package.json / requirements.txt)을 마우스 오른쪽 버튼으로 클릭하여 애플리케이션에 대한 **Dependency Analytics Report**를 표시할 수도 있습니다.

### 애플리케이션 종속성에서 취약점 찾기

이제 패키지 버전 위로 마우스를 가져가면 추가 세부 정보를 얻을 수 있습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/crda-01.png)

팝업은 즉각적인 권장 사항과 권장 버전 업그레이드를 수락하기 위한 **Peek Problem** 또는 **Quick Fix** 기능을 제공합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/crda-02.png)

**Peek Problem**를 선택하면 취약성의 심각도와 권장 사항에 대한 요약 보기를 볼 수 있습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/crda-03.png)

**Quick Fix**을 선택하면 권장 버전으로의 전환을 확인하는 두 번째 팝업이 제공됩니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/crda-04.png)

확인되면 버전이 매니페스트 파일에서 권장 버전으로 자동 변경된 것을 확인할 수 있습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/crda-05.png)

### 결과 이해 및 수정 우선 순위 지정

매니페스트 파일을 열면 IDE 내에서 **Dependency Analytics Report**를 볼 수도 있습니다. 이것은 클릭할 수 있는 버튼과 함께 IDE의 오른쪽 하단 모서리에 팝업 창으로 나타납니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/dependency-analytics-03.png)

버튼을 클릭하면 **Security Issues**, **Dependency Details** 및 **라이센스** Issues에 대한 요약 정보가 제공됩니다. 또한 추가 정보를 얻고 조언을 수정하기 위해 Snyk 계정으로 로그인할 수 있는 Snyk 고유의 취약점을 볼 수 있습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/dependency-analytics-02.png)

## SCM (Snyk Source Code Management) Integrations

Snyk는 다양한 [Git 저장소(SCM) Integration](https://support.snyk.io/hc/en-us/sections/360001138098-Git-repository-SCM-integrations)을 지원합니다. 이 예에서는 Snyk의 GitHub 통합에 중점을 둘 것입니다. Snyk의 [GitHub Integration](https://support.snyk.io/hc/en-us/articles/360004032117-GitHub-integration)을 통해 모든 통합 저장소에서 지속적으로 보안 검색을 수행하고 오픈 소스 구성 요소의 취약성을 감지하고 자동화된 수정을 제공할 수 있습니다.

통합이 완료되면 다음과 같은 기능을 사용할 수 있습니다:

### **1.** 프로젝트 수준 보안 보고서

Snyk will produce advanced security reports, allowing you to explore the vulnerabilities found in your repositories and fix them right away by opening a fix pull request directly to your repository, with the required upgrades or patches.

### **2.** 프로젝트 모니터링 및 Automatic Fix Pull Request

Snyk은 매일 또는 매주 프로젝트를 자주 스캔합니다. 새로운 취약점이 발견되면 이메일과 저장소에 대한 수정 사항이 포함된 Automatic Fix Pull Request를 열어 알려줍니다. **Open a fix PR**을 수동으로 하는 기능도 있습니다. 이 예에서는 **Priority score**에 주의를 환기시키고자 합니다. Snyk는 문제의 우선 순위를 가능한 한 빠르고 쉽게 지정할 수 있도록 [priority score](https://support.snyk.io/hc/en-us/articles/360009884837)를 제공하므로 최소한의 노력으로 가장 큰 영향을 미칠 수 있습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-rh-vuln-01.png)

**Open a fix PR**을 하기로 결정하면 Snyk는 프로젝트에서 식별된 취약성에 대한 적절한 수정 사항을 계산하고 PR을 생성합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-rh-pr-01.gif)

{% hint style="warning" %}
PR 생성 프로세스는 1\~2분 정도 소요될 수 있습니다.
{% endhint %}

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-rh-pr-02.gif)

완료되면 Pull Request을 검토하고 **approve**/**merge**할 수 있는 GitHub 저장소로 리디렉션됩니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-rh-pr-03.png)
