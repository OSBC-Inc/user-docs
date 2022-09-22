# IDE 플러그인으로 스캔

## 매니페스트 파일

Snyk CLI는 오픈 소스 종속성을 위해 다양한 프로그래밍 언어와 패키지 관리자를 지원합니다. 지원되는 매니페스트 파일의 전체 목록은 [Open source language and package manager support](../../../../products/snyk-open-source/language-and-package-manager-support/)을 참조하세요.

{% hint style="info" %}
CLI는 기본적으로 지원되는 첫 번째 매니페스트 파일을 검색합니다. 즉, 프로젝트에 매니페스트 파일이 여러 개 있는 경우 `--file` 옵션을 사용하여 검사할 매니페스트 파일의 이름을 제공해야 합니다.
{% endhint %}

Snyk CLI에는 여러 명령이 있지만 검사를 위해 `--json` 옵션과 함께 `test` 명령을 사용하여 출력을 기계가 읽을 수 있는 형식으로 변환하여 구문 분석할 수 있습니다: `snyk test --file=<manifest 파일> --json`

`test` 명령은 종속성이 이미 설치되어 있고(즉, `mvn install` 또는 `npm install`이 실행된 후 스캔) 관련되는 경우 패키지 잠금 파일이 존재할 것으로 예상합니다. 종속성이 설치되기 전에 스캔을 실행하려고 하면 다음과 같은 오류가 표시될 것으로 예상할 수 있습니다:

```
~/git/goof $ snyk test
Missing node_modules folder: we can't test without dependencies.
Please run 'npm install' first.
```

성공적인 실행의 경우 다음과 유사한 긴 JSON 파일이 표시됩니다. 반환되는 데이터를 이해하려면 [데이터 매핑](data-mapping.md) 페이지를 참조하세요.

```javascript
{
  "vulnerabilities": [
    {
      "CVSSv3": "CVSS:3.0/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H",
      "alternativeIds": [],
      "creationTime": "2019-10-22T12:22:54.665794Z",
      "credit": [
        "Roman Burunkov"
      ],
      "cvssScore": 9.8,
      "disclosureTime": "2019-10-18T11:17:09Z",
      "exploit": "Not Defined",
      "fixedIn": [
        "1.1.6-alpha.6"
      ],
      "functions": [],
      "functions_new": [],
      "id": "SNYK-JS-EXPRESSFILEUPLOAD-473997",
      "identifiers": {
        "CVE": [],
        "CWE": [
          "CWE-79"
        ],
        "NSP": [
          1216
        ]
      },
      "language": "js",
      "modificationTime": "2019-11-20T09:48:38.528931Z",
      "moduleName": "express-fileupload",
      "packageManager": "npm",
      "packageName": "express-fileupload",
      "patches": [],
      "publicationTime": "2019-10-22T15:08:40Z",
      "references": [
        {
          "title": "GitHub PR",
          "url": "https://github.com/richardgirges/express-fileupload/pull/171"
        }
      ],
```

{% hint style="info" %}
모든 유료 Snyk 고객은 플랜에 라이선스 스캔 기능이 포함되어 있습니다. `snyk test` 명령은 테스트 결과에 취약점과 오픈 소스 라이선스 위반을 모두 반환합니다. 라이센스 위반을 구별하려면 레코드 필드 내에서 `"type": "license"`를 찾으십시오.
{% endhint %}

## 스캔을 다시 실행해야 하는 경우

사용자에게 최신 스캔 결과를 제공하고 있는지 확인하려면 다음 중 하나가 발생할 때마다 snyk 스캔을 다시 실행해야 합니다.

* 매니페스트 파일이 편집되었습니다.
* 마지막 스캔 이후 하루가 지났습니다. 이는 Snyk CLI를 구동하는 취약점 데이터베이스가 매니페스트 파일을 편집하지 않은 경우에도 사용자가 볼 수 있는 새로운 취약성을 지속적으로 수집하기 때문에 필요합니다.
* semvers에는 유연성이 있고 재설치는 매니페스트 파일 변경 없이 이전에 설치된 것과 다른 종속성 버전을 가져올 수 있으므로 사용자가 종속성을 명시적으로 다시 설치(예: `mvn install` 호출)할 때마다.
