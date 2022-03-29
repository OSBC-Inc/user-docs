# Rule 작성

### Rego의 Rules

Rule은 Rego로 작성합니다. Rego를 작성할 때 두 가지 작업을 수행합니다.

1. 정책 결정을 내리는 **Rule**을 작성하십시오. Rule은 조건부 할당입니다.
2. Rule을 **Policies**로 구성합니다. Policies은 계층적 이름을 가진 Rule 집합입니다.

정책 언어에 대해 자세히 확인하려면 [공식 OPA 정책 언어 문서 페이지](https://www.openpolicyagent.org/docs/latest/policy-language/)를 참조하십시오.

{% hint style="info" %}
[OPA Playground](https://play.openpolicyagent.org)를 사용하여 Rego를 사용해보거나 가이드의 예시를 실행할 수도 있습니다.
{% endhint %}

### 새로운 Rule을 생성하는 방법

시작할 수 있는 두 가지 옵션이 있습니다.

1.  다음 명령어를 이용하여 `template` Rule 작성에 필요한 파일을 생성합니다.

    ```
    snyk-iac-rules template --rule <RULE-NAME> --format <hcl2|json|yaml|tf-plan>
    ```

    이는 제공된 구성 형식을 기반으로 하는 fixture 파일을 포함하여 Rule에 대한 스캐폴딩을 생성합니다. 자세한 내용은 [template 명령에 대한 설명서](https://docs.snyk.io/products/snyk-infrastructure-as-code/custom-rules/sdk-reference#template-options)를 참조하십시오.
2. Rego 정책을 처음부터 만들고 예상 파일 및 폴더 구조를 직접 일치시킵니다.\
   `rules`\
   `└── my_rule`\
   `├── main.rego`\
   `└── main_test.rego`

{% hint style="info" %}
`template` 명령어를 사용하지 않으면 Rego 테스트 프레임워크를 직접 작성해야 합니다.
{% endhint %}

### Rule의 구조

Rego에서는 다음과 같이 요청을 허용하거나 거부하는 명령문을 작성할 수 있습니다.\
`allow { input.name == "alice" }` or `deny { input.name == "alice" }`

{% hint style="info" %}
**`template`** 명령어를 사용하여 Rule을 생성한 경우 기본 진입점은 **rules/deny**입니다. 이 Rule을 무시하고 다른 이름을 사용하려면 [Bundling Rules](bundling-rules.md)를 확인하십시오.
{% endhint %}

`snyk-iac-rules` 템플릿을 실행할 때 생성된 거부 규칙은 다음과 같습니다. `--rule new-rule --form hcl2`

{% code title="rules/new-rule/main.rego" %}
```
package rules

deny[msg] {
	resource := input.resource.test[name]
	resource.todo
	msg := {
		# Mandatory fields
		"publicId": "new-rule",
		"title": "Default title",
		"severity": "low",
		"msg": sprintf("input.resource.test[%s].todo", [name]),
		# Optional fields
		"issue": "",
		"impact": "",
		"remediation": "",
		"references": [],
	}
}
```
{% endcode %}

{% hint style="warning" %}
Snyk IaC CLI에 올바르게 표시되도록 하려면 다음 형식의 **msg** 속성을 따라야 합니다.
{% endhint %}

속성은 다음과 같습니다.

* **publicId:** COMPANY-001과 같이 사용자 고유의 이름 지정 규칙입니다. 내부 Snyk Rule과 구별하기 위해 **"SNYK-"으로 시작하거나 포함하지 못합니다.**
* **title:** Issue를 요약한 짧은 제목입니다.
* **severity:** **low/medium/high/critical** 중 하나일 수 있습니다.
* **msg:** `input.aws_s3_messages[%s].tags`와 같이 리소스 이름과 속성만 변경하는 것이 좋습니다. 기능 `sprintf`는 Rego에서 제공하며 Issue가 발견된 정확한 위치를 설명하는 동적 오류 메시지를 제공할 수 있습니다.

다음 특성은 선택 사항이지만 Snyk CLI에서 스캔 결과를 향상시키는 데 사용할 수 있습니다.

* **issue:** 정확한 Issue에 대한 자세한 설명입니다.
* **impact:** 이 Issue를 해결하지 않을 경우 미치는 영향에 대한 자세한 설명입니다.
* **remediation:** Issue 해결 방법에 대한 자세한 설명입니다. 여기에 snippet을 제공하는 것이 좋습니다.
* **references:** 문서에 대한 URL이 있는 문자열 배열을 제공할 수 있습니다 .

Rule에 대해 생성된 테스트에서는 생성된 2개의 Terraform 파일을 사용하여 허용 및 거부된 fixtures에 대한 Rule에 의해 올바른 `msg` 필드가 반환되는지 확인합니다.

```
package rules

import data.lib
import data.lib.testing

test_new_ruleryle {
	# array containing test cases where the rule is allowed
	allowed_test_cases := [{
		"want_msgs": [],
		"fixture": "allowed.tf",
	}]

	# array containing cases where the rule is denied
	denied_test_cases := [{
		"want_msgs": ["input.resource.test[denied].todo"], # verifies that the correct msg is returned by the denied rule
		"fixture": "denied.tf",
	}]

	test_cases := array.concat(allowed_test_cases, denied_test_cases)
	testing.evaluate_test_cases("new-rule", "./rules/new-rule/fixtures", test_cases)
}
```

### Rule의 예

{% hint style="info" %}
더 많은 예시는[ ](examples.md)[Custom Rule 예시](examples.md)를 참조하십시오.
{% endhint %}

이 예시에서는 리소스에 `owner` 태그가 없는 경우 `msg`를 할당하도록 템플릿 Rule을 수정했습니다.

{% code title="rules/my_rule/main.rego" %}
```
package rules

deny[msg] {
    resource := input.resource.aws_redshift_cluster[name]
    not resource.tags.owner
	
    msg := {
        "publicId": "my_rule",
        "title": "Missing an owner from tag",
        "severity": "medium",
        "msg": sprintf("input.resource.aws_redshift_cluster[%s].tags", [name]),
        "issue": "",
        "impact": "",
        "remediation": "",
        "references": [],
    }
}
```
{% endcode %}

### 제한 사항 / 참고 사항

* Rego 정책을 Wasm 모듈로 컴파일하면서 Wasm을 지원하는 내장 기능만 사용할 수 있습니다. [정책 참조 문서](https://www.openpolicyagent.org/docs/latest/policy-reference/)의 하단에 이러한 항목을 식별하는 데 도움이 되는 표가 있습니다.
* Rule은 파일 또는 동일한 패키지의 개별 파일에 동일한 이름으로 여러 번 정의할 수 있습니다.

```
packages rules

deny[msg] {
    resource.this
}
...

deny[msg] {
    resource.that
}
...
```

이러한 Rule은 각 정의가 추가되기 때문에 `incremental`이라고 합니다. Incremental 정의에 대한 자세한 내용은 [문서](https://www.openpolicyagent.org/docs/latest/policy-language/#incremental-definitions)를 참조하십시오. 동일하게 명명된 Rule이 다른 값을 반환해야 합니다. 그렇지 않으면 OPA가 오류를 반환합니다. 전체 정의에 대한 자세한 내용은 [문서](https://www.openpolicyagent.org/docs/latest/policy-language/#complete-definitions)를 참조하십시오.

보다 복잡한 항목을 확인하려면 [OPA가 Conflict Resolution을 해결하는 방법](https://www.openpolicyagent.org/docs/latest/faq/#conflict-resolution)을 참조하십시오.
