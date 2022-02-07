# Snyk for Bazel

Snyk은 Bazel에서 관리하는 디펜던시가 있는 테스트 프로젝트를 Snyk API를 통해 지원합니다.

{% hint style="info" %}
Snyk API 문서는 [https://snyk.docs.apiary.io/](https://snyk.docs.apiary.io)를 참조하세요.
{% endhint %}

{% hint style="info" %}
**기능 지원 여부**\
Snyk API는 Business 및 Enterprise plans에서 사용할 수 있습니다. 자세한 내용은 [pricing plans](https://snyk.io/plans/)을 참조하세요
{% endhint %}

Dep Graph API에는 추가 권한이 필요합니다. 액세스를 요청하려면 support@snyk.io에 문의하세요.

이 문서는 Snyk을 사용하여 Bazel 프로젝트를 테스트하는 방법을 제공합니다.

## Bazel Overview

[https://docs.bazel.build/versions/master/bazel-overview.html](https://docs.bazel.build/versions/master/bazel-overview.html)에 따르면 다음과 같이 소개되어 있습니다.

> _Bazel is an open-source build and test tool similar to Make, Maven, and Gradle. It uses a human-readable, high-level build language. Bazel supports projects in multiple languages and builds outputs for multiple platforms. Bazel supports large codebases across multiple repositories, and large numbers of users_

Bazel은 npm과 같은 패키지 매니저가 가지고 있는 디펜던시 매니페스트 파일이나 lockfile을 가지고 있지 않습니다. 대신 빌드 구성은 Python3 기반의 도메인별 언어인 [Starlark](https://docs.bazel.build/versions/main/skylark/language.html)를 사용하여 [BUILD](https://docs.bazel.build/versions/main/build-ref.html#BUILD\_files) 파일에서 관리합니다.

Bazel은 npmjs.org 또는 Maven Central과 같은 패키지 레지스트리와 제한적으로 통합됩니다. [Maven](https://docs.bazel.build/versions/main/external.html#maven-artifacts-and-repositories)과 같은 외부 레지스트리에서 디펜던시를 설치하는 데 도움이 되도록 추가할 수 있는 Bazel 규칙이 있습니다.

그러나 많은 경우 사용자는 모든 전이를 포함하여 종속성 정보(패키지 이름, 위치 및 버전)를 수동으로 지정해야 한다. 그런 다음 빌드 중에 Bazel에서 가져올 수 있습니다.

Bazel 디펜던시는 Starlark를 사용하여 BUILD 파일에서 코드로 지정되기 때문에 Snyk은 프로젝트가 어떤 의존성을 가지고 있는지 쉽게 발견할 수 없다.

권장하는 접근방식은 [Snyk Dep Graph Test API](https://github.com/snyk/dep-graph) 통해 의존성을 테스트하는 것입니다.

## How it works

1. For each type of dependency (e.g. Maven, Cocoapods), create a [Dep Graph JSON object](https://github.com/snyk/dep-graph) listing all the dependency packages and versions (see below)
2.  As part of a Bazel test rule, send this object as a POST request to the [Dep Graph Test API](https://support.snyk.io/hc/en-us/articles/360011549737-Snyk-for-Bazel#h\_01EEWFQJFTCWFQBMQR0X32J8B8), (along with your [auth token](https://docs.snyk.io/snyk-api-info/authentication-for-api)), example curl request:

    ```
    curl -X POST 'https://snyk.io/api/v1/test/dep-graph' \
      -H 'Authorization: token {{your token}}' \
      -H 'Content-Type: application/json; charset=utf-8' \
      -d @dep-graph.json
    ```
3. Check the [API response](https://support.snyk.io/hc/en-us/articles/360011549737-Snyk-for-Bazel#h\_01EEWP8F4MK9MFJT5X0A4ZGS93) for pass/fail status and any resulting vulnerabilities

## Snyk Dep Graph Test API

The Snyk Dep Graph Test API takes a generic dependency graph, and returns a report containing any relevant vulnerabilities for those dependencies.

The set of supported package managers/repository ecosystems are listed on the [API documentation](https://snyk.docs.apiary.io/#reference/test/dep-graph/test-dep-graph) (at time of writing these are `deb`, `gomodules`, `gradle`, `maven`, `npm`, `nuget`, `paket`, `pip`, `rpm`, `rubygems` & `cocoapods`).

Any of your Bazel dependencies that are available in these ecosystems can be tested via the API.

## Snyk Dep Graph JSON Syntax

The Dep Graph Test API takes a [Snyk Dep Graph](https://github.com/snyk/dep-graph) JSON object describing the root application, and the graph of direct and transitive dependencies.

The [schema](https://github.com/snyk/dep-graph#depgraphdata) for this format is as follows:

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

Here are some further notes on specific components in the dep graph object:

* `schemaVersion` - version of the dep-graph schema, set this to `1.2.0`
* `pkgManager.name` - one of `deb`, `gomodules`, `gradle`, `maven`, `npm`, `nuget`, `paket`, `pip`, `rpm`, `rubygems` or `cocoapods`
* `pkgs` - array of objects containing `id`, `name` & `version` of all packages in the dep-graph. Note that the `id` _must_ be of the form `name@version`. List each of your dependencies in this array, including an item representing the project itself
* `graph.nodes` - array of objects describing the relationships between entries in `pkgs`. In Bazel this is typically just the project node with all other packages defined as a flat array of direct dependencies in `deps`
* `graph.rootNodeId` - specifies the `id` of the entry in `graph.nodes` to use as the root node of the graph. You should set this to the `nodeId` of the project node

## Snyk Dep Graph Test API Response

The Dep Graph Test API returns a JSON object describing any issues (vulnerabilities & licences) found in the dep graph dependencies.

Here is an example response with a single vulnerability.

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

Here are some further notes on specific components in the response object:

* `ok` - boolean value summarising whether Snyk found any vulnerabilities in the supplied dependencies. You can use this for a quick pass/fail test
* `issuesData` - a hash of each unique vulnerability found. Each vulnerability contains many useful properties, such as `title`, `description`, `identifiers`, `publicationTime`, `severity` etc
* `issues` - an simple array of mappings from vulnerabilities in `issuesData` to package. As a vulnerability may be relevant to multiple packages, this mapping is used to keep the response length as short as possible

## Examples

{% hint style="info" %}
**Note**\
See [https://github.com/snyk/bazel-simple-app](https://github.com/snyk/bazel-simple-app) for a full example Bazel Java project, and corresponding Snyk Dep Graph object.
{% endhint %}

For a simple Bazel project with a single dependency on a Maven package, you may specify the dependency like this:

```
maven_jar(
    name = "logback-core",
    artifact = "ch.qos.logback:logback-core:1.0.13",
    sha1 = "dc6e6ce937347bd4d990fc89f4ceb469db53e45e",
)
```

From this you could construct the following Dep Graph JSON object:

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

This particular package (`ch.qos.logback:logback-core@1.0.13`) contains a vulnerability, described in detail in the resulting JSON response object.
