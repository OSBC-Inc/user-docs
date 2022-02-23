# labels를 사용하여 Dockerfile과 이미지를 자동으로 연결

Snyk을 사용하면 Dockerfile에서 빌드된 모든 컨테이너 이미지로 수동 또는 자동으로 연결할 수 있습니다. 이를 사용하여 실행 중인 애플리케이션에 대한 보안 영향을 이해하고, 작업을 수행하고 Dockerfile 기본 이미지를 업데이트할 때 더 안전하게 보호할 수 있거나 다시 빌드해야 하는 이미지를 파악할 수 있습니다.

## 연결된 이미지 보기

이 정보는 프로젝트 세부 정보의 **LINKED IMAGES** 섹션에 표시됩니다.

![](../../../.gitbook/assets/mceclip3.png)

컨테이너 레지스트리 통합을 통해 가져온 이미지를 기존 Dockerfile 프로젝트에 자동으로 연결할 수 있습니다. 이 작업은 이미지의 OCI label이 있는 Snyk의 조직에 존재하는 Dockerfile의 경로와 일치하는지 확인하여 수행됩니다.

## 작동 방식

프로젝트 가져오기(또는 재테스트) 시 이미지가 분석되고 취약점이 스캔되며 이미지 label도 이미지 매니페스트에서 검색됩니다. 그런 다음 Snyk은 다음을 확인합니다.

* dockerfile 위치를 정의하는 이미지 label이 있습니다.
  * `org.opencontainers.image.source` - 프로젝트 저장소에 대한 URL(필수)
  * `io.snyk.containers.image.dockerfile` - Dockerfile 경로, 예: "/Dockerfile-prod" (선택 사항)
* Dockerfile 프로젝트는 이미지 label에서 일치하는 저장소(및 경로 또는 /Dockerfile)가 있는 동일한 조직에 존재합니다.

위의 사항이 적용되면 Snyk은 이미지와 dockerfile 프로젝트 사이에 링크를 자동으로 생성합니다.

## 연결 자동 업데이트/제거

dockerfile label이 업데이트되고 새 위치를 대상으로 지정하는 경우 링크가 자동으로 업데이트됩니다. 이는 재테스트 시 또는 반복 테스트가 실행될 때 발생할 수 있습니다.

이미지 프로젝트 또는 Dockerfile 프로젝트가 삭제되거나, Snyk의 기존 프로젝트 없이 Dockerfile 위치를 대상으로 하도록 Dockerfile label이 업데이트된 경우 또는 Dockerfile label이 제거된 경우 링크가 제거됩니다.

## brokered SCM integrations로 연결

링크를 생성하려면 Snyk이 Dockerfile 저장소 URL을 올바른 SCM 조직 소스에 매핑할 수 있어야 합니다. brokered integrations의 경우 이 URL을 기본적으로 사용할 수 없기 때문에 이 방법이 조금 더 복잡합니다.

![](../../../.gitbook/assets/mceclip0-4-.png)

사용 가능하게 되면 Snyk은 이를 링크 생성에 사용할 수 있습니다.
