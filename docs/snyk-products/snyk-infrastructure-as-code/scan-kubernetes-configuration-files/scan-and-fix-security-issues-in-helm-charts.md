# Helm Charts의 보안 문제 스캔 및 수정

잘못된 구성과 보안 문제가 있는지 Kubernetes 구성 파일을 검색하는 것 외에도, Snyk은 Helm Charts를 템플릿하고 결과 매니페스트를 스캔할 수 있습니다. 이 템플릿 기능은 Snyk UI를 통해 저장소를 가져올 때만 사용할 수 있습니다. Snyk CLI를 사용하여 템플릿 Helm Charts를 검색하는 방법은 아래 섹션을 참조하세요. Helm Charts를 스캔하면 Snyk은 각 템플릿 및 종속 템플릿에 대한 프로젝트를 만들고 잘못된 구성에 대한 보고서를 생성하고 수정 권장 사항을 제공합니다.

## 전제 조건

* 관리자는 조직을 선호하는 Git 저장소와 통합하고 [문서](../scan-cloudformation-files/configure-your-integration-to-find-security-issues-in-your-cloudformation-files.md)에 설명한 대로 구성 파일 감지를 활성화해야 합니다.
* 저장소는 [standard Chart directory structure](https://helm.sh/docs/topics/charts/#the-chart-file-structure)에 맞추어 진행합니다.
* 현재 우리는 기본값 파일인 values.yaml을 사용한 Helm Charts 템플릿만 지원합니다. Helm 값의 특정 구성을 검색하려는 경우 지원되는 워크플로는 Snyk 외부의 차트를 템플릿으로 만들고 매니페스트를 일반 Kubernetes 파일로 스캔합니다.
  * 기본값 파일에서 템플릿할 수 없는 Helm Charts는 현재 지원하지 않습니다.
* 모든 차트 디펜던시는 구성된 Helm 저장소에서 공개적으로 다운로드할 수 있거나 테스트 대상 차트와 동일한 git 저장소에서 찾을 수 있어야 합니다.

## 차트 스캔 및 수정

1. 계정에 로그인하고 관리하려는 관련 그룹 및 조직으로 이동합니다.
2. 관리자가 클라우드 구성 파일 감지를 활성화하기 전에 테스트를 위해 이미 저장소를 가져온 경우 Helm Charts를 가져오려면 해당 저장소를 다시 가져와야 합니다.
3. 저장소를 스캔할 때마다 다음과 같이 진행합니다.
   1. Helm Charts의 각 템플릿은 저장소별로 그룹화된 Snyk 프로젝트를 만듭니다.
   2. 클라우드 구성 파일을 가져오기 위해 저장소를 다시 가져온 경우 Snyk은 구성 파일을 가져오고 테스트하며 이미 가져온 애플리케이션 매니페스트 파일도 다시 테스트합니다. 테스트 시간은 "now"로 표시됩니다.
4. 관심 있는 프로젝트 링크를 클릭하여 검색 결과를 보고 그에 따라 구성 파일을 수정합니다.
   1. 외부 디펜던시에서 생성된 프로젝트도 검사하고 문제가 표시됩니다.

![](../../../.gitbook/assets/screenshot\_2020-04-24\_at\_08.51.18.png)

## 사용자 정의 Helm 값 구성 테스트

기본값만 사용하여 차트를 테스트하는 것만으로는 충분하지 않을 때가 있습니다. Snyk은 현재 사용자 지정 값을 가져오기에 전달하는 기능을 지원하지 않습니다. 이 섹션은 Snyk 이외의 사용자 지정 구성을 템플릿으로 지정하고 결과 Kubernetes 매니페스트를 검색하는 방법에 대한 지침을 제공합니다.

Snyk CLI와 Helm을 함께 사용할 수 있습니다.

```bash
cd /path/to/helm/chart
helm dependency update
helm template . --output-dir out
snyk iac test out/
```

기본이 아닌 구성을 테스트하기 위해 표준 Helm 값 플래그(예: --set 또는 --values)를 Helm 템플릿에 전달할 수 있습니다.

이 프로세스를 스크립팅하여 CLI 파이프라인에서 실행하거나, 또는 Helm 템플릿 파일을 저장소로 실행하여 Snyk에 프로젝트로 가져올 수 있습니다.
