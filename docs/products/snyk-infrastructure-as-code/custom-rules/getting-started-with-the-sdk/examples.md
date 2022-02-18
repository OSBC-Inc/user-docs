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
Rego 코드가 이전에 제공된 Terraform 파일을 평가하는 방법을 이해하려면 SDK가 [fixture 파일을 JSON으로 파싱하는 방법](parsing-an-input-file.md)을 확인하세요.
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

1. “owner” 태그  , OR
2. A “description” tag

For this, we will use two new fixture files, one for each case:

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

To express logical OR in Rego, we can define multiple rules or functions with the same name. This is also described in the OPA documentation for[ Logical OR](https://www.openpolicyagent.org/docs/latest/#logical-or).

First, we will add a function that will implement the `NOT` for each tag. Then, we will call this function with the resource:

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

This will successfully return all the rules that deny.

{% hint style="warning" %}
We recommend always validating that your rule is correct by [updating and running the unit tests](./#test-a-custom-rule).
{% endhint %}

The test for this rule will now contain multiple test cases, to show that the logical OR works as expected:

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

### Example with strings

Let’s extend this further and add a third condition. Deny all resources that are missing either:

1. An “owner” tag , OR
2. A “description” tag, OR
3. The email of the owner does not belong to the “@corp-domain.com” domain

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
We recommend always validating that your rule is correct by [updating and running the unit tests](testing-a-rule.md).
{% endhint %}

The test for this rule will look very similar to the ones from previous example and will also require its own fixture file.

### Example with XOR

Now let’s say that we want to add more complexity and check the following:

* If the tag type is a “user”, then we want the tag “email” to exist as well.
* If not (assume the other type is a “service”), we want it to have a serviceDescription.
* These two will be mutually exclusive; if the first condition applies, the second one shouldn’t, and vice versa.

| Type    | Email | ServiceDescription |
| ------- | ----- | ------------------ |
| User    | YES   | NO                 |
| Service | NO    | YES                |

To do this, we are going to refactor our code to use a checkTags helper function. This can check if there are any tags, but also check for the two conditions above with an OR.

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

To convert this to an XOR we can use an `else` rule:

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

If you want to try it out yourselves, we have provided the same example in an [OPA Playground](https://play.openpolicyagent.org/p/1xcdj9kJRw).

{% hint style="warning" %}
We recommend always validating that your rule is correct by[ updating and running the unit tests](testing-a-rule.md).
{% endhint %}

The test for this rule will look very similar to the ones from previous example and will also require its own fixture file.

### Examples with grouped resources

We can also iterate over many resources by adding them to an array of resources.

```
"resources": [
            "aws_iam_policy",
            "aws_iam_group_policy",
            "aws_iam_user_policy",
            "aws_iam_role_policy",
            "data.aws_iam_policy_document",
]
```

One way to leverage this is to implement denylist rules.

For example, we may want to ensure that if someone defines a Kubernetes ConfigMap, then they cannot use it to store sensitive information such as passwords, secret keys, and access tokens.

We can do that and expand what we define as "sensitive information" over time by defining a group of sensitive tokens inside a denylist:

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

Any key containing the substrings "pass", "secret", "key", and "token" can be considered sensitive and so should not be included in the ConfigMap.

##
