# 자동으로 가져오기/삭제 고급사용

Kubernetes 워크로드 프로젝트의 자동으로 가져오기/삭제에 대한 고급 사용 사례가 있는 경우 규칙을 작성할 수 있습니다. 컨트롤러는 [Rego policy language](https://www.openpolicyagent.org/docs/latest/policy-language/)로 작성된 정책 파일을 사용하여 정책 결정을 평가합니다. 파일이름이 **workload-events.rego**인지 확인합니다.

## 정책 구문

ConfigMap의 Snyk 컨트롤러에 정책 파일을 제공합니다. 정책 구문은 다음과 같습니다.

```
package snyk
orgs := ["<org-id>"]
default workload_events = false
```

값을 true로 바꾸면 클러스터의 **모든 항목**을 자동으로 가져오거나 삭제합니다.

{% hint style="warning" %}
Jobs 및 Pods와 같은 일부 워크로드 유형은 Snyk 조직에서 많은 워크로드 가져오기를 생성할 수 있으므로 workload\_events 키를 true로 설정하는 것은 **권장하지 않습니다**.
{% endhint %}

**package snyk**과 주요 **workload\_events**는 모두 Snyk 컨트롤러에서 필수입니다.

## 둘 이상의 조직 사용

Orgs는 조직 공개 ID목록입니다. 자동으로 가져오기/삭제 기능을 사용하기 위해 둘 이상의 조직을 추가할 수 있습니다. 조직의 설정 페이지에서 이 공개 ID를 찾을 수 있습니다.

```
package snyk
orgs := ["<org-id-1>","<org-id-2>"]
default workload_events = false
```

## Rule 정의

고유한 Rule을 정의하려면 **workload\_events** 키에 대한 조건을 설정하고 조직의 공개 ID를 제공하세요. 예를 들어 **기본** 네임스페이스에서 워크로드를 가져오고 클러스터에서 삭제되면 Snyk 측에서 자동으로 삭제하는 정책은 다음과 같습니다.

```
package snyk
orgs := ["19982df2-0ed5-4a16-b355-e6535cfc41ef"]
default workload_events = false
workload_events {
    input.metadata.namespace == "default"
}
```

여기서 **input**은 Snyk 컨트롤러에서 스캔한 워크로드의 Kubernetes 메타데이터를 나타냅니다.

특정 주석을 사용하여 워크로드 이벤트(생성/삭제)에 대한 정책을 생성할 수 있습니다.

```
package snyk
orgs := ["19982df2-0ed5-4a16-b355-e6535cfc41ef"]
default workload_events = false
workload_events {
    input.metadata.annotations.team == "apollo"
}
```

## 워크로드 유형 제외

Pods와 Jobs와 같은 특정 워크로드 유형을 워크로드 이벤트(생성/삭제)에서 제외하는 것이 좋습니다. 이러한 유형은 실제로 Snyk 조직에서 많은 워크로드 가져오기를 생성할 수 있기 때문입니다. 다음 예제를 사용하여 이 작업을 수행할 수 있습니다.

```
package snyk
orgs := ["19982df2-0ed5-4a16-b355-e6535cfc41ef"]
default workload_events = false
workload_events {
    input.kind != "Job"
    input.kind != "Pod"
}
```

## 정책을 사용하도록 Snyk 컨트롤러를 구성

```
kubectl create configmap snyk-monitor-custom-policies \
    -n snyk-monitor \
    --from-file=workload-events.rego # This name is hardcoded
helm upgrade --install snyk-monitor snyk-charts/snyk-monitor \
    --namespace snyk-monitor \
    --set clusterName="Production cluster" \
    --set workloadPoliciesMap=snyk-monitor-custom-policies
```

이제 Snyk 컨트롤러를 배포하거나 정책을 선택하기 위해 이미 실행 중인 경우 다시 시작할 수 있습니다. 이제 Snyk에서 새로운 워크로드를 확인할 수 있습니다.
