# Snyk Code CLI 결과 이해

## Snyk Code 테스트 예시

이 예제는 로컬 프로젝트(`goof`)에 대해 snyk code 테스트를 실행합니다.

```
snyk code test goof
```

이렇게 하면 다음과 같은 결과가 나타납니다.

```
Testing goof ...

 ✗ [Medium] Use of Hard-coded Credentials
     Path: typeorm-db.js, line 11
     Info: Do not hardcode credentials in code. Found hardcoded credential used in typeorm.createConnection.

 ✗ [Medium] Use of Hard-coded Credentials
     Path: typeorm-db.js, line 12
     Info: Do not hardcode passwords in code. Found hardcoded password used in typeorm.createConnection.

 ✗ [Medium] Cleartext Transmission of Sensitive Information
     Path: app.js, line 12
     Info: http (used in require) is an insecure protocol and should not be used in new code.

 ✗ [Medium] Allocation of Resources Without Limits or Throttling
     Path: routes/index.js, line 77
     Info: This endpoint handler performs a system command execution and does not use a rate-limiting mechanism. It may enable the attackers to perform Denial-of-service attacks. Consider using a rate-limiting middleware such as express-limit.

 ✗ [Medium] Allocation of Resources Without Limits or Throttling
     Path: routes/index.js, line 166
     Info: This endpoint handler performs a file system operation and does not use a rate-limiting mechanism. It may enable the attackers to perform Denial-of-service attacks. Consider using a rate-limiting middleware such as express-limit.

 ✗ [Medium] Allocation of Resources Without Limits or Throttling
     Path: routes/index.js, line 223
     Info: This endpoint handler performs a file system operation and does not use a rate-limiting mechanism. It may enable the attackers to perform Denial-of-service attacks. Consider using a rate-limiting middleware such as express-limit.

 ✗ [Medium] Information Exposure
     Path: app.js, line 27
     Info: Disable X-Powered-By header for your Express app (consider using Helmet middleware), because it exposes information about the used framework to potential attackers.

 ✗ [High] Command Injection
     Path: routes/index.js, line 86
     Info: Unsanitized input from the HTTP request body flows into child_process.exec, where it is used to build a shell command. This may result in a Command Injection vulnerability.

 ✗ [High] SQL Injection
     Path: routes/index.js, line 39
     Info: Unsanitized input from the HTTP request body flows into find, where it is used in an SQL query. This may result in an SQL Injection vulnerability.

 ✗ [High] Cross-site Scripting (XSS)
     Path: routes/index.js, line 109
     Info: Unsanitized input from the HTTP request body flows into send, where it is used to render an HTML page returned to the user. This may result in a Cross-Site Scripting attack (XSS).

 ✗ [High] Hardcoded Secret
     Path: app.js, line 73
     Info: Avoid hardcoding values that are meant to be secret. Found a hardcoded string used in here.

✔ Test completed

Organization:      free-plan-org
Test type:         Static code analysis
Project path:      goof

11 Code issues found
4 [High]  7 [Medium]
```

## 결과 검토

snyk code 테스트에서 11개의 Issue(high 4개, medium 7개)를 발견했습니다.

Issue는 가장 높은 심각도의 Issue가 맨 아래에 있도록 정렬됩니다.

각 항목에는 다음이 포함됩니다.

* Issue의 심각도 및 취약점 유형
* 경로: Issue가 발견된 파일의 경로 및 행 (potentially issues are cross-files, the location in the path refers to the issue's sink)
* 정보: Issue의 데이터 흐름에 대한 설명

Snyk용 CLI는 [CLI reference](https://docs.snyk.io/snyk-cli/cli-reference#exit-codes)에 설명된 대로 exit code들을 사용합니다.
