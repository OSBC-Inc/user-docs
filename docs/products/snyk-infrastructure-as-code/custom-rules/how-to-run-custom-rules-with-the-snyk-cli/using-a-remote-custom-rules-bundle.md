# 원격 custom rules bundle 사용

custom rules bundle을 생성한 후 [Pushing a bundle](../getting-started-with-the-sdk/pushing-a-bundle.md) 단계에 따라 지원되는 OCI 레지스트리 중 하나로 배포할 수 있습니다.

custom rules bundle을 성공적으로 push한 후 다음 항목을 사용하여 적용할 수 있습니다.

* [Snyk Settings page](using-a-remote-custom-rules-bundle.md#snyk-settings-page)
* [Snyk API](using-a-remote-custom-rules-bundle.md#snyk-api)
* [Environment variables](using-a-remote-custom-rules-bundle.md#environment-variables)

마지막으로 위의 옵션 중 하나를 통해 custom rules를 적용했으면 OCI 레지스트리에서 pull 권한을 부여할 수 있도록 사용자 이름과 암호를 사용하여 Snyk CLI를 구성하십시오.

```
snyk config set oci-registry-username=<org registry username>
snyk config set oci-registry-password=<org registry password>
```

이렇게 하면 다음과 같은 Snyk 환경 변수가 설정됩니다.

* `SNYK_CFG_OCI_REGISTRY_USERNAME`
* `SNYK_CFG_OCI_REGISTRY_PASSWORD`

완료되면 정상적으로 Snyk IaC 스캔을 실행합니다. CLI는 백그라운드에서 구성된 컨테이너 레지스트리로 push한 bundle을 가져옵니다.

```
snyk iac test <file>
```

결과 구성 스캔 문제에는 기본 Snyk rules과 custom rules의 문제가 모두 포함됩니다. [Understanding the CLI Output](../../snyk-cli-for-infrastructure-as-code/understanding-configuration-scan-issues.md)을 참조하십시오.

{% hint style="warning" %}
bundle 경로를 정의하는 방법은 한 번에 하나만 정의해야 합니다. Snyk 설정 페이지 또는 Snyk API를 통해 custom rules 설정을 비활성화해야 합니다. 또는 `snyk config unset`을 사용하여 이전에 저장된 설정을 지웁니다.
{% endhint %}

### Snyk 설정 페이지

Snyk 설정 페이지를 사용하여custom rules 설정을 구성하는 것이 좋습니다. 이 방법을 사용하면 custom rules bundle의 URL 및 태그를 수정할 때마다 간편하게 업데이트할 수 있습니다.

{% hint style="info" %}
태그는 custom rules bundle을 버전화하는 데 유용합니다. 새 버전 태그를 설정하여 업데이트 bundle을 쉽게 구성할 수 있습니다.
{% endhint %}

이러한 원격 bundle은 조직 수준 및 그룹 수준 모두에서 구성할 수 있습니다. 그룹에 대한 원격 bundle을 구성하면 원격 bundle이 그룹의 모든 조직에 적용됩니다.

원격 bundle을 구성하려면 다음과 같이 진행합니다.

* Infrastructure as Code Settings에서 **Rules** 섹션을 찾습니다.

{% hint style="info" %}
조직 레벨에서 원격 custom rules bundle을 구성하는 작업은 Settings > Infrastructure as Code로 이동하여 수행할 수 있습니다.

마찬가지로, Settings > Infrastructure as Code로 이동하여 그룹 레벨에서 설정할 수 있습니다.
{% endhint %}

![](<../../../../.gitbook/assets/image (89).png>)

* **Enable rules** 토글을 사용하여 원격 bundle 구성을 사용하도록 설정합니다. 이렇게 하면 아래와 같이 양식이 표시됩니다.

![](<../../../../.gitbook/assets/image (91).png>)

* custom rules의 원격 bundle에 대한 OCI 레지스트리 URL 및 태그를 구성하고 **Save changes**를 클릭하여 저장합니다.

![](<../../../../.gitbook/assets/image (87) (1).png>)

custom rules의 원격 bundle이 구성되었으며 IaC 파일을 테스트할 때 사용됩니다.

#### 그룹의 원격 bundle 구성 재정의

기본적으로 그룹에 대한 원격 bundle을 구성하면 원격 bundle이 그룹의 모든 조직에 적용됩니다. 따라서 그룹 구성이 업데이트되면 이러한 변경 사항이 모든 해당 조직에 적용됩니다.

그러나 조직은 여전히 그룹의 구성을 재정의하고 고유한 bundle과 태그를 정의할 수 있습니다. 이러한 설정은 그룹이 구성을 업데이트할 때 변경되지 않습니다.

그룹의 구성을 재정의하려면 Infrastructure as Code Settings에서 조직의 `Rules`섹션으로 이동하십시오.

* 처음에 섹션은 조직의 그룹에서 상속된 구성으로 채워집니다.

![](<../../../../.gitbook/assets/image (79).png>)

* 구성을 조직에 맞게 업데이트하고 **Save changes**를 클릭합니다.

![](<../../../../.gitbook/assets/image (83) (1) (1).png>)

* 이제 그룹 수준의 구성이 조직에 대해 이러한 사용자 지정 설정을 재정의하지 않습니다.

**Reset to group default** 버튼을 사용하여 언제든지 그룹 구성의 상속을 복원할 수 있습니다.

### Snyk API

Snyk 설정 페이지를 통해 수동으로 설정을 업데이트하는 데 시간이 많이 걸리는 경우 Snyk API를 사용할 수도 있습니다. 현재 API 호출을 통해 custom rules 설정의 변형을 전송할 수 있습니다.

* 예를 들어 **그룹** 수준에서 custom rules bundle을 구성하려면 다음 본문을 제공하여 [Group IaC Settings API](https://snykv3.docs.apiary.io/#reference) endpoint를 호출합니다.

```
{
   "data": {
         "type": "iac_settings",
         "attributes": {
           "custom_rules": {
             "oci_registry_url": "registry-1.docker.io/group-account/group-bundle-image",
             "oci_registry_tag": "1.3.14",
             "is_enabled": true
           }
       }
   }
}
```

* 태그만 업데이트하려는 경우 더 간단한 본문을 전송할 수 있습니다.

```
{
   "data": {
         "type": "iac_settings",
         "attributes": {
           "custom_rules": {
             "oci_registry_tag": "1.3.14"
           }
       }
   }
}
```

* custom rules를 비활성화하려면`is_enabled`플래그를 전송하면 됩니다.

```
{
   "data": {
         "type": "iac_settings",
         "attributes": {
           "custom_rules": {
             "is_enabled": false
           }
       }
   }
}
```

API가 그룹 설정으로 회신하므로 사용자는 변경 사항을 확인할 수 있습니다.

```
{
  "type": "iac_settings",
  "id": "<group id>",
  "attributes": {
    "custom_rules": {
      "oci_registry_url": "registry-1.docker.io/group-account/group-bundle-image",
      "oci_registry_tag": "1.3.14",
      "is_enabled": true
    },
   "updated": "2021-11-27T11:34:33.132Z"
  }
```

#### 그룹의 원격 bundle 구성 재정의

설정 페이지와 유사하게 [Group IaC Settings API](https://snykv3.docs.apiary.io/#reference) \*\*\*\*는 원격 bundle을 그룹의 모든 조직에 적용합니다. 조직은 API 호출을 사용하여 그룹의 구성을 재정의하고 고유한 bundle 및 태그를 정의할 수 있습니다.

* 그룹의 구성을 재정의하려면 요청 본문에 다른 custom rules bundle 및 태그를 제공하여 [**Org IaC Settings API**](https://snykv3.docs.apiary.io/#reference) endpoint를 호출하십시오.

```
{
   "data": {
         "type": "iac_settings",
         "attributes": {
           "custom_rules": {
             "oci_registry_url": "registry-1.docker.io/org-account/org-bundle-imageage",
             "oci_registry_tag": "1.3.15",
             "is_enabled": true
           }
       }
   }
}
```

* API는 조직의 설정과 부모 섹션 아래의 그룹 설정에 응답하므로 다음 두 가지를 비교할 수 있습니다.

```
{
  "type": "iac_settings",
  "id": "<org id>",
  "attributes": {
    "custom_rules": {
      "oci_registry_url": "registry-1.docker.io/org-account/org-bundle-image",
      "oci_registry_tag": "1.3.15",
      "is_enabled": true
    },
   "updated": "2021-11-27T11:34:33.132Z",
   "parents": {
      "group": {
        "id": "<group id>",
        "type": "iac_settings",
        "attributes": {
          "custom_rules": {
            "oci_registry_url": "registry-1.docker.io/group-account/group-bundle-image",
            "oci_registry_tag": "1.3.14",
            "is_enabled": true
          },
          "updated": "2021-11-19T10:59:45.259Z"
        }
      }
    }
  }
```

* 그룹 설정으로 되돌리려면 다음 요청 본문을 제공하여 API를 호출하십시오.

```
{
   "data": {
         "type": "iac_settings",
         "attributes": {
           "custom_rules": {
             "inherit_from_parent": "group"
           }
       }
   }
}
```

* API는 조직의 설정과 부모 섹션 아래의 그룹 설정에 응답하므로 다음 두 가지를 비교할 수 있습니다.

```
{
  "type": "iac_settings",
  "id": "<org id>",
  "attributes": {
    "custom_rules": {
      "oci_registry_url": "registry-1.docker.io/group-account/group-bundle-image",
      "oci_registry_tag": "1.3.14",
      "is_enabled": true,
      "inherit_from_parent": "group"
    },
   "updated": "2021-11-19T10:59:45.259Z",
   "parents": {
      "group": {
        "id": "<group id>",
        "type": "iac_settings",
        "attributes": {
          "custom_rules": {
            "oci_registry_url": "registry-1.docker.io/group-account/group-bundle-image",
            "oci_registry_tag": "1.3.14",
            "is_enabled": true
          },
          "updated": "2021-11-19T10:59:45.259Z"
        }
      }
    }
  }
```

### 환경 변수

조직의 Snyk 구성을 사용하여 custom rules bundle의 위치를 구성할 수도 있습니다. 프로젝트의 폴더에서 다음 명령을 실행하여 Snyk IaC CLI를 사용하여 컨테이너 레지스트리를 구성합니다.

```
snyk config set oci-registry-url=registry-1.docker.io/org-account/org-bundle-image:1.3.14
```

`SNYK_CFG_OCI_REGISTRY_URL` 환경 변수를 설정합니다.

{% hint style="info" %}
OCI 레지스트리 URL이 Dockerhub와 같은 올바른 URL인지 확인하세요.

`registry-1.docker.io/org-account/org-bundle-image:1.3.14`

bundle 경로를 정의하는 방법은 한 번에 하나만 정의해야 하므로 Snyk 설정 페이지에서 이전에 정의된 URL을 지우거나 custom rules를 사용하지 않도록 설정해야 합니다.
{% endhint %}

### Troubleshooting

**-d** 플래그로 명령을 실행하여 디버그 로그를 사용하도록 설정합니다.

```
snyk iac test <file> -d
```

다음과 같은 문제가 발생할 수 있습니다.

* 잘못된 컨테이너 레지스트리 URL을 제공하는 경우: 도커 허브를 사용하는 경우 위의 참고 사항을 참조하십시오.

```
We were unable to download the custom bundle to the disk. 
Please ensure access to the remote Registry and validate you have provided all the right parameters.
```

* 잘못된 자격 증명을 제공하고 있습니다.

```
There was an authentication error. Incorrect credentials provided.
    We were unable to download the custom bundle to the disk.
    Please ensure access to the remote Registry and validate you have provided all the right parameters.
```

설명할 수 없는 차이점을 발견하셨다면 지원 티켓을 올려주세요.
