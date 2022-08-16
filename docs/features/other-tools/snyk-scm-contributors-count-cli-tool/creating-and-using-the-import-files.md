---
description: "\bImport file을 생성하고 snyk-api-import 도구와 함께 사용하는 방법"
---

# Import file 생성 및 사용

## Import file 작동 방식

이 기능은 Bitbucket 및 Azure에서만 작동합니다.

`snyk-scm-contributors-count` 도구가 Snyk 계정과 SCM 계정에 모두 연결되면 도구는 Snyk에서 모니터링하는 저장소/프로젝트를 찾아냅니다.

`importConfDir` 와 `importFileRepoType` flags를 명령에 적용하면 도구가 [snyk-api-import ](creating-and-using-the-import-files.md#using-the-snyk-api-import-tool)도구와 함께 사용하여 누락된 리포지토리를 Snyk 계정으로 가져오는 데 사용할 모니터링되지 않는 리포지토리 데이터로 채워진 import file을 생성합니다.

* Snyk token을 내보냈고 관련 Snyk 계정에 도구가 스캔하는 특정 SCM에 대한 통합 세트가 있는 경우 도구는 `snyk-api-import` 도구 에서 필요에 따라 Snyk에서 OrgID 및 IntegrationID를 찾아 일치시키고 도구를 가져와 자동으로 import file에 추가합니다.
* Snyk token을 내보내지 않았거나 사용자에게 아직 Snyk 계정이 없는 경우 이 기능을 사용하여 SCM의 모든 저장소를 매핑하고 나중에 `snyk-api-import` 도구에서 사용할 import file을 생성할 수 있습니다. 이 경우 또는 도구가 OrgID 또는 IntegrationID를 찾을 수 없는 경우 도구는 사용자에게 이러한 ID를 제공하라는 메시지를 표시하고(한 번) 자동으로 import file에 추가합니다.

## The import flags

`importConfDir` - 이 flag는 모니터링되지 않는 저장소에 대한 쿼리가 작성되어야 하고 json import file을 생성할 폴더(쓰기 권한이 있는) 경로가 필요합니다. 예를 들면 다음과 같습니다 :

```
snyk-scm-contributors-count <command> --token TOKEN -- importConfDir /snyk/import/
```

기본적으로 이 명령은 SCM을 스캔할 때 발견된 모든 유형의 모니터링되지 않는 저장소로 json import file을 채웁니다.

`importFileRepoType` - 이 flag는 `all,` `private`, or `public`(대소문자 구분하지 않음) 값으로 설정하여 지정된 repo 유형의 데이터만 import file을 채울 수 있습니다. 예를 들면 다음과 같습니다 :

```
snyk-scm-contributors-count <command> --token TOKEN -- importConfDir /snyk/import/ --importFileRepoType 'private'
```

{% hint style="info" %}
Import file은 Snyk에서 올바른 조직 및 통합으로 가져오기 위해 사용자의 OrgID 및 IntegrationID가 필요합니다.&#x20;

도구는 Snyk에서 이 두 값을 찾으려고 시도합니다(SNYK\_TOKEN이 내보내지고 Snyk의 조직 매핑이 SCM의 매핑으로 미러링된 경우) 도구가 해당 값을 찾을 수 없는 경우 사용자에게 제공하라는 메시지가 명령줄에서 표시됩니다.

사용자가 OrgID 및 IntegrationID에 대한 값을 한 번 지정하면 이러한 값이 import file의 모든 항목에 대해 설정됩니다(즉, 가져온 모든 저장소가 Snyk의 동일한 조직 아래에 있음을 의미함).
{% endhint %}

## snyk-api-import 도구 사

snyk-api-import 도구는 사용자가 안전하고 강력한 방식으로 Snyk 계정의 새 저장소를 가져올 수 있도록 도와줍니다.

이 도구를 사용하려면 가져올 repos 데이터가 있는 json 파일이 필요합니다. 이 파일은 이전 섹션에서 설명한 대로 **snyk-contributors-count** 도구에 의해 자동 생성될 수 있습니다.

## 추가 정

**snyk-api-import** 도구에 대한 자세한 내용은 다음을 참조하십시오 :

* [https://github.com/snyk-tech-services/snyk-api-import](https://github.com/snyk-tech-services/snyk-api-import)
* [https://github.com/snyk-tech-services/snyk-api-import/blob/master/docs/import.md](https://github.com/snyk-tech-services/snyk-api-import/blob/master/docs/import.md)
