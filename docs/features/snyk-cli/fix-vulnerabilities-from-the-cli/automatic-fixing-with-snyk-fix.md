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

베타 기간 동안 snyk fix를 활성화하려면 **Settings** [![](https://github.com/snyk/user-docs/raw/5e52535b78618f57eda40eb08fc8fbf91e16f1f0/docs/.gitbook/assets/cog\_icon.png)](https://github.com/snyk/user-docs/blob/5e52535b78618f57eda40eb08fc8fbf91e16f1f0/docs/.gitbook/assets/cog\_icon.png) > **Snyk Preview** 를 클릭합니다. **synk 수정 기능**을 실행하고 **변경 사항 저장**을 클릭합니다.

![](https://github.com/snyk/user-docs/raw/5e52535b78618f57eda40eb08fc8fbf91e16f1f0/docs/.gitbook/assets/cleanshot\_2021-07-02\_at\_11.39.43\_2x.png)

The `snyk fix` command supports all the `snyk test` command options and has the following additional options:

* **`--`**`quiet` \*\*\*\* - Suppress all output to the command line.
* `--dry-run` - Run almost all the logic and display output, but do not make the final changes to the relevant files. Show a preview of the changes.
* `--sequential` - Install each dependency update separately one at a time (the default is to install all at once). The default is much slower, but helps increase the number of successful updates by allowing some updates to fail and the process to continue.

### Python support

* Pip projects with `requirements.txt` files (or custom named files, for example `prod.txt`)
* Pipenv projects with `Pipfile` \*\*\*\* and \*\*\*\* `Pipfile.lock` files
* Poetry projects with `pyproject.toml` \*\*\*\* and `Poetry.lock` files

#### Usage examples

`snyk fix --file=requirements.txt`

`snyk fix --file=base.txt --package-manager=pip`

`snyk fix --all-projects`

#### Requirements with `-r` directives

Where the `requirements.txt` looks like this, both `base.txt` and `requirements.txt` are updated if needed:

```
-r base.txt # this means grab all the dependencies from here
django===1.6.1
```

**Direct dependency upgrades (dependencies stated in the manifest)**

Direct dependency upgrades are applied in the relevant files. All files referenced are found and updated.

**Pins (transitive dependencies that are pulled in via direct dependencies)**

Pins are applied in the manifest file that was tested.

If multiple files are tested but are related (for example one requires the other), Snyk starts to apply changes to the files higher up in the directory structure.

Snyk detects previously fixed files and skips applying fixes to them again.

#### Projects which use `constraints.txt`

Constraints files are requirements files that control only which version of a dependency is installed, not whether it is installed or not. Their syntax and contents are nearly identical to requirements files. There is one key difference: including a package in a constraints file does not trigger installation of the package. For more information, see [User Guide - pip documentation v21.0.1](https://pip.pypa.io/en/stable/user\_guide/#constraints-files).

**Direct dependency upgrades (dependencies stated in the manifest)**

Direct dependency upgrades are applied in the relevant files. All files referenced are found and updated.

**Pins (transitive dependencies that are pulled in via direct dependencies)**

All transitive dependencies are pinned in the `constraints.txt` file if referenced with the `-c` directive in the requirements manifest file.

#### Python (`pipenv`)

Snyk delegates to `pipenv` directly to update dependencies to the specified recommended versions. All `pipenv` environment variables and behaviors are preserved as much as possible.

#### Python (`poetry`)

Snyk delegates to `poetry` directly to update dependencies to the specified recommended versions. All `poetry` environment variables and behaviors are preserved as much as possible.

### Troubleshooting

Run in debug mode to get more information on any errors.

```
DEBUG=*snyk* snyk fix
```

This provides a very verbose output that can help diagnose issues or can be sent to Snyk for debugging.
