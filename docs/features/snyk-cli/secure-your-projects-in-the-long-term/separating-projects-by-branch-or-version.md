# 분기 또는 버전별로 프로젝트 분리

{% hint style="info" %}
이 기능은 현재 오픈 베타 버전입니다. 완전히 지원되지 않는 영역이 있습니다. 현재 [Snyk Open Source](https://github.com/snyk/user-docs/blob/5e52535b78618f57eda40eb08fc8fbf91e16f1f0/docs/products/snyk-open-source)가 지원됩니다.
{% endhint %}

프로젝트에는 분기, 릴리스 또는 배포와 같이 개별적으로 모니터링하려는 여러 상태가 있을 수 있습니다. `--target-reference` 옵션을 사용하여 프로젝트를 이러한 특정 그룹으로 분리할 수 있습니다.

`--target-reference`는 모든 텍스트를 사용하므로 명령과 결합하여 자동으로 값을 설정할 수 있습니다.\
다음은 예입니다:

`--target-reference`를 현재 Git 브랜치로 설정합니다.

```
snyk monitor --target-reference="$(git branch --show-current)"
```

최신 Git 태그를 사용해야합니다.

```
snyk monitor --target-reference="$(git describe --tags --abbrev=0)"
```

프로젝트에서 사용되는 개발자 도구에 대한 옵션을 조정할 수 있습니다. 모든 유효한 Git 대상을 사용할 수 있습니다.

`--target-reference` 를 사용하면 프로젝트 페이지에서 하위 그룹을 만들 수 있습니다.

![하위 그룹이 있는 프로젝트 페이지.](https://github.com/snyk/user-docs/raw/5e52535b78618f57eda40eb08fc8fbf91e16f1f0/docs/.gitbook/assets/Screenshot%202021-10-21%20at%2013-08-58%20Projects.png)
