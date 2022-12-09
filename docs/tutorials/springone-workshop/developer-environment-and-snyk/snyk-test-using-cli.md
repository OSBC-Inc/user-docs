# CLI를 사용한 Snyk Test

## SPC 애플리케이션 테스트

SPC 애플리케이션의 루트 디렉터리에서 아래의 Snyk 명령을 실행합니다. Snyk test 명령은 취약점에 대한 디펜던시를 테스트하고 발견된 취약점 수를 알려줍니다.

```
snyk test
```

{% hint style="info" %}
Snyk CLI는 특정 사례 및 출력 포맷을 위한 여러 스위치를 제공합니다.
{% endhint %}

{% hint style="info" %}
애플리케이션을 빌드하지 않았기 때문에 스캔 시간이 더 오래 걸립니다. 2분 정도 소요됩니다. 응용 프로그램을 패키징한 경우 스캔하는 데 30초가 걸립니다.
{% endhint %}

### Snyk test 실행 결과

Snyk test는 수정 가능한 Issue와 수정 불가능한 Issue, 라이선스 컴플라이언스 Issue로 그룹화된 취약점 목록을 표시합니다. 잠시 시간을 내어 아래 결과와 유사한 출력을 검토하십시오. Snyk은 수정 가능한 취약점에 대한 fixG 조안 제공합니다.

```
Tested 83 dependencies for known issues, found 22 issues, 22 vulnerable paths.


Issues to fix by upgrading:

  Upgrade org.webjars:bootstrap@3.3.6 to org.webjars:bootstrap@3.4.1 to fix
  ✗ Cross-site Scripting (XSS) [Medium Severity][https://snyk.io/vuln/SNYK-JAVA-ORGWEBJARS-451160] in org.webjars:bootstrap@3.3.6
  ✗ Cross-site Scripting (XSS) [Medium Severity][https://snyk.io/vuln/SNYK-JAVA-ORGWEBJARS-451162] in org.webjars:bootstrap@3.3.6
  ✗ Cross-site Scripting (XSS) [Medium Severity][https://snyk.io/vuln/SNYK-JAVA-ORGWEBJARS-451164] in org.webjars:bootstrap@3.3.6
  ✗ Cross-site Scripting (XSS) [Medium Severity][https://snyk.io/vuln/SNYK-JAVA-ORGWEBJARS-451168] in org.webjars:bootstrap@3.3.6
  ✗ Cross-site Scripting (XSS) [Medium Severity][https://snyk.io/vuln/SNYK-JAVA-ORGWEBJARS-479505] in org.webjars:bootstrap@3.3.6
```

## Synk Test 사용의 추가 예

### 컨테이너 이미지 테스트

로컬 컨테이너 이미지를 테스트합니다. 이미지를 로컬에서 사용할 수 없는 경우, Snyk은 Docker Hub에서 이미지를 가져오려고 시도합니다.

```
snyk test --docker openjdk:8
```

{% hint style="info" %}
이 스캔은 이미지를 다운로드하는 데 약 30초가 걸립니다.
{% endhint %}

### public 저장소 테스트를 사용하기 전에 테스트

public GitHub, BitBucket 또는 GitLab 저장소를 테스트하려면 `snyk test`를 실행하고 GitHub URL을 repo에 포함하십시오.

```
snyk test https://github.com/snyk/goof
```

다음 git URL 형식이 지원됩니다.

* `git://github.com/user/project.git#commit-ish`
* `https://github.com/user/project#commit-ish`
* `user/project#commit-ish`
