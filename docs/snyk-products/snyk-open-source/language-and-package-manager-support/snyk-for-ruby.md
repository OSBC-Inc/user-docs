# Snyk for Ruby

Snyk는 [Bundler](https://bundler.io)에서 관리하는 디펜던시를 갖는 CLI와 Git 통합에서 루비 프로젝트를 테스트, 모니터링 및 수정하고 특정 디펜던시 버전을 [Ruby vulnerability database](https://snyk.io/vuln?type=rubygems)와 비교하는 것을 지원합니다.

Snyk는 모든 Bundler 그룹을 테스트하며 현재 특정 그룹(예: 테스트 또는 개발 그룹)을 제외할 수 없습니다.

Gemfile이 개인 Gem 소스에 액세스해야 하는 경우 [see below](snyk-for-ruby.md)를 참조하십시오.

매니페스트 파일은 다음 파일들을 지원합니다.

* `Gemfile`
* `Gemfile.lock`

{% hint style="info" %}
**Note**\
Snyk은 Ruby 프로젝트를 올바르게 테스트, 모니터링 및 수정하기 위해 두 파일이 모두 존재해야 합니다.
{% endhint %}

## Ruby 프로젝트의 취약점 수정

Snyk는 Gemfile을 수정한 후 번들 업데이트를 사용하여 취약한 Gem을 업데이트하여 취약점을 수정할 수 있습니다(가능한 한 지정한 규칙을 준수).

즉, 일부 시나리오에서는 모든 디펜던시를 취약하지 않은 버전으로 업그레이드할 수 없습니다. 이 경우 Gemfile의 규칙을 업데이트하는 것을 고려해야 합니다.

향후 릴리스에서는 이를 쉽게 할 수 있도록 제안사항을 제공할 계획입니다.

## **Private Gem Sources**

Private Gem Source를 사용하는 경우 Snyk CLI를 통해 테스트할 때 정상적으로 작동해야 합니다.

[Git에서 가져온 프로젝트에 대한 Private Gem Source를 구성](../../../features/integrations/private-registry-integrations/private-gem-sources-for-ruby.md)하려면 추가 단계를 수행해야 합니다.
