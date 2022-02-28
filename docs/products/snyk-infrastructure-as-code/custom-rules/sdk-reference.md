# SDK Reference

### 이름

`snyk-iac-rules` - Snyk IaC에 대한 Custom rules를 작성, 디버그, 테스트 및 bundle

### 개요

`snyk-iac-rules` \[COMMAND] \[PATH] \[OPTIONS]

### 설명

SDK는 Rego로 작성한 Custom rules를 작성, 디버그, 테스트 bundle 및 배포를 지원하며, 이 Rule을 Snyk IaC CLI에서 사용하여 IaC 구성 파일에 취약점을 찾을 수 있습니다.

Snyk에 대한 자세한 내용은 [https://snyk.io](https://snyk.io)을 참조하세요.

#### 시작 방법

1. 새로운 Rule 작성 `$ snyk-iac-rules template`
2. Rego 작성, fixture를 JSON을 파싱 `$ snyk-iac-rules parse`
3. Rule 테스트h `$ snyk-iac-rules test`
4. Rule을 Bundle로 구성 `$ snyk-iac-rules build`
5. Rule 배포 `$ snyk-iac-rules push`

### 명령어

명령어별 플래그 및 사용법, `help` 명령어를 참조하세요.(예: `snyk-iac-rules --help`)

Available top-level SDK commands:사용가능한 최상위 SDK 명령어는 다음과 같습니다.

`template` - 새로운 Rule을 작성하기위한 스캐폴딩을 생성합니다. `snyk-iac-rules template --help`를 참조하세요.

`parse` - 제공한 fixture 파일의 JSON 형식으로 반환합니다. Rego에는 JSON 입력이 필요하여 이를 사용하여 Rego Rule을 만드세요. `snyk-iac-rules parse --help`를 참조하세요.

`test` - 일치하는 파일에서 검색된 모든 테스트 사례를 실행합니다. `snyk-iac-rules test --help`를 참조하세요.

`build` - OPA 정책 및 데이터 파일을 bundle로 패키징합니다. `snyk-iac-rules build --help`를 참조하세요.

`push` - `build` 명령어로 생성된 bundle을 지원하는 컨테이너 레지스트리 중 하나로 지정합니다. `snyk-iac-rules push --help`를 참조하세요.

### 경로

SDK의 모든 명령어은 Rule의 위치를 지정하는 폴더에 대한 선택적 경로를 사용할 수 있습니다. `parse` 및 `push` 명령어은 이 경로가 엄격하게 필요한 유일한 명령입니다.

절대 경로 또는 상대 경로를 제공할 수 있습니다.

### 옵션

명령어별 플래그 및 사용법, `help` 명령어를 참조하세요.(예:6`snyk-iac-rules template --help`)

#### 템플릿 옵션

`--rule`=RULE

정의할 Rule의 필수 이름입니다. Rule 이름을 딴 폴더와 Rego Rule 및 Rego 테스트 파일을 포함하는 `rules/` 폴더가 최상위 수준에서 생성됩니다. 동시에 Rule을 작성하고 테스트 라이브러리를 확장하기 위한 `data.lib` 또는 테스트에 대한 `data.lib.testing`에서 액세스할 수 있는 유틸리티 함수를 포함하는 `lib/` 폴더를 생성합니다.

스캐폴딩 폴더 구조는 다음과 같습니다.

`rules`\
`└── RULE`\
`├── fixtures`\
`├── allowed.<extension>`\
`└── denied.<extension>`\
`├── main.rego`\
`└── main_test.rego`\
`lib`\
`└── testing`\
`└── main.rego`\
`└── tfplan.rego`\
`└── main.rego`

Note: Rule 이름은 공백을 포함하거나 `SNYK-`으로 시작할 수 없습니다.

`--format`=`hcl2`|`json`|`yaml`|`tf-plan`

Rule을 정의할 필수 구성 형식입니다. `rules/<RULE>/fixtures` 폴더에 두 개의 fixture 파일이 생성되며, 이 파일은 테스트에 의해 Rego Rule의 동작을 확인하는데 사용됩니다.

`--severity`=`low`|`medium`|`high`|`critical`

Snyk Infrastructure as Code CLI를 실행할 때 표시되는 Rule의 심각도입니다.

기본값: `low`

`--title`=`TITLE`

Snyk Infrastructure as Code CLI를 실행할 때 표시되는 Rule의 제목입니다.

#### Parse options

`--format`=`hcl2`|`yaml|tf-plan`

The forfixture의 형식입니다. 이 형식은 fixture에서 JSON을 생성하는데 사용하는 파서를 지정합니다.

기본값: `hcl2`

#### Test options

`--verbose`

tracing 로그를 출력합니다.

`--explain`=`full`|`notes`|`fails`

tracing 로그를 필터링합니다.

기본값: `fails`

`--timeout`=TIMEOUT

테스트가 실행되기를 기다리는 시간(nanoseconds)입니다. TIMEOUT보다 오래걸리면 테스트가 실패합니다.

기본값: 5000000 (5 seconds).

`--ignore`

테스트를 위해 로드되는 파일 및 폴더를 무시하는 데 사용할 수 있는 정규식을 허용합니다.

기본값: ".\*" (hidden files), "fixtures"

`--run`

테스트의 하위 집합을 실행할 때 사용할 수 있는 정규식을 허용합니다.

#### Build options

`--output`

결과 bundle의 이름과 위치를 제공합니다.

기본값: bundle.tar.gz

`--entrypoint`

기본적으로 템플릿 명령은 규칙에 대한 Rego를 `./rules/<rule>` 폴더 아래에 배치합니다. Rego는 rules 패키지에 속하며 항목 함수를 거부하며, 잘못된 구성이 발견되면 취약점을 나타내는 JSON을 반환합니다. 이 구조는 `rules/deny` 진입점과 함께 작동하지만 생성된 파일 및 패키지 구조를 수정해야 하는 경우 사용자 지정 진입점을 제공할 수 있습니다.

기본값: "rules/deny"

`--ignore`

bundling을 위해 로드되는 파일 및 폴더를 무시할 때 사용할 수 있는 정규식을 허용합니다.

기본값: ".\*”"(hidden files), "fixtures", "testing", "\*\_test.rego"

`--target`=`rego`|`wasm`

bundle에 사용할 형식입니다. 지금은 Snyk IaC CLI에서 Rego 번들을 지원하지 않습니다.

기본값: `wasm`

#### 모든 명령어에서 사용 가능한 플래그

\[COMMAND] `--help`, `--help` \[COMMAND], `-h`

도움말 텍스트를 출력합니다. 자세한 내용을 확인하려면 COMMAND를 지정할 수 있습니다.

#### Push 옵션

`--registry`

bundle을 push할 레지스트리 위치입니다(예: `docker.io/`, `/bundle.tar.gz`)

#### Flags available across all commands

\[COMMAND] `--help`, `--help` \[COMMAND], `-h`

도움말 텍스트를 출력합니다. 자세한 내용을 확인하려면 COMMAND를 지정할 수 있습니다.

### 예시

이름으로 새로운 Rule 생성 `CUSTOM_RULE`

```
$ snyk-iac-rules template --rule CUSTOMRULE
```

Rule 테스트

```
$ snyk-iac-rules test --run CUSTOM_RULE
```

Custom rules bundle 생성

```
$ snyk-iac-rules build --output bundle-v1.0.0.tar.gz
```

### EXIT CODES

사용 가능한 exit codes는 다음과 같습니다.

**0**: 성공

**1**: 실패, Custom rules가 잘못되었을 수 있습니다.
