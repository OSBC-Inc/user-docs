# 테스트 실행

Snyk을 사용하여 여러 방법으로 코드를 테스트할 수 있습니다.

* 수동으로 [Snyk CLI](running-tests.md#cli), [Snyk app](running-tests.md#snyk), [Snyk API](running-tests.md#api)를 사용합니다.
* Snyk은 반복적으로 저장소가 변경될 때 [테스트를 자동으로 실행](running-tests.md#undefined-1)할 수 있습니다.

{% hint style="info" %}
귀하의 계정에서 테스트가 제한될 수 있습니다. [What counts as a test?](https://support.snyk.io/hc/en-us/articles/360000925418-What-counts-as-a-test-)를 참조하십시오.
{% endhint %}

## 수동으로 테스트 실행

### CLI로 테스트 실행

\*\*\*\*[**CLI**](broken-reference)를 사용하면 다음 명령을 사용할 수 있습니다.

* **snyk test**로 오픈소스 코드를 스캔 합니다.
* **snyk container test**로 컨테이너 이미지를 스캔합니다.
* **snyk iac test**로 IaC(Infrastructure as Code)파일을 스캔 합니다.

자세한 내용은 [Snyk CLI 시작하기](broken-reference)를 참조하십시오.

### Snyk 앱으로 테스트 실행

새 프로젝트를 추가하거나 Retest now 버튼을 클릭하면 테스트가 실행됩니다.

자세한 내용은 [Snyk 시작하기](broken-reference)를 참조하십시오.

### API로 테스트 실행

테스트는 [**https://snyk.io/api/v1/test**](https://snyk.io/api/v1/test) \*\*\*\* endpoint를 호출할 때 진행합니다.

자세한 내용은 [API 문서](https://github.com/snyk/user-docs/tree/54e0dec0fe0e081d49f34119a9018499ad5c9e96/introducing-snyk/snyks-core-concepts/running-tests/README.md)를 참조하십시오.

## 자동으로 테스트 실행

Snyk은 반복되는 테스트와 함께 자동 스캔 기능을 제공하여 새로운 취약점을 자동으로 포착할 수 있도록 합니다. 프로젝트를 가져온 후 Snyk은 주기적으로 테스트를 진행하여 소스 코드가 새로 공개된 취약점의 영향을 받는지 확인합니다.

{% hint style="info" %}
테스트 빈도는 기본적으로 매일 진행하는 것으로 설정됩니다. 변경하려면 **Usage** 페이지([Usage page details](../../features/user-and-group-management/managing-settings/usage-page-details.md) 참조) 또는 project **Settings** 페이지([프로젝트 설정 보기](../../getting-started/introduction-to-snyk-projects/view-project-settings.md) 참조)로 이동하십시오.
{% endhint %}

### Snyk monitor

CLI 명령어 `snyk monitor`를 사용하여 Snyk 웹 사이트에서 새로운 취약점에 대해 지속적으로 모니터링할 프로젝트의 스냅샷을 생성합니다.

자세한 내용은 [Monitor your projects at regular intervals](broken-reference)를 참조하십시오.

### PR/MR 자동 테스트

기본적으로 Snyk은 모니터링되는 저장소에 생성된 모든 PR을 스캔하여 단일 보안 검사와 단일 라이선스 검사로 그룹화된 결과와 권장 사항을 제공합니다.

자세한 내용은 [PR에서 Snyk 테스트 활성화](broken-reference)를 참조하십시오.
