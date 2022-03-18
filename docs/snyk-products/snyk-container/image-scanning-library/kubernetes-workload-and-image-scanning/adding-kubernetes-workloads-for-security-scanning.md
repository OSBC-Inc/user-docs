# 보안 스캔을 위한 Kubernetes 워크로드 추가

Snyk 계정 관리자가 Kubernetes 클러스터에 Snyk 컨트롤러를 설치했으면 다음과 같이 테스트할 워크로드를 추가합니다.

* Snyk 공동작업자는 수동으로 새 Kubernetes 프로젝트를 추가할 수 있습니다.
* Kubernetes 공동작업자는 클러스터에서 워크로드를 표시하여 Snyk에 자동으로 추가할 수 있습니다.

## 전제 조건

Snyk에 계정이 있어야 하며 관리자(administrator)가 귀사에 등록해야 합니다.

또한 조직별로 Snyk와 귀사의 Kubernetes 환경 간에 통합을 구성해야 합니다. 통합이 구성되어 있는지 확인하려면 Integration ID가 있어야 합니다.

1. 관련 조직으로 이동합니다.
2. settings ![](../../../../.gitbook/assets/cog\_icon.png) > **Integrations**를 클릭합니다.
3. Kubernetes 섹션에서 **Edit Settings**를 클릭합니다.
4. **Integration ID**항목으로 스크롤하여 설정되었는지 확인합니다.

## 워크로드 자동 추가, 업데이트 및 제거

Snyk과 클러스터 간의 통합을 구성한 후에는 워크로드에 주석을 달아 Snyk에서 테스트하기 위한 프로젝트로 워크로드를 자동으로 추가할 수 있습니다.

{% hint style="info" %}
주석이 달린 가져오기는 **이미지** 자체가 변경되거나(이미지 변경으로 인해 작업량이 증가) **워크로드 세부정보**가 변경되어(워크로드의 새 수정본이 작성됨) 워크로드가 변경될 때 발생합니다. 워크로드에 대한 주석을 변경해도 워크로드는 변경되지 않습니다.

워크로드가 `snyk monitor`로 스캔된 후에만 주석을 달면, 전체 재검색을 유발하는 중요한 변경이 발생할 때까지 주석이 인식되지 않습니다. `snyk monitor` 포드를 종료하는 것은 재검색을 강제하는 한 가지 방법입니다.
{% endhint %}

다음 워크로드 타입에서 주석을 추가할 수 있습니다.

* Deployments
* ReplicaSets
* DaemonSets
* StatefulSets
* Jobs
* CronJobs
* ReplicationControllers
* Pods

**진행 단계**

1. 계정에 로그인하고 관리하려는 관련 그룹 및 조직으로 이동합니다.
2. settings ![](../../../../.gitbook/assets/cog\_icon.png) > **General**를 클릭합니다.
3. **Organization ID** 값을 복사합니다.
4. `orgs.k8s.snyk.io/v1` 키를 사용하여 워크로드에 주석을 추가합니다. 이 키는 쉼표로 구분된 목록에 조직 ID를 값으로 입력합니다.

단일 워크로드에 주석을 추가하여 여러 조직에 추가할 수도 있습니다.

1.  Snyk 컨트롤러는 워크로드의 변경 사항을 자동으로 인식하여 워크로드를 Snyk 프로젝트로 자동으로 가져옵니다.

    Example 1입니다. 자동으로 조직에 가져오기 위해 주석이 달린 배포 YAML 파일의 예입니다.

    ```
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: my-app-deployment
      annotations:
        orgs.k8s.snyk.io/v1: cacb791e-07cc-4b10-b4be-64de19f532f1
    spec:
      template:
        spec:
          containers:
          …
    ```

    여러 조직에 주석을 달려면 쉼표로 목록을 구분하여 사용하세요.
2. 가져온 프로젝트는 주석을 제거하더라도 Snyk 조직에 남아 있습니다. Snyk에서 프로젝트를 제거하려면 주석을 삭제하고 Snyk UI 또는 [API](https://snyk.docs.apiary.io/#reference/projects/individual-project/delete-a-project)에서 삭제해야 합니다.

## 워크로드 수동 추가

**Projects page**로 이동하여 **Add project**를 클릭하고 **Kubernetes**옵션을 선택합니다.

![](../../../../.gitbook/assets/uuid-619a153d-6c77-f7dc-854c-ff77b3173191-en.png)

가져오기 화면이 아래 화면과 유사하게 로드되어 왼쪽에는 Kubernetes 환경의 모든 네임스페이스가 표시되고 오른쪽에는 관련 네임스페이스 워크로드가 표시됩니다.

![](../../../../.gitbook/assets/uuid-3a8568e0-b5a4-34af-d612-83466b206882-en.png)

우리는 Kubernetes 내부의 특정 네임스페이스(\_**kube-\***\_로 시작하는 모든 네임스페이스) 검색을 의도적으로 무시하므로, 해당 네임스페이스는 물론 해당 네임스페이스가 포함하는 워크로드도 목록에 표시되지 않습니다.\
무시된 네임스페이스의 전체 목록은 [여기](https://github.com/snyk/kubernetes-monitor/blob/master/src/supervisor/watchers/internal-namespaces.ts)에서 찾을 수 있습니다. 이는 snyk-monitor를 설정할 때 helm에 다음을 추가하여 구성할 수 있습니다.

```
      --set excludedNamespaces={kube-node-lease,local-path-storage,some_namespace}
```

* 왼쪽에서 네임스페이스를 하나 이상 선택하고 각 네임스페이스에 대해 오른쪽에서 가져올 워크로드를 하나 이상 선택합니다.

![Select\_namespace.gif](../../../../.gitbook/assets/uuid-27db0a60-f18d-5ab0-9215-5a81e467f013-en.gif)

* 준비가 되었으면 화면 오른쪽 상단에서 **Add selected workloads**를 클릭합니다. 가져오기가 완료되면 프로젝트 페이지가 로드되고 가져온 모든 워크로드가 고유한 Kubernetes 아이콘과 함께 표시됩니다.

![Kubernetes icon](../../../../.gitbook/assets/uuid-24e0b69a-01c3-9434-9dac-9b44864bd269-en.png)

각 항목의 이름은 Kubernetes 메타데이터에 따라 다음과 같이 지정됩니다.**\<namespace>/\<kind>/\<name>**.

Kubernetes 프로젝트에 대해서만 필터링할 수 있습니다.

![](<../../../../.gitbook/assets/image (5).png>)
