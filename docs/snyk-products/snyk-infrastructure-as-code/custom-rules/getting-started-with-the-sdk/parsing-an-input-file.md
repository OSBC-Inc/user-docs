# 입력 파일 파싱

Rego 코드를 작성할 때 입력 파일의 내부 표현을 이해하는 것은 어려울 수 있습니다. [규칙 작성 방법](writing-a-rule.md)을 배울 때 알게 되겠지만 입력 값은 JSON과 유사한 객체이지만 입력 파일은 YAML, Terraform 또는 [Terraform Plan JSON Output](https://www.terraform.io/internals/json-format)일 수도 있습니다. 이러한 항목이 JSON으로 변환되는 방법을 쉽게 이해할 수 있도록 `parse` 명령을 제공했습니다.

입력 파일로 사용할 IaC 파일이 필요합니다. 이 입력 파일은 기본적으로 파일을 JSON으로 파싱하는 [규칙을 테스트](testing-a-rule.md)할 때도 사용할 수 있습니다.

### Terraform 파일 파싱

예를 들어, 다음 Terraform 파일을 사용합니다.

{% code title="example.tf" %}
```
resource "aws_redshift_cluster" "example" {
  cluster_identifier = "tf-redshift-cluster"
  database_name      = "mydb"
  master_username    = "foo"
  master_password    = "Mustbe8characters"
  node_type          = "dc1.large"
  cluster_type       = "single-node"
}
```
{% endcode %}

동등한 JSON 형식을 가져오려면 parse 명령을 실행합니다.

```
snyk-iac-rules parse example.tf --format hcl2
```

다음과 같이 규칙을 작성하기 위한 JSON이 출력됩니다.

```
{
	"resource": {
		"aws_redshift_cluster": {
			"example": {
				"cluster_identifier": "tf-redshift-cluster",
				"cluster_type": "single-node",
				"database_name": "mydb",
				"master_password": "Mustbe8characters",
				"master_username": "foo",
				"node_type": "dc1.large"
			}
		}
	}
}
```

Rego에서 `node_type` 필드에 액세스하는 것은 다음과 같습니다.

```
input.resource.aws_redshift_cluster.example.node_type
```

### YAML 파일 파싱

또 다른 예는 Kubernetes 리소스를 정의하는 YAML 파일입니다.

{% code title="example.yaml" %}
```
apiVersion: v1
kind: Pod
metadata:
  name: example
spec:
  containers:
    - name: example
      image: example:latest
      securityContext:
        privileged: true 
```
{% endcode %}

동등한 JSON 형식을 가져오려면 parse 명령어를 실행합니다.

```
snyk-iac-rules parse example.yaml --format=yaml
```

다음과 같이 규칙을 작성하기 위한 JSON이 출력됩니다.

```
{
	"apiVersion": "v1",
	"kind": "Pod",
	"metadata": {
		"name": "example"
	},
	"spec": {
		"containers": [
			{
				"image": "example:latest",
				"name": "example",
				"securityContext": {
					"privileged": true
				}
			}
		]
	}
}
```

Rego에서 `privileged` 필드에 액세스하는 것은 다음과 같습니다.

```
input.spec.containers[0].securityContext.privileged
```

### Terraform Plan JSON Output 파일 파싱

또 다른 예는 다음 Terraform Plan JSON output 파일로, `terraform show -json ./plan/example.json.tfplan` 명령에서 반환됩니다.

{% code title="example.json.tfplan" %}
```
{
  "format_version": "0.2",
  "terraform_version": "1.0.11",
  "planned_values": {
    "root_module": {
      "resources": [
        {
          "address": "aws_vpc.example",
          "mode": "managed",
          "type": "aws_vpc",
          "name": "example",
          "provider_name": "registry.terraform.io/hashicorp/aws",
          "schema_version": 1,
          "values": {
            "assign_generated_ipv6_cidr_block": false,
            "cidr_block": "10.0.0.0/16",
            "enable_dns_support": true,
            "instance_tenancy": "default",
            "tags": null
          },
          "sensitive_values": {
            "tags_all": {}
          }
        }
      ]
    }
  },
  "resource_changes": [
    {
      "address": "aws_vpc.example",
      "mode": "managed",
      "type": "aws_vpc",
      "name": "example",
      "provider_name": "registry.terraform.io/hashicorp/aws",
      "change": {
        "actions": [
          "create"
        ],
        "before": null,
        "after": {
          "assign_generated_ipv6_cidr_block": false,
          "cidr_block": "10.0.0.0/16",
          "enable_dns_support": true,
          "instance_tenancy": "default",
          "tags": null
        },
        "after_unknown": {
          "arn": true,
          "default_network_acl_id": true,
          "default_route_table_id": true,
          "default_security_group_id": true,
          "dhcp_options_id": true,
          "enable_classiclink": true,
          "enable_classiclink_dns_support": true,
          "enable_dns_hostnames": true,
          "id": true,
          "ipv6_association_id": true,
          "ipv6_cidr_block": true,
          "main_route_table_id": true,
          "owner_id": true,
          "tags_all": true
        },
        "before_sensitive": false,
        "after_sensitive": {
          "tags_all": {}
        }
      }
    }
  ],
  "configuration": {
    "provider_config": {
      "aws": {
        "name": "aws",
        "expressions": {
          "region": {
            "constant_value": "us-east-1"
          }
        }
      }
    },
    "root_module": {
      "resources": [
        {
          "address": "aws_vpc.example",
          "mode": "managed",
          "type": "aws_vpc",
          "name": "example",
          "provider_config_key": "aws",
          "expressions": {
            "cidr_block": {
              "constant_value": "10.0.0.0/16"
            }
          },
          "schema_version": 1
        }
      ]
    }
  }
}
```
{% endcode %}

동등한 JSON 형식을 가져오려면 parse 명령어를 실행합니다.

```
snyk-iac-rules parse example.json.tfplan --format=tf-plan
```

다음과 같이 규칙을 작성하기 위한 JSON이 출력됩니다.

```
{
	"data": {},
	"resource": {
		"aws_vpc": {
			"example": {
				"assign_generated_ipv6_cidr_block": false,
				"cidr_block": "10.0.0.0/16",
				"enable_dns_support": true,
				"instance_tenancy": "default",
				"tags": null
			}
		}
	}
}
```

Rego에서 `tags` 필드에 액세스하는 것은 다음과 같습니다.

```
input.resource.aws_vpc.example.tags
```
