# Snyk Target 및 Projects 소개

## Targets

Target은 통합, CLI, UI 또는 API를 통해 Snyk이 스캔한 외부 리소스를 나타냅니다.

Targetd은 SCM 저장소, Kubernetes 워크로드 또는 Snyk 외부의 기타 스캔 가능한 리소스를 나타낼 수 있습니다. Snyk이 생성하는 모든 [Project](./#projects)는 상위 Target에 연결됩니다. 하나의 Target은 많은 Project와 관련될 수 있습니다. Target의 구조는 [Origin](./#origin)에 따라 다릅니다.

Target은 Snyk 대시보드의 **Projects** 메뉴에 나타납니다.

## Origin

CLI, GitHub 또는 Kubernetes와 같은 ~~_Target ecosystem_~~입니다.

가능한 값은 다음과 같습니다.

* acr
* api
* artifactory-cr
* aws-config
* aws-lamba
* azure-functions
* azure-repos
* bitbucket-cloud
* bitbucket-server
* cli
* cloud-foundry
* digitalocean-cr
* docker-hub
* ecr
* gcr
* github
* github-cr
* github-enterprise
* gitlab
* gitlab-cr
* google-artifact-cr
* harbor-cr
* heroku
* ibm-cloud
* kubernetes
* nexus-cr
* pivotal
* quay-cr
* terraform-cloud

Origin은 [Target](./#targets)의 속성이며 Projects 메뉴에 Target 이름 옆의 아이콘으로 표시됩니다.

## Projects

Project는 Snyk이 주어진 Target에서 스캔하는 항목입니다. Project에는 다음 요소가 포함됩니다.

* Snyk 외부에서 스캔 가능한 항목입니다.
* 해당 스캔을 실행하는 방법을 정의하는 구성입니다.

Project는 Snyk 대시보드의 **Projects** 메뉴에서 확인할 수 있습니다.

![](../../.gitbook/assets/code1.png)

## Targetfile

Github 저장소의 pom 파일과 같이 Target에서 스캔할 특정 항목입니다.

[Snyk Code](../../snyk-products/snyk-code/) 스캔은 Targetfile을 사용하지 않습니다.

## Type

SAST(Static Application Security Testing) 또는 Snyk Open Source를 사용하는 Maven 프로젝트에 대해 이 프로젝트에 사용할 스캔 방법, 스캔을 위한 구성의 일부분입니다.
