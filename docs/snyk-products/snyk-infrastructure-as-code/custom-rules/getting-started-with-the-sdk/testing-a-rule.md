# Rule 테스트

[Rule 작성](writing-a-rule.md)에 표시된 대로 `template` 명령을 사용하여 Rule을 생성한 경우 SDK 및 생성된 Rule과 함께 제공되는 테스트 기능을 사용할 수 있습니다.

{% hint style="info" %}
원하는 대로 테스트 기능을 직접 작성하거나 SDK에서 생성된 기능을 수정할 수도 있습니다. 그러나 이 페이지의 지침은 적용되지 않습니다.
{% endhint %}

이전 튜토리얼을 기반으로 Rule을 작성했다고 가정하면 SDK의 템플릿 기능에 의해 생성된 `main_test.rego` 파일을 열고 `rules/my_rule/fixtures/` 폴더 내의 파일 이름으로 `fixture` 필드를 구성합니다. 템플릿 기능은 지원되는 형식당 하나의 파일을 작성하고 모든 파일에 대해 테스트를 실행하도록 구성했지만, 원하는 대로 fixture 파일을 제거할 수 있습니다.

`rules/my_rule/fixtures`에 따라 리소스를 저장할 fixture 파일을 작성하거나 수정합니다. 이러한 파일에는 모든 이름이 있을 수 있으므로 `denied.tf` 및 `allowed.tf`를 예로 들 수 있습니다.

{% hint style="warning" %}
파일은 어떤 이름이든 가질 수 있지만 파일 확장자에 세심한 주의를 기울여야 합니다. Terraform Plan JSON Output이 포함된 fixture 파일에 대한 테스트를 작성하려면 테스트 라이브러리가 일반 JSON과 Terraform Plan JSON Output을 구별할 수 있도록 파일 이름 확장자가 `.json.tfplan`인지 확인하십시오.
{% endhint %}

{% code title="rules/my_rule/fixtures/denied.tf" %}
```
resource "aws_redshift_cluster" "denied" {
  cluster_identifier = "tf-redshift-cluster"
  database_name      = "mydb"
  master_username    = "foo"
  master_password    = "Mustbe8characters"
  node_type          = "dc1.large"
  cluster_type       = "single-node"
}
```
{% endcode %}

{% code title="rules/my_rule/fixtures/allowed.tf" %}
```
resource "aws_redshift_cluster" "allowed" {
  cluster_identifier = "tf-redshift-cluster"
  database_name      = "mydb"
  master_username    = "foo"
  master_password    = "Mustbe8characters"
  node_type          = "dc1.large"
  cluster_type       = "single-node"
  tags {
    owner = "snyk"
  }
}
```
{% endcode %}

테스트 사례의 `want_msgs` 필드에 거부 규칙이 evaluate/return 할 것으로 예상되는 리소스의 msg 필드를 추가해야 합니다.`["input.resource.aws_redshift_cluster[denied].tags"]`.

{% hint style="info" %}
`want_msgs` 필드는 적절한 Rego 규칙에서 계산된 `msg` 필드에 해당하는 하드코딩된 값을 포함하는 배열이어야 합니다.
{% endhint %}

{% code title="rules/my_rule/main_test.rego" %}
```
package rules

import data.lib
import data.lib.testing

test_my_rule {
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
	testing.evaluate_test_cases("my_rule", "./rules/my_rule/fixtures", test_cases)
}
```
{% endcode %}

모든 테스트를 실행하려면 다음 명령어를 실행합니다.

```
 snyk-iac-rules test
```

테스트를 성공적으로 통과하면 `rules/` 폴더에 세 가지 다른 Rule이 있다고 가정하면 다음과 유사한 출력이 나타납니다.

```
PASS: 3/3
```

그러나 이들 중 하나라도 실패하면 다음과 유사한 출력이 나타납니다.

```
data.rules.test_my_rule: FAIL (1.12234ms)
FAIL: 2/3
```

`rules/` 폴더에 둘 이상의 Rule이 있는 경우 다음 명령어를 실행하여 특정 테스트를 대상으로 지정할 수 있습니다.

```
snyk-iac-rules test --run test_my_rule
```

그러면 다음과 같이 출력됩니다.

```
Executing Rego test cases...
data.rules.test_my_rule: FAIL (1.040468ms)
--------------------------------------------------------------------------------
FAIL: 1/1
```

자세한 내용이 필요한 경우 `--explain notes` 옵션을 추가합니다.

```
 snyk-iac-rules test --run test_my_rule --explain notes
```

옵션을 추가하면 실패한 테스트를 디버깅하기 위한 자세한 정보가 출력됩니다.

{% hint style="info" %}
현재 폴더에 생성된 Rule보다 더 많은 Rule이 있는 경우 `--ignore` 옵션을 사용하여 테스트와 무관한 폴더 및 파일 제외하십시오(`template` 명령어를 사용한 경우 `lib/` 및 `rules`는 제외하지 마십시오). 이렇게 하면 테스트 속도를 높이고 Rego가 비 Rego 파일을 평가하려고 하는 문제를 방지할 수 있습니다.
{% endhint %}
