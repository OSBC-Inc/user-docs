# 무시

## 사용법

`snyk ignore --id=<ISSUE_ID> [--expiry=] [--reason=] [--policy-path=<PATH_TO_POLICY_FILE>] [--path=<PATH_TO_RESOURCE>] [OPTIONS]`

또는

`snyk ignore [--expiry=] [--reason=] [--policy-path=<PATH_TO_POLICY_FILE>] --file-path=<PATH_TO_RESOURCE>] [OPTIONS]`

## 설명

`snyk ignore` 명령은는 모든 snyk ID에 따라 명시된 issue를 무시하거나 파일 시스템의 경로를 무시하도록 `.snyk` 정책 파일을 수정합니다.

그러면 다음과 유사한 블록이 포함되도록 로컬 `.snyk` 파일이 업데이트됩니다.:

```yaml
ignore:
  '<ISSUE_ID>':
    - '*':
        reason: <REASON>
        expires: <EXPIRY>
```

`--path` 옵션을 사용하는 경우 블록은 다음과 유사합니다.

```yaml
ignore:
  '<ISSUE_ID>':
    - '<PATH_TO_RESOURCE>':
        reason: <REASON>
        expires: <EXPIRY>
```

`--file-path` 옵션을 사용하는 경우 블록은 다음과 유사합니다.

```yaml
exclude:
  '<GROUP>':
    - <FILE MATCHING-PATTERN>
    - <FILE MATCHING-PATTERN>:
      reason: <REASON>
      expires: <EXPIRY>
      created: <CREATION TIME>
```

## Debug

`-d`옵션을 사용하여 디버그 로그를 출력합니다.

## 옵션

### `--id=<ISSUE_ID>`

무시할 Issue의 Snyk ID, --file-path와 함께 사용되는 경우 생략됩니다. 다른 사용 사례에서 필요합니다.

### `--expiry=<EXPIRY>`

`YYYY-MM-DD` 형식의 만료 날짜입니다.

지원되는 형식:

[ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html)

[RFC 2822](https://tools.ietf.org/html/rfc2822)

기본값: 30일 또는 `--file-path`와 함께 사용하는 경우 없음

### `--reason=<REASON>`

이 Issue를 무시하려면 Human-readable `<REASON>` 이여야 합니다.

기본값: 없음

### `--policy-path=<PATH_TO_POLICY_FILE>`

수동으로 전달할 `.snyk` 정책 파일의 경로입니다.

기본값: 없음

### `--path=<PATH_TO_RESOURCE>`

Issue를 무시할 depgraph 내의 리소스 경로입니다.

무시 규칙의 범위를 좁힐 때 사용합니다. 리소스 경로를 지정하지 않으면 모든 리소스가 무시됩니다.

사용하는 경우 `--policy-path` 옵션을 따릅니다.

기본값: 모두

### `--file-path=<PATH_TO_RESOURCE>`

Issue를 무시할 파일 시스템입니다. `snyk code` 및 `snyk test --unmanaged` 에서 사용

기본값: none

### `--file-path-group=[global|code|iac-drift]`

`--file-path`와 함께 사용되는 그룹화, 그렇지 않으면 생략됩니다.

기본값: 전역

## snyk ignore 명령의 예

### 특정 취약점 무시

```
$ snyk ignore --id='npm:qs:20170213' --expiry='2021-01-10' --reason='Module not affected by this vulnerability'
```

### 리소스 경로가 지정된 특정 취약점 무시

```
$ snyk ignore --id='SNYK-JS-PATHPARSE-1077067' --expiry='2021-01-10' --path='nyc@11.9.0 > istanbul-lib-report@1.1.3 > path-parse@1.0.5' --reason='Module not affected by this vulnerability'
```

### 30일 동안 특정 취약점 무시

```
$ snyk ignore --id=npm:tough-cookie:20160722
```

### 2031-01-20까지 특정 파일 무시

2031-01-20까지 `snyk test --unmanaged`에서 사용되는 특정 파일을 무시하고 설명은 향후 참조로 사용하십시오.

```
$ snyk ignore --file-path='./deps/curl-7.58.0/src/tool_msgs.c' --expiry='2031-01-20' --reason='patched file'
```

### glob 표현식을 사용하여 파일 또는 폴더 무시

특정 그룹에 추가하여 glob 표현식과 일치하는 파일을 무시합니다. Snyk Code에 적용됩니다. Snyk Open Source, Container, 또는 Infrastructure as Code적용되지 않습니다.

```
$ snyk ignore --file-path='./**/vendor/**/*.cpp' --file-path-group='global'
```
