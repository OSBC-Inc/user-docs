# Bazel용 Snyk

Snyk은 Bazel에서 관리하는 디펜던시가 있는 테스트 프로젝트를 Snyk API를 통해 지원합니다.

{% hint style="info" %}
Snyk API 문서는 [https://snyk.docs.apiary.io/](https://snyk.docs.apiary.io)를 참조하십시오.
{% endhint %}

{% hint style="info" %}
**기능 지원 여부**\
Snyk API는 Business 및 Enterprise plans에서 사용할 수 있습니다. 자세한 내용은 [pricing plans](https://snyk.io/plans/)을 참조하십시오.
{% endhint %}

Dep Graph API에는 추가 권한이 필요합니다. 액세스를 요청하려면 support@snyk.io에 문의하십시오.

이 문서는 Snyk을 사용하여 Bazel 프로젝트를 테스트하는 방법을 설명합니다.

### Bazel 개요

[https://docs.bazel.build/versions/master/bazel-overview.html](https://docs.bazel.build/versions/master/bazel-overview.html)에 따르면 다음과 같이 소개되어 있습니다.

> _Bazel is an open-source build and test tool similar to Make, Maven, and Gradle. It uses a human-readable, high-level build language. Bazel supports projects in multiple languages and builds outputs for multiple platforms. Bazel supports large codebases across multiple repositories, and large numbers of users_

Bazel은 npm과 같은 패키지 매니저가 가지고 있는 디펜던시 매니페스트 파일이나 lockfile이 없습니다. 대신 빌드 구성은 Python3 기반의 도메인별 언어인 [Starlark](https://docs.bazel.build/versions/main/skylark/language.html)를 사용하여 [BUILD](https://docs.bazel.build/versions/main/build-ref.html#BUILD\_files) 파일에서 관리합니다.

Bazel은 npmjs.org 또는 Maven Central과 같은 패키지 레지스트리와의 기본 통합이 제한되어 있습니다. [Maven](https://docs.bazel.build/versions/main/external.html#maven-artifacts-and-repositories)과 같은 외부 레지스트리에서 디펜던시를 설치하는 데 도움이 되도록 추가할 수 있는 Bazel 규칙이 있습니다.

그러나 많은 경우 사용자는 모든 전이를 포함하여 종속성 정보(패키지 이름, 위치 및 버전)를 수동으로 지정해야 합니다. 그런 다음 빌드 중에 Bazel에서 가져올 수 있습니다.

Bazel 디펜던시는 Starlark를 사용하여 BUILD 파일에서 코드로 지정되기 때문에 Snyk은 프로젝트가 어떤 의존성을 가지고 있는지 쉽게 발견할 수 없습니다.

권장하는 접근 방식은 [Snyk Dep Graph Test API](https://github.com/snyk/dep-graph)를 통해 의존성을 테스트하는 것입니다.

### 작동 방식

1. 각 디펜던시 유형(Maven, Cocoapods 등)에 대해 모든 디펜던시 패키지 및 버전을 나열하는 [Dep Graph JSON object](https://github.com/snyk/dep-graph)를 생성합니다(아래 참조).
2.  Bazel 테스트 규칙의 일부로 이 객체를 POST request로 [Dep Graph Test API](https://support.snyk.io/hc/en-us/articles/360011549737-Snyk-for-Bazel#h\_01EEWFQJFTCWFQBMQR0X32J8B8)([auth token](https://docs.snyk.io/snyk-api-info/authentication-for-api) 포함)에 전송합니다. curl request를 예로 들면 다음과 같습니다.

    ```
    curl -X POST 'https://snyk.io/api/v1/test/dep-graph' \
      -H 'Authorization: token {{your token}}' \
      -H 'Content-Type: application/json; charset=utf-8' \
      -d @dep-graph.json
    ```
3. pass/fail 상태 및 그로 인한 취약점에 대한 [API response](https://support.snyk.io/hc/en-us/articles/360011549737-Snyk-for-Bazel#h\_01EEWP8F4MK9MFJT5X0A4ZGS93)를 확인합니다.

### Snyk Dep Graph Test API

Snyk Dep Graph Test API는 일반 디펜던시 그래프를 가져와 해당 디펜던시에 대한 관련 취약점이 포함된 보고서를 반환합니다.

지원하는 패키지 매니저/리포지토리 에코시스템의 목록은 [API documentation](https://snyk.docs.apiary.io/#reference/test/dep-graph/test-dep-graph)에서 확인할 수 있습니다. ( `deb`, `gomodules`, `gradle`, `maven`, `npm`, `nuget`, `paket`, `pip`, `rpm`, `rubygems` , `cocoapods`)

모든 Bazel 디펜던시는 API를 통해 테스트 가능합니다.

### Snyk Dep Graph JSON Syntax

Dep Graph Test API는 root 애플리케이션을 설명하는 [Snyk Dep Graph](https://github.com/snyk/dep-graph) JSON 객체와 직접 및 간접 의존성 그래프를 사용합니다.

해당 형식의 [schema](https://github.com/snyk/dep-graph#depgraphdata)는 다음과 같습니다.

```
export interface DepGraphData {
  schemaVersion: string;
  pkgManager: {
    name: string;
    version?: string;
    repositories?: Array<{
      alias: string;
    }>;
  };
  pkgs: Array<{
    id: string;
    info: {
      name: string;
      version?: string;
    };
  }>;
  graph: {
    rootNodeId: string;
    nodes: Array<{
      nodeId: string;
      pkgId: string;
      info?: {
        versionProvenance?: {
          type: string;
          location: string;
          property?: {
            name: string;
          };
        },
        labels?: {
          [key: string]: string | undefined;
        };
      };
      deps: Array<{
        nodeId: string;
      }>;
    }>;
  };
}
```

다음은 dep 그래프 객체의 특정 구성 요소에 대한 참고 사항입니다.

* `schemaVersion` - dep-graph 스키마 버전, `1.2.0`으로 설정
* `pkgManager.name` - `deb`, `gomodules`, `gradle`, `maven`, `npm`, `nuget`, `paket`, `pip`, `rpm`, `rubygems` 또는 `cocoapods` 중 하나
* `pkgs` - dep-graph에 있는 모든 `id`, `name` 및 `version`을 포함한 객체 배열입니다. `id`의 형식은 `name@version`이어야 합니다. 프로젝트 자체를 나타내는 항목을 포함하여 배열의 디펜던시를 나열합니다.
* `graph.nodes` - `pkgs`에 있는 항목 간의 관계를 설명하는 객체 배열입니다. Bazel에서 `deps`의 직접적인 디펜던시의 배열이며 정의된 다른 모든 패키지와 함께 프로젝트 노드입니다.
* `graph.rootNodeId` - 그래프의 root node로 사용할 `graph.nodes` 항목의 `id`를 지정합니다. 이것을 프로젝트 node의 `nodeId`로 설정해야 합니다.

### Snyk Dep Graph Test API Response

Dep Graph Test API는 dep graph 디펜던시에서 발견된 Issue(취약점 및 라이선스)를 설명하는 JSON 객체를 반환합니다.

다음 예시는 단일 취약점이 존재하는 API Response입니다.

```
{
    "ok": false,
    "packageManager": "maven",
    "issuesData": {
        "SNYK-JAVA-CHQOSLOGBACK-30208": {
            "CVSSv3": "CVSS:3.0/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H",
            "alternativeIds": [],
            "creationTime": "2017-03-19T14:58:38Z",
            "credit": [
                "Unknown"
            ],
            "cvssScore": 9.8,
            "description": "## Overview\n[ch.qos.logback:logback-core](https://mvnrepository.com/artifact/ch.qos.logback/logback-core) is a logback-core module.\n\nAffected versions of this package are vulnerable to Arbitrary Code Execution. A configuration can be ...",
            "disclosureTime": "2017-03-13T06:59:00Z",
            "exploit": "Not Defined",
            "fixedIn": [
                "1.1.11"
            ],
            "functions": [],
            "id": "SNYK-JAVA-CHQOSLOGBACK-30208",
            "identifiers": {
                "CVE": [
                    "CVE-2017-5929"
                ],
                "CWE": [
                    "CWE-502"
                ]
            },
            "language": "java",
            "mavenModuleName": {
                "artifactId": "logback-core",
                "groupId": "ch.qos.logback"
            },
            "modificationTime": "2020-06-12T14:36:56.271247Z",
            "moduleName": "ch.qos.logback:logback-core",
            "packageManager": "maven",
            "packageName": "ch.qos.logback:logback-core",
            "patches": [],
            "proprietary": false,
            "publicationTime": "2017-03-21T15:30:44Z",
            "references": [
                {
                    "title": "GitHub Commit #1",
                    "url": "https://github.com/qos-ch/logback/commit/f46044b805bca91efe5fd6afe52257cd02f775f8"
                },
                {
                    "title": "GitHub Commit #2",
                    "url": "https://github.com/qos-ch/logback/commit/979b042cb1f0b4c1e5869ccc8912e68c39f769f9"
                },
                {
                    "title": "Logback News",
                    "url": "https://logback.qos.ch/news.html"
                },
                {
                    "title": "NVD",
                    "url": "https://web.nvd.nist.gov/view/vuln/detail?vulnId=CVE-2017-5929"
                },
                {
                    "title": "NVD",
                    "url": "https://web.nvd.nist.gov/view/vuln/detail?vulnId=CVE-2017-5929/"
                }
            ],
            "semver": {
                "vulnerable": [
                    "[, 1.1.11)"
                ]
            },
            "severity": "high",
            "title": "Arbitrary Code Execution"
        }
    },
    "issues": [
        {
            "pkgName": "ch.qos.logback:logback-core",
            "pkgVersion": "1.0.13",
            "issueId": "SNYK-JAVA-CHQOSLOGBACK-30208",
            "fixInfo": {}
        }
    ],
    "org": {
        "id": "3e5fe3fe-9181-4f0f-a231-39764485e73f",
        "name": "stephen.elson-xnf"
    }
}
```

다음은 Response 객체의 구성 요소에 대한 참고 사항입니다.

* `ok` - Snyk에게 제공한 디펜던시에서 취약점을 발견했는지 여부를 요약하는 값입니다.
* `issuesData` - 발견된 취약점의 고유한 Hash값입니다. 각 취약점에는 `title`, `description`, `identifiers`, `publicationTime`, `severity` 등이 포함되어 있습니다.
* `issues` - `issuesData`의 취약점에서 패키지로의 간단한 매핑 배열입니다. 취약점은 여러 패키지와 관련될 수 있으므로 매핑은 response 길이를 최대한 짧게 유지하는데 사용합니다.

### 예

{% hint style="info" %}
**Note**\
Bazel Java 프로젝트 및 Snyk Dep Graph 객체는 [https://github.com/snyk/bazel-simple-app](https://github.com/snyk/bazel-simple-app)을 참조하십시오.
{% endhint %}

Maven 패키지에 대한 단일 디펜던시가 있는 간단한 Bazel 프로젝트의 경우 다음과 같이 디펜던시를 지정할 수 있습니다.

```
maven_jar(
    name = "logback-core",
    artifact = "ch.qos.logback:logback-core:1.0.13",
    sha1 = "dc6e6ce937347bd4d990fc89f4ceb469db53e45e",
)
```

이를 통해 다음과 같이 Dep Graph JSON 객체를 구성할 수 있습니다.

```
{
  "depGraph": {
    "schemaVersion": "1.2.0",
    "pkgManager": {
      "name": "maven"
    },
    "pkgs": [
      {
        "id": "app@1.0.0",
        "info": {
          "name": "app",
          "version": "1.0.0"
        }
      },
      {
        "id": "ch.qos.logback:logback-core@1.0.13",
        "info": {
          "name": "ch.qos.logback:logback-core",
          "version": "1.0.13"
        }
      }
    ],
    "graph": {
      "rootNodeId": "root-node",
      "nodes": [
        {
          "nodeId": "root-node",
          "pkgId": "app@1.0.0",
          "deps": [
            {
              "nodeId": "ch.qos.logback:logback-core@1.0.13"
            }
          ]
        },
        {
          "nodeId": "ch.qos.logback:logback-core@1.0.13",
          "pkgId": "ch.qos.logback:logback-core@1.0.13",
          "deps": []
        }
      ]
    }
  }
}
```

특정 패키지 (`ch.qos.logback:logback-core@1.0.13`)에는 JSON Response 객체에 자세히 설명된 취약점이 포함되어 있습니다.
