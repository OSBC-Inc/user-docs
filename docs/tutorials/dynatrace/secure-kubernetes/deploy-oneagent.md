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

Provide a name for your connection as shown below:

{% hint style="info" %}
This name simplifies deployment and is used by various Dynatrace settings including Kubernetes cluster name, Network Zone, ActiveGate Group, and Host Group. For individually unique settings follow activation instructions from [Kubernetes monitoring documentation](https://dt-url.net/a32h0p41).
{% endhint %}

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/dynatrace-k8s-config-02.png)

Then click on **Create tokens**.

{% hint style="warning" %}
**DO NOT** leave this menu. You will need to copy and paste a few things and switch to your terminal and back for the remaining steps. If you navigate away from this menu, you will need to create new tokens and break the process.
{% endhint %}

## Step 3:

From your terminal, create a namespace and deploy the [Dynatrace Operator](https://github.com/dynatrace/dynatrace-operator) into your K8s cluster.

```bash
kubectl create namespace dynatrace
kubectl apply -f https://github.com/Dynatrace/dynatrace-operator/releases/latest/download/kubernetes.yaml
```

Next, copy and paste the **PaaS Token** & **API Token** from **Step 2** into the following command:

```bash
kubectl -n dynatrace create secret generic dynakube --from-literal="apiToken=DYNATRACE_API_TOKEN" --from-literal="paasToken=PLATFORM_AS_A_SERVICE_TOKEN"
```

## Step 4:

Go back to your Dynatrace environment Dashboard and copy the command shown below.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/dynatrace-k8s-config-03.png)

Once copied, switch back to your terminal and execute the example command:

```bash
 wget https://github.com/dynatrace/dynatrace-operator/releases/latest/download/install.sh \
 -O install.sh && sh ./install.sh --api-url "$YOUR_API_URL" \
 --api-token "$YOUR_API_TOKEN" \
 --paas-token "$YOUR_PASS_TOKEN" \
 --cluster-name "$YOUR_CLUSTER_NAME"
```

Where **$YOUR\_API\_URL** is that of your Dynatrace tenant, **$YOUR\_API\_TOKEN**, **$YOUR\_PASS\_TOKEN** and **$YOUR\_CLUSTER\_NAME** are those created above. If successful, you will see results similar to what is shown below:

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

That's it! You are ready to move to the next section.
