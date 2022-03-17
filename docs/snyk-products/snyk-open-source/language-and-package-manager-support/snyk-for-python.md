# Python용 Snyk

Snyk은 CLI 및 애플리케이션 UI(app.snyk.io)를 통해 취약점에 대한 보안 스캔을 제공합니다.

이 문서는 Snyk을 사용하여 Python 프로젝트를 스캔하는 방법을 제공합니다.

## 특징

{% hint style="info" %}
요금제에 따라서 기능을 사용하지 못할 수 있습니다.
{% endhint %}

| Package managers / Features                          | CLI support | Git support | License scanning | Fixing | <p>Runtime</p><p>monitoring</p> |
| ---------------------------------------------------- | ----------- | ----------- | ---------------- | ------ | ------------------------------- |
| [Pip and PyPI](https://pypi.org/project/pip/)        | ✔︎          | ✔︎          | ✔︎               | ✔︎     |                                 |
| [pipenv](https://pipenv.kennethreitz.org/en/latest/) | ✔︎          |             | ✔︎               |        |                                 |
| setup.py                                             | ✔︎          |             | ✔︎               | ✔︎     |                                 |
| [Poetry](https://python-poetry.org)                  | ✔︎          |             | ✔︎               | ✔︎     |                                 |

{% hint style="info" %}
PyPI 라이선스는 모든 Python 프로젝트에서 지원합니다.
{% endhint %}

## 작동 방식

트리를 구축한 후에는 [vulnerability database](https://snyk.io/vuln)를 사용하여 디펜던시 트리의 모든 패키지에서 취약점을 찾을 수 있습니다.

{% hint style="info" %}
디펜던시를 스캔하려면 먼저 관련 패키지 매니저를 설치했는지, 프로젝트에 지원되는 매니페스트 파일이 포함되어 있는지 확인해야 합니다.
{% endhint %}

Snyk이 트리를 분석하고 빌드하는 방법은 프로젝트의 언어 및 패키지 매니저와 프로젝트 위치에 따라 다릅니다.

## Python 프로젝트에서 Snyk CLI 사용하기

Snyk이 트리를 분석하고 구축하는 방식은 프로젝트의 언어 및 패키지 매니저에 따라 다릅니다.

## Pip

Snyk은 테스트를 실행하기 위해 전체 중첩 디펜던시 트리가 필요합니다. Requirements.txt 파일에는 최상위 종속성만 포함되며 중첩 또는 전이 종속성은 포함되지 않습니다. 정확성을 보장하는 가장 효율적인 방법은 전체 pip 프로젝트를 설치하는 것입니다.

Snyk은 연결되지 않는 별도의 디펜던시 트리가 아닌 해당 특정 서비스/제품에 사용된 특정 pip 설치에 대해 테스트를 실행합니다.

전체 디펜던시 트리를 스캔하기 위해서 Snyk은 설치된 패키지를 분석하여 누락된 패키지가 없는지 확인합니다. 이는 매니페스트 파일에 명시적으로 지정하지 않는 경우에도 발생합니다.

## Pipenv

디펜던시 트리를 빌드하려면 Snyk이 필요로하는 `pipenv install` 명령어를 실행하여 `pipenv graph`를 생성한 다음 디펜던시 검색이 자동으로 수행하도록 합니다.

Snyk은 빌드된 디펜던시 트리를 사용하여 `pipfile`을 분석합니다.

## setup.py

디펜던시 트리를 구축하기 위해 Snyk은 `setup.py` 파일을 분석하고 `install_requires` 키에 나열된 패키지를 감지합니다.

이 파일에는 자동 검색이 없으므로 수동으로 지정해야 합니다.

```
snyk test --file=setup.py
```

패키지를 가상 환경에 설치한 다음 pip freeze를 실행하여 seup.py를 requirements.txt로 변환할 수 있습니다.

## Poetry

Python Poetry 애플리케이션에서 문제를 찾기 위해 Snyk은 pyproject.toml 및 poety.lock 파일을 사용합니다. 이 두 파일은 모두 Snyk이 Poetry 디펜던시를 식별하고 문제를 테스트하기 위해 존재해야 합니다.

## 추가 지원 세부정보

```
https://github.com/snyk/snyk-python-plugin/blob/master/lib/types.ts
```

## CLI parameters for Python

### 전제 조건

* Snyk CLI를 사용하기 전에 관련 패키지 매니저를 설치하십시오.
* 테스트 진행 이전에 Snyk에서 지원하는 관련 매니페스트 파일을 포함합니다.
* [Snyk CLI](../../../features/snyk-cli/install-the-snyk-cli/)를 설치하고 인증하여 로컬 환경에서 프로젝트 분석을 시작합니다.

### Parameters

Python 프로젝트에서 취약점을 스캔할 때 다음 옵션을 사용할 수 있습니다.

| Option                  | Description                                                                                                                                                                                                                                                                                                                        |
| ----------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `--command=`            | <p>Snyk은 디펜던시를 스캔하고 찾기위해 Python을 사용합니다. Snyk은 스캔을 시작하려면 Python 버전이 필요하면 기본값은 "python"입니다.</p><p>여러 Python 버전을 사용하는 경우 해당 옵션을 사용하여 실행할 Pyhton 버전을 지정하세요.</p><p>예: <code>snyk test --command=python3</code></p><p>자세한 내용은 <a href="snyk-for-python.md">Using different Python versions</a>를 참조하십시오.</p>                              |
| `--skip-unresolved=`    | environment에서 패키지를 찾을 수 없는 경우 패키지를 건너뜁니다.(예: 스캔을 실행하는 시스템에서 액세스할 수없는 개인 패키지).                                                                                                                                                                                                                                                      |
| `--file=`               | <p>테스트할 특정 파일을 지정합니다. 기본적으로 Snyk은 프로젝트의 최상위 경로에서 requirements.txt. 파일을 검색합니다.</p><p>이 옵션과 함깨 명시적으로 지정된 경우 Snyk은 req.txt.라는 모든 매니페스트 파일을 인식할 수 있습니다.</p><p>예를 들어, Snyk은 매니페스트 파일의 이름을 requirements-dev.txt.로 변경했을 때 이를 인식합니다.</p><p><strong>Note</strong>: 파일 이름이 requirements.txt가 아닌 경우 --package-manager=pip를 cmd에 추가해야 합니다.</p> |
| `--package-manager=pip` | 이 파라미터는 requirements.txt. 파일이 아닌 파일을 지정하는 경우 사용합니다. 이 파라미터가 없으면 테스트가 실패합니다. pip값으로 이 파라미터를 지정합니다.                                                                                                                                                                                                                                  |

## Python 프로젝트를 위한 Git Services

Python 프로젝트는 Snyk이 지원하는 모든 Git 저장소에서 가져올 수 있습니다.

pip를 패키지 매니저로 사용하여 Python 프로젝트를 테스트하기 위해 `requirements.txt`파일을 분석하므로 가져오기 전에 이 파일이 저장소에 있어야 합니다.

`requirements.txt`의 파일 이름을 변경한 경우(예: `requirements-dev.txt`로 변경) `**/requirements/*.txt` 규칙을 따르는 모든 파일을 Python 프로젝트로 가져오려고 합니다.

파일을 requirements 폴더에 배치한 경우(예: `requirements/requirements.txt` 파일을 배치한 경우) `**/requirements/*.txt` 규칙을 따르는 모든 파일을 Python 프로젝트로 가져오려고 합니다.

requirements가 아닌 다른 매니페스트 파일 형식을 생성하는 패키지 매니저를 사용하는 경우 매니페스트 파일을 requirements.txt 형식으로 변환하거나 가져옵니다(패키지 매니저/지원 파일에 따라 다름).

예제는 다음과 같습니다.

```
dephell deps convert --from=conda --to=requirements.txt
```

## 다른 Python 버전 사용

일부 Python 프로젝트에는 Python 3에서만 유효한 디펜던시가 있을 수 있습니다. 기본적으로 Snyk은 Python 2로 스캔합니다.

CLI 와 Git 모두에서 디펜던시를 스캔하기 위해 Snyk에서 사용하는 Python 버전을 조정할 수 있습니다.

## CLI에서 Python 버전 설정

다음 파라미터를 `snyk test` 또는 `snyk monitor` 시 입력합니다.

```
--command=python3
```

`.snyk` [정책 파일](../../../features/snyk-cli/test-for-vulnerabilities/the-.snyk-file.md)에 다음 옵션을 추가하여 특정 Python 버전을 지정할 수 있습니다.

```
language-settings:
python: '3.7.2'
```

## Git 프로젝트에서 Python 버전 설정

{% hint style="info" %}
Git에서 가져온 프로젝트를 테스트할 때 Snyk은 Python 2 또는 Python 3의 최신 버전(예: 2.7.4 또는 3.7.4)을 사용합니다.
{% endhint %}

기본적으로 Snyk은 Python 2를 사용하여 테스트합니다.

Snyk이 Git에서 가져온 프로젝트를 테스트 하는데 사용하는 Python 주 버전을 정의하려면 조직 설정 또는 `.snyk` [정책 파일](../../../features/snyk-cli/test-for-vulnerabilities/the-.snyk-file.md)을 사용하세요.

조직의 모든 프로젝트에 대한 Python 버전을 정의하려면 다음과 같이 진행합니다.

1. 정에 로그인하고 관리할 관련 그룹 및 조직으로 이동합니다.
2. 설정 ![](../../../.gitbook/assets/cog\_icon.png) > **Languages**.
3. **Edit settings** for **Python**을 클릭합니다.
4. 이 조직의 프로젝트를 테스트할 때 **Python 2** 또는 **Python 3**을 사용하도록 선택합니다.

![](../../../.gitbook/assets/mceclip1-18-.png)

다른 Python 버전으로 작업하려면 다른 조직을 만드는 것을 권장합니다..

하나의 조직을 사용하고 싶지만 프로젝트에서 다른 Python 버전을 사용해야 하는 경우 프로젝트 저장소에 `.snyk` 파일을 추가하고 원하는 버전을 지정할 수 있습니다.

`.snyk` 파일은 프로젝트 매니페스트 파일과 동일한 디렉토리에 존재해야 합니다.

## 메이저 및 마이너 버전

`.snyk` 파일을 찾을 때 Snyk은 지정된 메이저 버전을 감지하고 이를 사용하여 프로젝트가 Python 2 또는 Python 3으로 테스트되는지 여부를 확인합니다. 따라서 정확한 버전을 사용하지 않습니다.

예를 들어 Git을 통해 가져온 프로젝트의 경우 다음과 같이 진행합니다.

```
language-settings:
python: '3.7.2'
```

이 예제는 Snyk에 최신 버전의 Python 3을 사용하도록 지시하지만 Snyk은 지정된 마이너 버전 및 패치 버전을 사용하지 않습니다.
