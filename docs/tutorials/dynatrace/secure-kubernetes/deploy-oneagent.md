# OneAgent 배포

{% embed url="https://youtu.be/K2PVsCivTMU" %}

{% hint style="info" %}
빠르게 시작할 수 있도록 단계별 지침을 제공합니다. 자세한 제품 설명서는 다음 Dynatrace 설명서 페이지를 참조하십시오.\
1\. [Kubernetes에서 Dynatrace 설정](https://www.dynatrace.com/support/help/setup-and-configuration/setup-on-container-platforms/kubernetes/)\
2\. [Dynatrace ActiveGate](https://www.dynatrace.com/support/help/setup-and-configuration/dynatrace-activegate/)\
3\. [Dynatrace OneAgent](https://www.dynatrace.com/support/help/setup-and-configuration/dynatrace-oneagent/)
{% endhint %}

## Step 1:

Dynatrace 환경에서 **Infrastructure**로 이동한 다음 아래와 같이 왼쪽 탐색 메뉴에서 **Kubernetes**로 이동합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/dynatrace-k8s-config-01.png)

**Add Custer** 선택합니다.

## Step 2:

아래와 같이 연결 이름을 제공합니다:

{% hint style="info" %}
이 이름은 배포를 단순화하고 Kubernetes 클러스터 이름, Network Zone, ActiveGate Group 및 Host Group을 비롯한 다양한 Dynatrace 설정에서 사용됩니다. 개별적으로 고유한 설정의 경우 [Kubernetes 모니터링 문서](https://dt-url.net/a32h0p41)의 활성화 지침을 따르십시오.
{% endhint %}

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/dynatrace-k8s-config-02.png)

그런 다음 **Create tokens**를 클릭합니다.

{% hint style="warning" %}
이 메뉴를 **떠나지 마십시오**. 몇 가지 항목을 복사하여 붙여넣고 터미널로 전환했다가 나머지 단계를 수행해야 합니다. 이 메뉴에서 벗어나 탐색하는 경우 새 토큰을 생성하고 프로세스를 중단해야 합니다.
{% endhint %}

## Step 3:

터미널에서 네임스페이스를 만들고 [Dynatrace Operator](https://github.com/dynatrace/dynatrace-operator)를 K8s 클러스터에 배포합니다.

```bash
kubectl create namespace dynatrace
kubectl apply -f https://github.com/Dynatrace/dynatrace-operator/releases/latest/download/kubernetes.yaml
```

그런 다음 **Step 2**의 **PaaS Token** **및** **API Token**을 복사하여 다음 명령에 붙여넣습니다.

```bash
kubectl -n dynatrace create secret generic dynakube --from-literal="apiToken=DYNATRACE_API_TOKEN" --from-literal="paasToken=PLATFORM_AS_A_SERVICE_TOKEN"
```

## Step 4:

Dynatrace 환경 Dashboard로 돌아가서 아래 표시된 명령을 복사합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/dynatrace-k8s-config-03.png)

복사가 완료되면 터미널로 다시 전환하고 예제 명령을 실행합니다.

```bash
 wget https://github.com/dynatrace/dynatrace-operator/releases/latest/download/install.sh \
 -O install.sh && sh ./install.sh --api-url "$YOUR_API_URL" \
 --api-token "$YOUR_API_TOKEN" \
 --paas-token "$YOUR_PASS_TOKEN" \
 --cluster-name "$YOUR_CLUSTER_NAME"
```

**$YOUR\_API\_URL**이 Dynatrace 테넌트의 URL인 경우 **$YOUR\_API\_TOKEN**, **$YOUR\_PASS\_TOKEN** 및 **$YOUR\_CLUSTER\_NAME**은 위에서 생성된 것입니다. 성공하면 아래와 유사한 결과가 표시됩니다:

```
Check for token scopes...

Check if cluster already exists...

Creating Dynatrace namespace...

Applying Dynatrace Operator...
customresourcedefinition.apiextensions.k8s.io/dynakubes.dynatrace.com configured
serviceaccount/dynatrace-dynakube-oneagent unchanged
serviceaccount/dynatrace-dynakube-oneagent-unprivileged unchanged
serviceaccount/dynatrace-kubernetes-monitoring unchanged
serviceaccount/dynatrace-operator unchanged
serviceaccount/dynatrace-routing unchanged
role.rbac.authorization.k8s.io/dynatrace-operator unchanged
clusterrole.rbac.authorization.k8s.io/dynatrace-kubernetes-monitoring unchanged
clusterrole.rbac.authorization.k8s.io/dynatrace-operator unchanged
rolebinding.rbac.authorization.k8s.io/dynatrace-operator unchanged
clusterrolebinding.rbac.authorization.k8s.io/dynatrace-kubernetes-monitoring unchanged
clusterrolebinding.rbac.authorization.k8s.io/dynatrace-operator unchanged
deployment.apps/dynatrace-operator unchanged
Warning: kubectl apply should be used on resource created by either kubectl create --save-config or kubectl apply
secret/dynakube configured

Applying DynaKube CustomResource...
dynakube.dynatrace.com/dynakube created

Adding cluster to Dynatrace...
Kubernetes monitoring successfully setup.
```

다 됐습니다! 다음 섹션으로 이동할 준비가 되었습니다.
