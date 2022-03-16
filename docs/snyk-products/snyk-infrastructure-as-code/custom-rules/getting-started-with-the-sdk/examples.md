# Custom Rule 예시

### Boolean Rule 예제

{% hint style="info" %}
이 문서의 전체 예제는 [OPA Playground](https://play.openpolicyagent.org/p/SCYndBjWxh) 및 [snyk/custom-rules-example](https://github.com/snyk/custom-rules-example) 저장소에서 확인할 수 있습니다.
{% endhint %}

SDK(`snyk-iac-rules template --rule CUSTOM-RULE-1`)를 사용하여 새로운 Rule `CUSTOM-RULE-1`을 생성했으며 Terraform 리소스가 들어 있는 매우 간단한 fixture 파일이 있다고 가정합니다.

{% code title="rules/CUSTOM-RULE-1/fixtures/denied.tf" %}
```
resource "aws_redshift_cluster" "denied" {
  cluster_identifier = "tf-redshift-cluster"
  node_type          = "dc1.large"
  tags = {
  }
}
```
{% endcode %}

이제 생성된 Rego를 수정하여 소유자가 태그된 리소스를 적용하려고 합니다.

1. 모든 `AWS_redsshift_cluster` 리소스에서 열거할 변수 `[name]`을 생성합니다. 이 변수는 원하는 모든 변수(`i`, `j`, `name` 등)로 이름을 지정할 수 있습니다.
2. 대입 표현식(바다코끼리 연산자) `:=;` 을 사용하여 리소스 변수에 값을 할당하여 이 값을 저장합니다.(`resource := input.resource.aws_sshift_cluster[name]`)
3. 각 리소스에 대해 소유자 태그가 있는지 확인합니다. 그렇게 하려면 `resource.tags.owner` 경로가 정의되어 있는지 확인합니다. 정의되지 않은 경우 정의되지 않은 것으로 평가됩니다. 앞에 `NOT` 키워드를 사용하면 `TRUE`로 평가됩니다(예: `resource.tags.owner`).

수정한 Rego는 다음과 같습니다.

{% code title="rules/CUSTOM-RULE-1/main.rego" %}
```
package rules

deny[msg] {
    resource := input.resource.aws_redshift_cluster[name]
    not resource.tags.owner

    msg := {
        "publicId": "CUSTOM-RULE-1",
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

{% hint style="info" %}
Rego 코드가 이전에 제공된 Terraform 파일을 평가하는 방법을 이해하려면 SDK가 [fixture 파일을 JSON으로 파싱하는 방법](parsing-an-input-file.md)을 확인하십시오.
{% endhint %}

{% hint style="warning" %}
[유닛 테스트를 업데이트하고 실행](testing-a-rule.md)하여 Rule이 올바른지 확인하는 것이 좋습니다.
{% endhint %}

Rule에 대한 테스트에서는 Rego Rule이 본 가이드의 시작 부분에 있는 설비가 유효하지 않음을 식별할 수 있는지 확인합니다.

{% code title="rules/CUSTOM-RULE-1/main_test.rego" %}
```
package rules

import data.lib
import data.lib.testing

test_CUSTOM_RULE_1 {
	# array containing test cases where the rule is allowed
	allowed_test_cases := [{
		"want_msgs": [],
		"fixture": "allowed.tf",
	}]

	# array containing cases where the rule is denied
	denied_test_cases := [{
		"want_msgs": ["input.resource.aws_redshift_cluster[denied].tags"],
		"fixture": "denied.tf",
	}]

	test_cases := array.concat(allowed_test_cases, denied_test_cases)
	testing.evaluate_test_cases("CUSTOM-RULE-1", "./rules/CUSTOM-RULE-1/fixtures", test_cases)
}
```
{% endcode %}

### Logical AND 예제

위의 예제를 확장하여 두 가지 조건을 만족하는 모든 경우를 허용하도록 Rule을 업데이트해 보겠습니다.

1. 리소스에 "owner" 태그가 존재, **AND**
2. 리소스에 "description" 태그가 존재

새로운 조건을 테스트하기 위해 `template` 명령어을 사용하여 새로운 Rule `CUSTOM-RULAY-2`를 생성하고 다음 fixture 파일을 작성합니다.

{% code title="rules/CUSTOM-RULE-2/fixtures/denied.tf" %}
```
resource "aws_redshift_cluster" "denied" {
  cluster_identifier = "tf-redshift-cluster"
  node_type          = "dc1.large"
  tags = {
    owner = "team-123"
  }
}
```
{% endcode %}

여러 식을 함께 결합하면 Logical `AND`가 표현됩니다.

* 이 작업은 `;`연산자를 사용하여 수행할 수 있습니다.
* 또는 식을 여러 줄로 분할하여 `;` (`AND`) 연산자를 생략할 수 있습니다.

{% hint style="info" %}
Logical AND는 [OPA 설명서](https://www.openpolicyagent.org/docs/latest/#expressions-logical-and)에서도 다룹니다.
{% endhint %}

{% code title="rules/CUSTOM-RULE-2/main.rego" %}
```
package rules

aws_redshift_cluster_tags_present(resource) {
    resource.tags.owner
    resource.tags.description
}

deny[msg] {
    resource := input.resource.aws_redshift_cluster[name]
    not aws_redshift_cluster_tags_present(resource)
    msg := {
        "publicId": "CUSTOM-RULE-2",
        "title": "Missing a description and an owner from the tag",
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

{% hint style="warning" %}
[유닛 테스트를 업데이트하고 실행](testing-a-rule.md)하여 Rule이 올바른지 확인하는 것이 좋습니다.
{% endhint %}

Rule에 대한 테스트는 `CUSTOM-RULE-1`의 테스트와 동일하게 표시되지만 테스트 이름과 `testing.evaluate_test_cases` 함수에 전달된 처음 두 파라미터가 다릅니다.

{% code title="rules/CUSTOM-RULE-2/main_test.rego" %}
```
package rules

import data.lib
import data.lib.testing

test_CUSTOM_RULE_2 {
	# array containing test cases where the rule is allowed
	allowed_test_cases := [{
		"want_msgs": [],
		"fixture": "allowed.tf",
	}]
	# array containing cases where the rule is denied
	denied_test_cases := [{
		"want_msgs": ["input.resource.aws_redshift_cluster[denied].tags"],
		"fixture": "denied.tf",
	}]
	test_cases := array.concat(allowed_test_cases, denied_test_cases)
	testing.evaluate_test_cases("CUSTOM-RULE-2", "./rules/CUSTOM-RULE-2/fixtures", test_cases)
}
```
{% endcode %}

### Logical OR 예제

`NOT` 연산자와 `OR` 기능을 결합하여 위의 Rule을 다시 작성할 수 있습니다.

새로운 Rule CUSTOM-RULE-3의 예제를 업데이트하여 두 조건 중 하나에 실패한 경우를 모두 **거부**하겠습니다. 다음 중 하나가 누락된 모든 aws\_redshift\_cluster 리소스를 거부합니다.

1. “owner” 태그 , **OR**
2. “description” 태그

이를 위해 case별로 하나씩 두 개의 새로운 fixture 파일을 사용합니다.

{% code title="rules/CUSTOM-RULE-3/fixtures/denied1.tf" %}
```
resource "aws_redshift_cluster" "denied1" {
  cluster_identifier = "tf-redshift-cluster"
  node_type          = "dc1.large"
  tags = {
    owner = "team-123@corp-domain.com"
  }
}
```
{% endcode %}

{% code title="rules/CUSTOM-RULE-3/fixtures/denied2.tg" %}
```
resource "aws_redshift_cluster" "denied2" {
  cluster_identifier = "tf-redshift-cluster"
  node_type          = "dc1.large"
  tags = {
    description = "description",
  }
}
```
{% endcode %}

Logical OR을 Rego로 표현하기 위해, 우리는 동일한 이름의 여러 Rule이나 함수를 정의할 수 있습니다. 이 내용은 Logical OR에 대한 [OPA 설명서](https://www.openpolicyagent.org/docs/latest/#logical-or)에도 설명되어 있습니다.

우선 태그별로 `NOT`을 구현하는 기능을 추가하겠습니다. 그런 다음 리소스를 사용하여 이 함수를 호출합니다.

{% code title="rules/CUSTOM-RULE-3/main.rego" %}
```
package rules

aws_redshift_cluster_tags_missing(resource) {
    not resource.tags.owner
}

aws_redshift_cluster_tags_missing(resource) {
    not resource.tags.description
}

deny[msg] {
    resource := input.resource.aws_redshift_cluster[name]
    aws_redshift_cluster_tags_missing(resource)
    msg := {
        "publicId": "CUSTOM-RULE-3",
        "title": "Missing a description or an owner from the tag",
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

이렇게 하면 거부하는 모든 Rule이 성공적으로 반환됩니다.

{% hint style="warning" %}
[유닛 테스트를 업데이트하고 실행](testing-a-rule.md)하여 Rule이 올바른지 확인하는 것이 좋습니다.
{% endhint %}

이제 이 Rule에 대한 테스트에는 여러 테스트 사례가 포함되어 Logical OR이 예상대로 작동하는지 확인할 수 있습니다.

{% code title="rules/CUSTOM-RULE-3/main_test.rego" %}
```
package rules

import data.lib
import data.lib.testing

test_CUSTOM_RULE_3 {
	# array containing test cases where the rule is allowed
	allowed_test_cases := [{
		"want_msgs": [],
		"fixture": "allowed.tf",
	}]
	# array containing cases where the rule is denied
	denied_test_cases := [{
		"want_msgs": ["input.resource.aws_redshift_cluster[denied1].tags"],
		"fixture": "denied1.tf",
	},{
		"want_msgs": ["input.resource.aws_redshift_cluster[denied2].tags"],
		"fixture": "denied2.tf",
	}]
	test_cases := array.concat(allowed_test_cases, denied_test_cases)
	testing.evaluate_test_cases("CUSTOM-RULE-3", "./rules/CUSTOM-RULE-3/fixtures", test_cases)
}
```
{% endcode %}

### Strings 예제

추가 확장하여 세 번째 조건을 추가할 수 있습니다. 모든 리소스를 거부할 수 있습니다.

1. “owner” 태그 , **OR**
2. “description” 태그, **OR**
3. 소유자의 이메일이 "@nota-domain.com" 도메인에 속하지 않는 경우

{% code title="rules/CUSTOM-RULE-4/main.rego" %}
```
package rules

aws_redshift_cluster_tags_missing(resource) {
    not resource.tags.owner
}

aws_redshift_cluster_tags_missing(resource) {
    not resource.tags.description
}

aws_redshift_cluster_tags_missing(resource) {
    not endswith(resource.tags.owner, "@corp-domain.com")
}

deny[msg] {
    resource := input.resource.aws_redshift_cluster[name]
    aws_redshift_cluster_tags_missing(resource)
    msg := {
        "publicId": "CUSTOM-RULE-4",
        "title": "Missing a description and an owner from tag, or owner tag does not comply with email requirements",
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

{% hint style="warning" %}
[유닛 테스트를 업데이트하고 실행](testing-a-rule.md)하여 Rule이 올바른지 확인하는 것이 좋습니다.
{% endhint %}

이 Rule에 대한 테스트는 이전의 테스트와 매우 유사하며 자체 설비 파일도 필요합니다.

### XOR 예제

다음과 같이 진행하겠습니다.

* 태그 유형이 "user"인 경우 "email" 태그도 함께 사용하길 원합니다.
* 그렇지 않은 경우(다른 유형이 "service"라고 가정), 서비스설명(ServiceDescription)으로 지정합니다.
* 이 두 가지는 상호 배타적일 것입니다. 첫 번째 조건이 적용되면 두 번째 조건이 적용되면 안 되고, 두 번째 조건이 적용되면 두 번째 조건이 적용되면 안 되고, 그 반대도 마찬가지입니다.

| Type    | Email | ServiceDescription |
| ------- | ----- | ------------------ |
| User    | YES   | NO                 |
| Service | NO    | YES                |

이를 위해 checkTags 도우미 기능을 사용하도록 코드를 리팩터링하겠습니다. 이렇게 하면 태그가 있는지 확인할 수 있을 뿐만 아니라 위의 두 가지 조건을 OR로 확인할 수도 있습니다.

{% code title="rules/CUSTOM-RULE-5/main.rego" %}
```
package rules

checkTags(resource){
    resource.tags.type == "user"
    not resource.tags.email
}

checkTags(resource){
    resource.tags.type == "service"
    not resource.tags.serviceDescription
}

checkTags(resource){
    count(resource.tags) == 0
}

deny[msg] {
    resource := input.resource.aws_redshift_cluster[name]
    checkTags(resource)   

    msg := {
        "publicId": "CUSTOM-RULE-5",
        "title": "Complex rule",
        "severity": "medium",
        "msg": sprintf("input.resource.aws_redshift_cluster[%v].tags", [name]),
        "issue": "",
        "impact": "",
        "remediation": "",
        "references": [],
    }
}
```
{% endcode %}

이를 XOR로 변환하려면 `else` Rule을 사용할 수 있습니다.

{% code title="rules/CUSTOM-RULE-5/main.rego" %}
```
package rules

checkUserTag(resource){
    not resource.tags.email
}

checkUserTag(resource){
    resource.tags.serviceDescription
}

checkServiceTag(resource){
    not resource.tags.serviceDescription
}

checkServiceTag(resource){
    resource.tags.email
}

checkTags(resource){
	count(resource.tags) == 0
}

checkTags(resource) {
    resource.tags.type == "user"
    checkUserTag(resource)
} else {
    resource.tags.type == "service"
    checkServiceTag(resource)
}

deny[msg] {
    resource := input.resource.aws_redshift_cluster[name]
	checkTags(resource)
    msg := {
        "publicId": "CUSTOM-RULE-5",
        "title": "Missing the right tags from for a resource of type user or service",
        "severity": "medium",
        "msg": sprintf("input.resource.aws_redshift_cluster[%v].tags", [name]),
        "issue": "",
        "impact": "",
        "remediation": "",
        "references": [],
    }
}
```
{% endcode %}

직접 체험해 보고 싶다면 [OPA Playground](https://play.openpolicyagent.org/p/1xcdj9kJRw)에서 동일한 예시를 제공합니다.

{% hint style="warning" %}
[유닛 테스트를 업데이트하고 실행](testing-a-rule.md)하여 Rule이 올바른지 확인하는 것이 좋습니다.
{% endhint %}

이 Rule에 대한 테스트는 이전 예의 테스트와 매우 유사하며 fixture 파일도 필요합니다.

### 그룹화된 리소스 예시

리소스 배열에 추가함으로써 많은 리소스를 반복할 수 있습니다.

```
"resources": [
            "aws_iam_policy",
            "aws_iam_group_policy",
            "aws_iam_user_policy",
            "aws_iam_role_policy",
            "data.aws_iam_policy_document",
]
```

이것을 활용하는 한 가지 방법은 denylist rules를 구현하는 것입니다.

예를 들어, 누군가가 Kubernetes ConfigMap을 정의한 경우 암호, 비밀 키 및 액세스 토큰과 같은 중요한 정보를 저장하는 데 사용할 수 없도록 할 수 있습니다.

이를 통해 denylist 내에서 중요한 토큰 그룹을 정의함으로써 시간이 지남에 따라 "민감한 정보"로 정의한 내용을 확장할 수 있습니다.

```
package rules

sensitive_denylist := [
	"pass",
	"secret",
	"key",
	"token",
]

check_sensitive(keys, denylist) {
	_ = keys[key]
	contains(key, denylist[_])
}

deny[msg] {
	input.kind == "ConfigMap"
	input.data = keys
	check_sensitive(keys, sensitive_denylist)
	msg := {
		"publicId": "CUSTOM-RULE-7",
		"title": "ConfigMap exposes sensitive data",
		"severity": "high",
		"msg": "input.data",
		"issue": "",
		"impact": "",
		"remediation": "",
		"references": [],
	}
}
```

"pass", "secret", "key" 및 "token"이 포함된 키는 중요한 것으로 간주될 수 있으므로 ConfigMap에 포함해서는 안 됩니다.

##
