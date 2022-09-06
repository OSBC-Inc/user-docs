# Snyk fix를 사용한 자동 수정

{% hint style="info" %}
이 기능은 현재 베타 버전입니다. 피드백을 주시면 감사하겠습니다.  [snyk-fix-feedback@snyk.io](mailto:snyk-fix-feedback@snyk.io) 으로 문의하십시오.
{% endhint %}

{% hint style="info" %}
최신 버전의 CLI([v1.715.0](https://github.com/snyk/cli/releases/tag/v1.715.0) 이상)에 `snyk fix` 를 사용해야 합니다.
{% endhint %}

`synk fix` command는 지원되는 에코시스템에 대한 권장 업데이트를 자동으로 적용하는 새로운 CLI command입니다.

`snyk test` command를 사용하면 지원되는 에코시스템에 대한 실행 가능한 수정 사항이 다음 예와 같이 검색 결과에 나타납니다.

```
Tested 78 dependencies for known issues, found 34 issues, 145 vulnerable paths.Issues to fix by upgrading dependencies:  Upgrade django@2.2.13 to django@2.2.22 to fix
  ✗ HTTP Header Injection [High Severity][https://app.snyk.io/vuln/SNYK-PYTHON-DJANGO-1290072] in django@2.2.13
    introduced by django@2.2.13 and 13 other path(s)
  ✗ Directory Traversal (new) [High Severity][https://app.snyk.io/vuln/SNYK-PYTHON-DJANGO-1298665] in django@2.2.13
    introduced by django@2.2.13 and 13 other path(s)
  ✗ Insecure Permissions [High Severity][https://app.snyk.io/vuln/SNYK-PYTHON-DJANGO-609368] in django@2.2.13
    introduced by django@2.2.13 and 13 other path(s)
  ✗ Insecure Permissions [High Severity][https://app.snyk.io/vuln/SNYK-PYTHON-DJANGO-609369] in django@2.2.13
    introduced by django@2.2.13 and 13 other path(s)Organization:           libs
Package manager:        poetry
Target file:            lib/poetry.lock
Project name:           libs-develop
Open source:            no
Project path:           lib
Licenses:               enabled
```

다음은 `snyk fix` 실행의 출력 예를 보여 줍니다.

```
► Running `snyk test` for /Users/lili/www/snyk/python-fix/packages/poetry/test/system/workspaces/with-pins✔ Looking for supported Python items
✔ Processed 1 pyproject.toml items
✔ DoneSuccessful fixes:  ../python-fix/packages/poetry/test/system/workspaces/with-pins/poetry.lock
  ✔ Upgraded django from 2.2.13 to 2.2.18
  ✔ Upgraded jinja2 from 2.11.2 to 2.11.3Summary:
  1 items were successfully fixed
  10 issues: 4 High | 3 Medium | 3 Low
  10 issues are fixable
  10 issues were successfully fixed
```

**주의**: 성공적인 테스트 결과만 `synk fix` 로 전달됩니다. 또한 지원되지 않는 모든 에코시스템 테스트 결과는 건너뜁니다.

### snyk fix 실행

베타 기간 동안 snyk fix를 활성화하려면 **Settings** [![](https://github.com/snyk/user-docs/raw/5e52535b78618f57eda40eb08fc8fbf91e16f1f0/docs/.gitbook/assets/cog\_icon.png)](https://github.com/snyk/user-docs/blob/5e52535b78618f57eda40eb08fc8fbf91e16f1f0/docs/.gitbook/assets/cog\_icon.png) > **Snyk Preview** 를 클릭합니다. **synk fix 기능**을 **Enabled**하고 **Save changes를** 클릭합니다.

![Snyk Preview settings에서 Snyk fix를 Enabled](https://github.com/snyk/user-docs/raw/5e52535b78618f57eda40eb08fc8fbf91e16f1f0/docs/.gitbook/assets/cleanshot\_2021-07-02\_at\_11.39.43\_2x.png)

`snyk fix` command는 모든 `snyk test` command 옵션을 지원하며 다음과 같은 추가 옵션이 있습니다:

* **`--`**`quiet` \*\*\*\* - command line에 대한 모든 출력을 억제합니다.
* `--dry-run` - 거의 모든 로직을 실행하고 출력을 표시하되, 관련 파일을 최종 변경하지 마십시오. 변경 사항의 미리 보기를 표시합니다.
* `--sequential` - 각 디펜던시 업데이트를 한 번에 하나씩 별도로 설치합니다(기본값은 한 번에 모두 설치). 기본값은 훨씬 느리지만 일부 업데이트가 실패해 프로세스가 계속 진행되도록 허용하여 성공적인 업데이트 수를 늘리는 데 도움이 됩니다.

### 파이썬 지원

* `requirements.txt` 파일(또는 사용자 지정 파일(예: `prod.txt`))이 포함된 Pip 프로젝트
* `Pipfile` \*\*\*\* 및 \*\*\*\* `Pipfile.lock` 파일이 포함된 Pipenv 프로젝트
* `pyproject.toml` \*\*\*\* and `Poetry.lock` 파일을 사용한 Poetry 프로젝트

### 사용 예

`snyk fix --file=requirements.txt`

`snyk fix --file=base.txt --package-manager=pip`

`snyk fix --all-projects`

### `-r` 지시문이 있는 요구 사항

`requirements.txt` 가 이렇게 표시되는 경우, 필요한 경우 `base.txt` 와 `requirements.txt` 가 모두 업데이트됩니다:

```
-r base.txt # this means grab all the dependencies from here
django===1.6.1
```

**Direct dependency 업그레이드 (매니페스트에 명시된 디펜던시)**

Direct dependency 업그레이드는 관련 파일에 적용됩니다. 참조된 모든 파일이 발견되고 업데이트됩니다.

**Pins (Direct dependency  통해 가져온 Transitive dependency)**

Pins  테스트된 매니페스트 파일에 적용됩니다.

여러 파일이 테스트되었지만 관련성이 있는 경우(예: 한 파일이 다른 파일을 필요로 함), Snyk은 디렉터리 구조에서 더 높은 위치에 있는 파일에 변경 사항을 적용하기 시작합니다.

Snyk은 이전에 수정된 파일을 감지하고 수정 사항을 적용하는 것을 다시 건너뜁니다.

### `constraints.txt`를 사용하는 프로젝트

제약 조건 파일은 설치 여부가 아니라 설치된 종속성의 버전만 제어하는 요구 사항 파일입니다. 구문과 내용은 요구 사항 파일과 거의 동일합니다. 한 가지 중요한 차이점이 있습니다. 제약 조건 파일에 패키지를 포함해도 패키지 설치가 트리거되지 않습니다. 자세한 내용은 사용 설명서 - [pip documentation v21.0.1.](https://pip.pypa.io/en/stable/user\_guide/#constraints-files)을 참조하세요.

**Direct dependency 업그레이드 (매니페스트에 명시된 디펜던시)**

Direct dependency 업그레이드는 관련 파일에 적용됩니다. 참조된 모든 파일이 발견되고 업데이트됩니다.

**Pins (Direct dependency  통해 가져온 Transitive dependency)**

모든 Transitive dependency은 요구 사항 매니페스트 파일에서 `-c` 지시문과 함께 참조되는 경우 `constraints.txt` 파일에 고정됩니다.

#### Python (`pipenv`)

Snyk은 지정된 권장 버전에 대한 디펜던시를 업데이트하기 위해 직접 `pipenv`에 위임합니다. 모든 `pipenv` 환경 변수와 동작은 최대한 보존됩니다.

#### Python (`poetry`)

Snyk은 지정된 권장 버전에 대한 디펜던시를 업데이트하기 위해 `poetry`에 직접 위임합니다. 모든 `poetry` 환경 변수와 동작은 최대한 보존됩니다.

### issue 해결

디버그 모드에서 실행하여 오류에 대한 자세한 정보를 얻으십시오.

```
DEBUG=*snyk* snyk fix
```

이것은 issue 진단에 도움이 되거나 디버깅을 위해 Snyk으로 보낼 수 있는 매우 자세한 출력을 제공합니다.
