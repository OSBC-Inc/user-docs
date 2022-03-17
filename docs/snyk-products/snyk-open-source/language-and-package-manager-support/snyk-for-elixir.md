# Elixir용 Snyk

Snyk CLI를 이용하여 [Elixir](https://www.notion.so/Elixir-7c925900bf774c84b83b65c14084e80e) 프로젝트의 취약점을 테스트하기 위한 보안 스캔을 제공합니다.

## 특징

| Package managers / Features                                  | CLI support | Git support | License scanning | Fixing | Runtime monitoring |   |
| ------------------------------------------------------------ | ----------- | ----------- | ---------------- | ------ | ------------------ | - |
| [Mix](https://hexdocs.pm/mix/Mix.html)/[Hex](https://hex.pm) | ✔︎          |             |                  |        |                    |   |

## 작동 방식

Snyk은 매니페스트 및 lockfile을 분석하여 프로젝트에 대한 디펜던시 트리를 구축합니다.

트리를 구축한 후에는 [vulnerability database](https://snyk.io/vuln)를 사용하여 디펜던시 트리의 모든 패키지에서 취약점을 찾을 수 있습니다.

## Elixir 프로젝트에서 Snyk CLI 사용하기

### Mix/Hex

{% hint style="info" %}
디펜던시를 스캔하려면 먼저 Elixir와 Mix를 설치하세요 자세한 내용은 [해당 문서](https://elixir-lang.org/install.html)를 참조하십시오.
{% endhint %}

Mix는 Elixir 프로젝트를 생성, 컴파일 및 테스트하고 디펜던시를 관리하는 등의 작업을 제공하는 빌드 도구입니다.

Mix는 Hex 패키지 매니저와 통합하여 디펜던시를 관리합니다.

디펜던시 트리를 작성하기 위해 Snyk은 `mix.ex` 및 `mix.lock` 파일을 분석합니다. `mix.lock` 파일이 있어야 하며 `mix.exs` 파일과 동기화되어야 합니다.

**프로젝트 이름 지정**

Snyk UI의 프로젝트 이름은 Mix에서 내보낸 `Project/0` 함수의 `app` 키워드에 따라 지정됩니다. `mix.exs` 파일에 존재합니다.

프로젝트 이름을 재정의하려면 `--project-name` CLI 파라미터를 사용하십시오.

**Umbrella projects**

Mix Umbrella 프로젝트를 테스트하는 경우 Snyk는 이 프로젝트가 상위 프로젝트임을 감지하고 모든 하위 app을 자동으로 포함합니다.

메인 `mix.ex`와 함께 각 앱 `mix.ex`는 Snyk UI에서 별도의 프로젝트로 나타나며 app의 경로에 따라 이름이 지정됩니다.

**디펜던시 유형**

Snyk은 모든 전이적 디펜던시 및 취약점을 포함하여 Mix 프로젝트에 나열된 모든 `:hex` 패키지를 완벽하게 지원합니다.

Hex support includes both Elixir and ErlaHex 지원은 Elixir와 Erlang 패키지 모두를 포함합니다.

Snyk은 `:path`, `:git` 및 `:github` 디펜던시를 제한적으로 지원하지만 이들의 전이적 디펜던시나 취약점은 지원하지 않는다.

* `:path` 디펜던시는 이름으로 디펜던시 트리에 나타납니다.
* `:git` 및 `:github` 디펜던시가 리포지토리 URL 및 버전별로 디펜던시 트리에 표시됩니다(`mix.exs` 파일에 정의된 대로 `:branch`, `:tag` 또는 `:ref`).
