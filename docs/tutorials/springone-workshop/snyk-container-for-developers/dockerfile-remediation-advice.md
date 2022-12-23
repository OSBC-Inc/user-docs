# Dockerfile 수정 조언

## 이미지에 Dockerfile 수정 조언 추가

Snyk은 개발자가 개발 과정에서 보안 결정을 잘 내릴 수 있도록 수정 조언을 제공할 수 있습니다. Snyk은 Snyk CLI 또는 Snyk UI에서 이 작업을 수행할 수 있습니다. 샘플 애플리케이션 **goof**에서 이 정보를 표시하도록 Snyk UI를 구성할 것입니다.

시작하려면 프로젝트 페이지에서 컨테이너 이미지를 선택하십시오.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/container\_image\_snyk\_ui.png)

Snyk UI는 사용자에게 수정 조언을 제공할 수 있으며 컨테이너 이미지를 구성하기 위한 링크를 제공합니다. 보라색 상자 또는 오른쪽 상단 모서리에서 설정 영역 링크를 선택하여 Dockerfile로 컨테이너 이미지를 구성합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/screen-shot-2020-08-21-at-4.38.33-pm.png)

컨테이너 이미지의 source control 저장소를 사용하여 Dockerfile의 위치를 구성합니다.

{% hint style="info" %}
Snyk UI에서 Dockerfile 수정 기능을 사용하려면 Snyk UI에서 source control 저장소를 구성해야 합니다. 자세한 내용은 [GitHub 통합](../../../features/integrations/git-repository-scm-integrations/github-integration.md)을 참조하십시오.
{% endhint %}

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/screen-shot-2020-04-18-at-1.52.23-pm.png)

source control 저장소 선택하기

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/screen-shot-2020-04-18-at-1.53.02-pm.png)

저장소에서 Dockerfile의 위치를 선택합니다. 이 파일은 일반적으로 루트 레벨에 저장되며 Dockerfile이라고 합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/screen-shot-2020-04-18-at-1.53.16-pm.png)

Snyk UI에 컨테이너 이미지를 테스트하고 있는 것을 보여줍니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/screen-shot-2020-04-18-at-2.16.19-pm.png)

테스트가 완료되면 Snyk UI에 컨테이너 이미지에 대해 구성된 Dockerfile이 표시됩니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/container\_image\_goof\_dockerfile\_set.png)

Snyk UI는 컨테이너 이미지에 대한 수정 조언을 표시합니다. Snyk UI는 base image, 취약점 수 및 취약점의 심각도를 표시합니다. 또한 개발자가 base image에 대해 더 나은 선택을 할 수 있도록 minor, major 및 alternative 조언을 제공합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/image\_redmiation\_advice\_spc.png)
