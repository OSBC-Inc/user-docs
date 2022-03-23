# Dockerfile에서 취약한 기본 이미지 감지

Snyk은 Git 저장소를 가져올 때 Dockerfile을 스캔하여 취약한 기본 이미지를 탐지합니다. 이렇게 하면 이미지를 빌드하기 전에 보안 문제를 검사할 수 있으므로 잠재적인 문제가 레지스트리나 운영 환경에 도달하기 전에 해결하는 데 도움이 됩니다.

[Git 저장소를 Snyk에 통합](../../../features/integrations/git-repository-scm-integrations/)하면 해당 저장소에 있는 모든 Dockerfile이 자동으로 선택되어 웹 UI에 ‘projects’로 표시됩니다.

![](../../../.gitbook/assets/mceclip0-5-.png)

## Dockerfile에서 컨테이너 이미지로 연결

Dockerfile에서 작성된 모든 컨테이너 이미지로 연결할 수도 있습니다. 이 정보를 사용하여 실행 중인 애플리케이션에 대한 보안 영향을 파악하고, 조치를 취할 수 있습니다. 또한 Dockerfile 기본 이미지를 업데이트할 때 보안이 강화되거나 다시 빌드해야 하는 이미지를 파악할 수 있습니다.

![](../../../.gitbook/assets/mceclip3.png)

취약한 기본 이미지 탐지 및 수정 권장 사항에 대한 자세한 내용은 [기본 이미지 감지](../getting-around-the-snyk-container-ui/base-image-detection.md)를 참조하십시오.
