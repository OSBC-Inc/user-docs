# Snyk CLI 빌드의 향상된 장애

Snyk CLI는 빌드 실패 시 다음 옵션을 제공합니다.

```
--severity-threshold=low|medium|high
```

제공된 수준 이상의 취약점만 보고합니다.

```
--fail-on=all|upgradable|patchable
```

수정할 수 있는 취약점이 있는 경우에만 실패합니다.

```
--fail-on=all
```

업그레이드하거나 패치할 수 있는 취약점이 하나 이상 있으면 실패합니다.

```
--fail-on=upgradable
```

업그레이드할 수 있는 취약점이 하나 이상 있으면 실패합니다.

```
--fail-on=patchable
```

패치할 수 있는 취약점이 하나 이상 있으면 실패합니다. 취약점에 수정 사항이 없고 이 옵션을 사용 중인 경우 테스트를 통과합니다.

Snyk CLI 자체에는 기본적으로 더 복잡한 사용 사례에 대한 테스트를 실패할 수 있는 기능이 없습니다. 다음은 보다 복잡한 합격/불합격 기준을 달성하는 몇 가지 방법입니다.

## --severity-threshold 와 보안 정책 결합

[보안 정책](../../fixing-and-prioritizing-issues/policies/)은 해당 정책을 사용하는 조직에 대해 프로젝트를 테스트할 때 심각도가 특정 기준에 일치하는 경우 취약점의 심각도를 변경할 수 있는 기능을 제공합니다. 예를 들어 다음과 같은 CLI를 사용하여 `synk test` 를 실행하는 경우 취약점의 심각도를 높음에서 낮음으로 변경할 수 있습니다.

```
 --severity-threshold=medium|high
```

이전에 심각도가 높았던 이 취약점은 더 이상 빌드에 실패하지 않습니다.

{% hint style="info" %}
보안 정책에는 기준 일치에 사용할 수 있는 일부 속성이 없습니다. 시간이 지남에 따라 에 추가될 때 사용할 수 있는 항목을 보려면 보안 정책 구성을 참조하십시오.
{% endhint %}

다음은 정책이 적용되지 않은 기본 조직에 대해 실행되는 `--severity-threshold=high` 를 사용한 `snyk test` 의 예입니다.

![정책이 적용되지 않은 기본 조직에 대 테스트](https://camo.githubusercontent.com/de965fce454134d8cadaaf22fe093c4fdf1722a7349e99f1d2d8bc4cf9726836/68747470733a2f2f67626c6f627363646e2e676974626f6f6b2e636f6d2f6173736574732532462d4d56584b6472682d6a59334b44475073386c512532462d4d5a545f57334f316f46794d417a46396733732532462d4d5a5472633044364e6a5436566c53316a6d55253246696d6167652e706e673f616c743d6d6564696126746f6b656e3d32376530656538632d313437662d343934322d616461342d303864653037663637633430)

다음은 이 특정 취약점 심각도를 낮은 수준으로 다운그레이드하는 정책을 가진 조직에 대해 실행되는 `--severity-threshold=high` 를 사용한 `snyk test` 의 예입니다. 취약점이 없습니다.

![정책이 적용된 조직에 대 테스트](https://github.com/snyk/user-docs/raw/5e52535b78618f57eda40eb08fc8fbf91e16f1f0/docs/.gitbook/assets/test-organization-with-policy-applied.png)

### 지원 도구

다음은 Snyk CLI를 위한 snyk-delta 또는 snyk-filter 오픈 소스 지원 도구 사용에 대해 설명합니다.

snyk-delt는 현재 테스트와 이전에 모니터링한 스냅샷 사이의 취약점 델타를 찾습니다.

snyk-messages는 npmjs.org에서 사용할 수 있으며 다음을 사용하여 CI/CD 파이프라인으로 가져올 수 있습니다.

```
npm install -g snyk-delta
```

synk-filter는 `synk test` 를 JSON 형식으로 출력한 사용 가능한 데이터를 기반으로 사용자 정의 통과/실패 기준을 제공합니다.

snyk-filter는 npmjs.org에서 사용할 수 있으며 npm 설치를 사용하여 CI/CD 파이프라인으로 가져올 수 있습니다.

```
npm install -g snyk-filter
```

#### 새 취약점이 도입된 경우에만 현재 빌드에 실패합니다.

**Inline mode**

```
snyk test --json --print-deps | snyk-delta
```

Org + 프로젝트 좌표를 지정하여 특정 스냅샷을 가리킬 수 있습니다.

```
snyk test --json --print-deps | snyk-delta --baselineOrg xxx --baselineProject xxx
```

**Standalone**

```
snyk-delta --baselineOrg xxx --baselineProject xxx --currentOrg xxx --currentProject xxx
```

자세한 내용은 [GitHub의 synk-delta 프로젝트](https://github.com/snyk-tech-services/snyk-delta)를 참조하십시오.

#### CVSS 점수가 다음보다 높은 경우 빌드 실패...

```
snyk test --json | snyk-filter -f /path/to/example-cvss-9-or-above.yml
```

#### 사용자 정의 기준 및 필터링

synk-filter는 `synk test` 를 JSON 형식으로 출력하여 사용 가능한 모든 기준의 조합을 사용할 수 있습니다.

빌드에 실패하는 것과 표시 기준이 다를 수도 있습니다. 이렇게 하면 일부 특정 기준에서만 실패하면서 테스트 출력에 모든 취약점을 표시하는 등의 작업을 수행할 수 있습니다.

예제와 자세한 내용은 [GitHub의 synk-filter 프로젝트](https://github.com/snyk-tech-services/snyk-filter)를 참조하십시오.
