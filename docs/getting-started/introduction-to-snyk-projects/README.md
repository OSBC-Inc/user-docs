# Snyk 프로젝트 소개

프로젝트는 Snyk이 스캔하는 항목을 정의합니다.

프로젝트에는 다음 요소가 포함됩니다.

* Snyk 외부에서 스캔 가능한 항목입니다.
* 해당 스캔을 실행하는방법을 정의하는 구성입니다.

프로젝트는 Snyk 대시보드의 **Projects** 메뉴에서 확인할 수 있습니다.

![](../../.gitbook/assets/code1.png)

## Target

Kubernetes 클러스터 또는 Github 저장소와 같이 스캔할 항목의 주소(Snyk 외부). 하나의 Target은 많은 프로젝트와 관련될 수 있습니다. Target의 구조는 Origin에 따라 다릅니다.

## Origin

LCI, API 또는 Kubernetes와 같은 프로젝트 에코 시스템.

## Targetfile

Github 리포지토리의 pom 파일과 같이 대성에서 스캔할 특정 항목입니다.

[Snyk Code](../../products/snyk-code/) 스캔은 Targetfile을 사용하지 않습니다.

## Type

SAST (Static Application Security Testing) 또는 Snyk Open Source를 사용하는 Maven 프로젝트에 대해 이 프로젝트에 사용할 스캔 방법, 스캔을 위한 구성의 일부분입니다.
