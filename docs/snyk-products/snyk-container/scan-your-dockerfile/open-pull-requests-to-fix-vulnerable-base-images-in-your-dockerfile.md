# Dockerfile의 취약한 기본 이미지를 수정하기 위한 PR 열기

Snyk은 Git 저장소를 가져올 때 Dockerfile을 검색하여 취약한 기본 이미지를 탐지하고 자동 PR을 사용하여 수정할 수 있도록 도와줍니다. 이렇게 하면 이미지를 빌드하기 전에 보안 문제를 검사하고 레지스트리 또는 프로덕션에 도달하기 전에 해결할 수 있습니다.

Dockerfile 수정 PR에 지원되는 git 기반 저장소는 다음과 같습니다.

* GitHub
* GitLab
* Bitbucket Server
* Bitbucket Cloud
* GitHub Enterprise Server
* Azure repos

Snyk에서 생성된 Dockerfile 프로젝트의 경우 기본 이미지가 [Official Docker image](https://docs.docker.com/docker-hub/official\_images/)인 경우 결과에는 기존의 더 취약한 이미지 대신 사용할 수 있는 적절한 기본 이미지 목록이 포함됩니다. 자세한 내용은 [기본 이미지 권장 사항](https://docs.snyk.io/snyk-container/getting-around-the-snyk-container-ui/analysis-and-remediation-for-your-images-from-the-snyk-app)에 대한 섹션을 참조하십시오.

그런 다음 Snyk은 자동으로 Dockerfile에 대한 수정 PR을 발행하여 사용 가능한 최신 minor 버전으로 업그레이드합니다.

초기 스캔 후 Dockerfile에 변경 사항이 있거나 더 나은 기본 이미지가 감지될 경우 자동 수정 PR이 생성됩니다.

또는 업그레이드할 버전에 대한 **Open a Fix PR**을 클릭하여 수동으로 생성할 수 있습니다.

![](../../../.gitbook/assets/mceclip0-6-.png)

Git 저장소의 수정 PR을 보고 변경 사항과 변경 사항이 발생한 위치를 확인할 수 있습니다. Dockerfile의 FROM 행이 향상된 버전으로 새롭게 업데이트됩니다.

{% hint style="info" %}
**참고**\
변경 사항을 병합하기 전에 애플리케이션이 제대로 작동하는지 확인하는 것이 좋습니다.
{% endhint %}

PR이 생성되고 확인 후 PR을 안전하게 병합하여 컨테이너 이미지의 취약점 수를 즉시 줄일 수 있습니다.

![mceclip1.png](../../../.gitbook/assets/mceclip1-1-.png)

![](../../../.gitbook/assets/mceclip2.png)

사용 가능 여부

이 기능은 모든 사용자가 사용할 수 있습니다. 모든 무료 사용자에게는 기본적으로 활성화되어 있고 Snyk 고객의 기존 통합에 대해 기본적으로 비활성화되어 있습니다. Integration 또는 Project 설정 섹션에서 설정할 수 있습니다.

![](../../../.gitbook/assets/auto-detect-dockerfiles.png)
