# C / C++용 Snyk

{% hint style="info" %}
이 기능은 현재 베타 버전입니다.

[Snyk Preview](broken-reference)를 활성화하려면 다음과 같이 진행합니다.

1. Snyk에 로그인합니다.
2. 설정 아이콘을 클릭하여 **Settings**로 이동합니다 .
3. **Snyk Preview**를 클릭합니다.
4. 기능을 활성화한 다음 **Save changes**를 클릭합니다.
{% endhint %}

Snyk을 사용하여 C/C++ 프로젝트를 스캔할 수 있습니다.

### 특징

{% hint style="info" %}
**NOTE**\
요금제에 따라 일부 기능을 사용하지 못할 수 있습니다.
{% endhint %}

| Package managers / Features | CLI support | Git support | License scanning | Fixing | Runtime monitoring |
| --------------------------- | ----------- | ----------- | ---------------- | ------ | ------------------ |
| C/C++                       | ✔︎          |             |                  |        |                    |

### 작동 방식

스캔은 다양한 온라인 소스의 최신 소스코드가 주기적으로 업데이트되는 오픈소스 데이터베이스에 의해 구동됩니다.

{% hint style="info" %}
C/C++의 취약점을 탐색하려면 [Snyk Vuln DB](https://security.snyk.io)를 사용하십시오 .
{% endhint %}

`snyk unmanaged test` 명령어를 실행하면 다음과 같이 진행합니다.

1. 현재 폴더의 모든 파일을 Hash 리스트로 변환합니다.
2. Hash를 Snyk 스캔 서버로 전송합니다.
3. 잠재적으로 일치하는 디펜던시 목록을 찾기 위해 데이터베이스를 쿼리합니다.
4. 디펜던시를 알려진 취약점에 연결합니다.
5. 결과를 표시합니다.

{% hint style="info" %}
프로젝트를 스캔하려면 스캔한 디렉토리에서 디펜던시를 소스코드로 사용할 수 있어야 합니다. 디펜던시가 다른 위치에 있는 경우 해당 위치를 스캔해야 합니다.
{% endhint %}

### 제약 및 제한 사항

{% hint style="info" %}
다음과 같은 제약 및 제한 사항은 의도된 것입니다. 우리가 앞으로 개선을 할 수는 있지만, 문제로 간주되지는 않습니다. 해결될 예정인 문제는 [Known Issues ](snyk-for-c-c++.md#known-issues)섹션에 있습니다.
{% endhint %}

**디펜던시 소스코드를 사용할 수 있어야 합니다.**

Snyk CLI가 소스코드에서 디펜던시를 찾을 수 있으려면 디펜던시의 전체 소스코드가 스캔한 폴더에 있어야 합니다. 다음은 Snyk이 스캔할 수 있는 일반적인 디렉토리 구조입니다.

```
c-example
├── deps
│   ├── curl-7.58.0
│   │   ├── include
│   │   │   ├── Makefile.am
│   │   │   ├── Makefile.in
│   │   │   ├── README
│   │   │   └── curl
│   │   ├── install-sh
│   │   ├── lib
│   │   │   ├── asyn.h
│   │   │   ├── base64.c
│   │   │   ├── checksrc.pl
│   │   │   ├── config-amigaos.h
│   │   │   ├── conncache.c
│   │   │   ├── conncache.h
│   │   ├── src
│   │   │   ├── tool_binmode.c
│   │   │   ├── tool_binmode.h
│   │   │   ├── tool_bname.c
│   │   │   ├── tool_xattr.c
...
```

디펜던시를 정확하게 식별하여 정확한 취약점 집합을 파악하기 위해서는 대부분의 파일을 변경되지 않은 원본 형식으로 유지하는 것이 중요합니다. 많은 파일을 수정할 경우(예: 헤더 파일만 포함) 스캔 엔진의 신뢰도가 낮아져 디펜던시가 식별되지 않거나 잘못 식별됩니다. (다른 버전 또는 다른 패키지로 식별됨)

#### 데이터 수집 참고 사항

C++ 프로젝트를 스캔할 때 다음 데이터가 수집되고 문제 해결을 위해 저장될 수 있습니다.

| Category       | Description                                                                                          |
| -------------- | ---------------------------------------------------------------------------------------------------- |
| 스캔한 파일의 Hash 값 | 모든 파일은 되돌릴 수 없는 Hash 리스트로 변환 됩니다.                                                                    |
| 스캔한 파일의 상대 경로  | 더 나은 식별 및 오픈소스 일치를 위해 스캔 중인 디렉토리와 관련된 파일 경로가 포함됩니다.예:`./project-name/vendor/bzip2-1.0.6/blocksort.c` |

### C/C++ 프로젝트용 Snyk CLI

#### Snyk CLI 설치

C/C++ 스캐닝은 [Snyk CLI](broken-reference)에서 사용할 수 있습니다. 자세한 내용은 [Install the CLI](broken-reference)를 참조하십시오.

{% hint style="info" %}
C/C++ 스캐닝이 포함된 Snyk CLI의 최소 버전은 1.857.0입니다.
{% endhint %}

#### 테스트 실행

프로젝트의 취약점을 테스트하려면 다음과 같이 진행하십시오.

```
$ snyk test --unmanaged
```

{% hint style="warning" %}
Windows에서 Linux 프로젝트를 스캔하는 경우 저장소가 \~\~_Linux line endings_\~\~로 되어있는지 확인하십시오. 자세한 내용은 [Known Issues](snyk-for-c-c++.md#known-issues)를 참조하십시오.
{% endhint %}

#### 디펜던시 표시

디펜던시를 표시하려면 `--print-deps` 옵션을 사용하십시오.

```bash
$ snyk test --unmanaged --print-deps

Dependencies:

  cpython|https://github.com/python/cpython/archive/v3.7.2.zip@3.7.2
  confidence: 1.000
  
  zip|http://ftp.debian.org/debian/pool/main/z/zip/zip_3.0.orig.tar.gz@3.0
  confidence: 0.993
```

식별하는 각 디펜던시에 기여한 파일을 확인하려면 `--print-dep-paths` 파라미터를 사용하십시오.

```bash
$ snyk unmanaged test --print-dep-paths

Dependencies:

  curl|https://github.com/curl/curl/releases/download/curl-7_58_0/curl-7.58.0.tar.xz@7.58.0
  confidence: 1.000
  matching files:
    - c-example/deps/curl-7.58.0/CHANGES
    - c-example/deps/curl-7.58.0/CMake/CMakeConfigurableFile.in
    - c-example/deps/curl-7.58.0/CMake/CurlSymbolHiding.cmake
    ... and 2857 more files
```

#### 신뢰 수준 이해

소프트웨어에서 사용하는 디펜던시의 소스코드를 변경해야 할 수도 있습니다. Snyk은 파일 시그니처를 사용하여 오픈소스 라이브러리에 가장 일치하는 항목을 찾기 때문에 변경 사항이 실제 라이브러리 식별의 정확성을 감소시킬 수 있습니다.

Snyk이 식별된 디펜던시와 해당 버전에 대해 얼마나 확신하는지 확인하려면 `--print-deps` 또는 `--print-dep-paths` 파라미터를 사용하십시오.

```
curl|https://github.com/curl/curl/releases/download/curl-7_58_0/curl-7.58.0.tar.xz@7.58.0
confidence: 0.993
```

이 신뢰 단계는 Snyk이 디펜던시의 실제 식별에 대해서 얼마나 확신하는지 나타냅니다. 숫자는 0과 1 사이로 표시되며 높을수록 결과가 더 정확합니다. 따라서 신뢰도가 **1**이라는 것은 소스 트리의 모든 파일이 데이터베이스의 모든 예상 파일과 완전히 일치한다는 것을 의미합니다.

#### JSON 출력

결과를 JSON 형식으로 출력하려면 `--json` 파라미터를 사용하십시오.

```
$ snyk test --unmanaged --json
[
  {
    "issues": [
      {
        "pkgName": "curl|https://github.com/curl/curl/releases/download/curl-7_58_0/curl-7.58.0.tar.xz",
        "pkgVersion": "7.58.0",
        "issueId": "CVE-2019-5481",
        "fixInfo": {
          "isPatchable": false,
          "isPinnable": false
        }
      }
    ],
    "issuesData": {
      "CVE-2019-5481": {
        "severity": "high",
        "CVSSv3": "",
        "originalSeverity": "high",
        "severityWithCritical": "high",
        "type": "vuln",
        "alternativeIds": [
          ""
        ],
        "creationTime": "2019-09-16T19:15:00.000Z",
        "disclosureTime": "2019-09-16T19:15:00.000Z",
        "modificationTime": "2020-10-20T22:15:00.000Z",
        "publicationTime": "2019-09-16T19:15:00.000Z",
        "credit": [
          ""
        ],
        "id": "CVE-2019-5481",
        "packageManager": "cpp",
        "packageName": "curl|https://github.com/curl/curl/releases/download/curl-7_58_0/curl-7.58.0.tar.xz",
        "language": "cpp",
        "fixedIn": [
          ""
        ],
        "patches": [],
        "exploit": "No Data",
        "functions": [
          ""
        ],
        "semver": {
          "vulnerable": [
            "7.58.0"
          ],
          "vulnerableHashes": [
            ""
          ],
          "vulnerableByDistro": {}
        },
        "references": [
          {
            "title": "https://curl.haxx.se/docs/CVE-2019-5481.html",
            "url": "https://curl.haxx.se/docs/CVE-2019-5481.html"
          },
        ],
        "internal": {},
        "identifiers": {
          "CVE": [
            "CVE-2019-5481"
          ],
          "CWE": [],
          "ALTERNATIVE": [
            ""
          ]
        },
        "title": "CVE-2019-5481",
        "description": "",
        "license": "",
        "proprietary": true,
        "nearestFixedInVersion": ""
      }
    },
    "fileSignaturesDetails": {
      "curl|https://github.com/curl/curl/releases/download/curl-7_58_0/curl-7.58.0.tar.xz@7.58.0": {
        "filePaths": [
          "deps/curl-7.58.0/CHANGES",
          "c-example/deps/curl-7.58.0/CMake/CMakeConfigurableFile.in",
          "c-example/deps/curl-7.58.0/CMake/CurlSymbolHiding.cmake"
        ],
        "confidence": 1
      }
    }
  }
]
```

### Command line 옵션

다음 `snyk` command line 옵션은 `snyk test --unmanaged` 및 `snyk monitor --unmanaged` 명령에서 지원됩니다.

#### ORG\_ID

`--org=<ORG_ID>`

특정 조직에 연결된 Snyk 명령을 실행할 `<ORG_ID>`를 지정합니다. `snyk monitor` 명령을 실행한 후 새 프로젝트가 생성되는 위치를 정의합니다. 일부 기능에는 지원 여부 및 private 테스트 제한이 있습니다. 조직이 여러 개인 경우 CLI에서 다음 명령을 사용하여 기본값을 설정할 수 있습니다.

```
snyk config set org=ORG_ID
```

기본값을 설정하면 새로 모니터링되는 모든 프로젝트가 기본 조직 아래에 생성됩니다. 기본값을 덮어쓰려면 `--org=<ORG_ID>`를 사용합니다.

기본값: `<ORG_ID>`, [계정 설정](https://app.snyk.io/account)에서 현재 선호하는 조직입니다.

자세한 내용은 [CLI에서 사용할 조직을 선택하는 방법](https://support.snyk.io/hc/en-us/articles/360000920738-How-to-select-the-organization-to-use-in-the-CLI) 문서를 참조하십시오.

#### json

`--json`

결과를 JSON 형식으로 출력합니다.

#### OUTPUT\_FILE\_PATH

`--json-file-output=OUTPUT_FILE_PATH`

`--json` 옵션 사용 여부에 관계없이 테스트 출력을 지정된 파일에 직접 저장합니다. (test 명령에서만 사용 가능)

이는 stdout을 통해 사람이 읽을 수 있는 테스트 출력을 표시하는 동시에 JSON 형식 출력을 파일에 저장하는 데 유용합니다.

**target-dir**

`--target-dir <directory>`

현재 디렉토리 대신 인수에 지정된 경로를 스캔합니다.

### Snyk App에서 스캔 결과 가져오기

Snyk App에서 테스트 결과(Issues 및 디펜던시)를 가져오려면 `snyk monitor --unmanaged` 명령어를 실행합니다.

```
$ snyk unmanaged monitor
Monitoring /c-example (c-example)...

Explore this snapshot at https://app.snyk.io/org/example-org/project/8ac0e233-d0f9-403e-b422-5970e7a37443/history/5de4616d-3967-485f-bf21-bbbe91068029

Notifications about newly disclosed issues related to these dependencies will be emailed to you.
```

디펜던시 및 취약점의 스냅샷이 생성되고 Snyk App으로 가져와 Issue를 검토하고 보고서에 포함된 것을 볼 수 있습니다.

관리되지 않는 디펜던시가 있는 프로젝트를 가져오면 Snyk App에 새 프로젝트가 생성됩니다.

![관리되지 않는 디펜던시가 있는 프로젝트](../../../.gitbook/assets/kuva.png)

### 알려진 문제

**Windows에서 스캔 시 발생하는 문제**

Git의 많은 오픈 소스 프로젝트들은 Unix 개행문자를 사용합니다. 기본적으로 Windows의 Git은 Unix 개행문자를 Windows 개행문자로 변환하고 실제 커밋에 대해서만 다시 변환합니다. Snyk 데이터베이스에는 원본 줄 끝이 있는 소스 코드 시그니처가 포함되어 있으므로 Windows에서 Windows 개행문자가 있는 파일에 대해 생성된 시그니처가 데이터베이스의 시그니처와 다릅니다. 이 경우 디펜던시가 발견되지 않을 가능성이 매우 높습니다.

Windows에서 Unix 개행문자가 있는 프로젝트를 스캔하려면 Git 개행문자 변환을 비활성화하십시오. 이 설정을 전체적으로 적용하려면 다음 명령어를 실행하십시오.

```shell
git config --global core.autocrlf false
```

### 자주 묻는 질문

#### 내 소스 코드가 Snyk 서버로 전송합니까?

아니요. 파일은 스캔을 위해 전송하기 전에 Hash 리스트로 변환됩니다.

#### Snyk이 디펜던시를 찾지 못한 이유는 무엇입니까?

Snyk은 많은 오픈 소스 구성 요소의 공식 릴리즈를 데이터베이스에 저장하지만 스캔한 소스 코드가 없거나 단순히 찾을 수 없는 것일 수 있습니다. 저희에게 알려주시면 어떤 일이 발생했는지 알아보고 스캔 알고리즘을 개선할 수 있도록 도와드리겠습니다.

다음은 사용자가 직접 확인할 수 있는 몇 가지 사항입니다.

* 스캔한 디펜던시의 소스 코드는 실제로 스캔한 폴더에서 소스 코드로 사용할 수 있습니다. Conan과 같은 패키지 관리자를 사용하는 경우 소스 코드는 다른 프로젝트 디펜던시의 소스 코드와 함께 Conan 캐시에 있을 가능성이 높습니다. 패키지 매니저로 관리하는 디펜던시를 스캔하려면 빌드 중과 같이 \~\~_깨끗한 환경_\~\~에서 작업을 수행하는 것이 좋습니다.
* 디펜던시의 소스 코드는 OSS 구성 요소의 공식 릴리스에서 가져온 것이 아니며, Snyk 데이터베이스에 없습니다.
* OSS의 소스 코드를 너무 많이 수정하면 Snyk이 감지할 수 없습니다. 파일이 너무 적고 대부분을 수정하면 Snyk은 해당 파일을 데이터베이스의 구성 요소와 일치시킬 수 없습니다. 일반적인 수정의 예로는 공백 형식 지정, 라이선스 또는 저작권 헤더 추가 등이 있습니다.
* 현재 Windows 기준으로 Git이 개행문자를 Windows 개행문자로 변환했습니다. 현재 Snyk은 원래의 개행문자를 유지하고 있는 파일들을 인식할 수 있습니다.
* OSS 구성 요소의 소스 코드가 너무 최신입니다. Snyk 데이터베이스는 매월 새로 고쳐지지만 최신 릴리스가 처리되는 데 시간이 걸립니다.
