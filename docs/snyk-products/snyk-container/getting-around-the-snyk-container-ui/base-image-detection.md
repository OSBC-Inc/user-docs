# 기본 이미지 감지

취약한 기본 이미지를 탐지하면 취약점의 원인을 식별하고 권장 사항에 따라 기본 이미지를 업데이트하여 수정할 수 있습니다.

[컨테이너 통합](../)(예: CLI 또는 컨테이너 레지스트리 통합)을 구성한 후에는 기본 이미지를 탐지할 수 있습니다.

{% hint style="info" %}
지원되는 이미지 목록은 [image scanning library](../image-scanning-library/)를 참조하십시오.
{% endhint %}

## 식별 방법

취약한 기본 이미지를 식별하려면 다음 방법 중 하나를 사용할 수 있습니다.

* **Auto-detection**: Snyk이 컨테이너 이미지를 분석하면 이미지 매니페스트에서 관련 메타데이터가 추출되고 기본 이미지가 자동으로 감지됩니다. 이 방법은 이미지 매니페스트에서 **rootfs** 레이어를 분석하며, 이는 DockerHub에서 하나 이상의 이미지/이미지 태그와 동일할 수 있습니다.
* **Dockerfile**: Snyk은 Dockerfile을 사용하여 취약한 기본 이미지를 탐지할 수도 있습니다. **--file** 옵션을 사용하여 CLI **snyk container** scan에 첨부하거나 프로젝트 설정을 통해 SCM에서 연결하거나 Git 저장소를 가져올 때 Dockerfile을 감지하고 스캔할 수도 있습니다. 이 방법은 더 정확할 수 있지만 자동 탐지에 비해 추가 단계가 필요합니다.

두 방법 모두 Snyk UI에 “project”가 생성됩니다.

## 기본 이미지 권장 사항

기본 이미지가 [공식 Docker 이미지](https://docs.docker.com/docker-hub/official\_images/)인 경우, 스캔된 취약점 중 일부를 해결하기 위한 업그레이드 권장 사항이 결과에 포함됩니다.

이를 통해 minor 및 major 업그레이드뿐만 아니라 취약점이 더 적을 수 있는 대체 기본 이미지의 취약점 수를 확인할 수 있습니다. 이를 통해 기본 이미지를 업그레이드할지, 어떤 이미지가 가장 적합한지 결정할 수 있습니다.

![](../../../.gitbook/assets/base-image2.png)

자세한 내용은 [Snyk 앱에서 이미지 분석 및 수정](analysis-and-remediation-for-your-images-from-the-snyk-app.md)을 참조하십시오.

프로젝트 지침에 의해 추가된 취약점 중 우선순위 점수에 따라 정렬된 기본 이미지 취약점을 찾을 수 있습니다. 또한 **Image Layer** 필터 아래의 **Base image** 옵션을 사용하여 기본 이미지 취약점만 필터링할 수 있습니다. 자세한 내용은 [이미지 레이어 정보](image-layer-information.md)를 참조하십시오.
