# Helm으로 Snyk 컨트롤러 설치

Kubernetes 워크로드에 대한 취약점 세부 정보를 얻으려면 Snyk 관리자가 먼저 클러스터에 Snyk 컨트롤러를 설치해야 합니다. Snyk 컨트롤러는 [Helm Hub](https://hub.helm.sh/charts/snyk/snyk-monitor)에 게시됩니다.

이 섹션에서는 다음 항목을 다룹니다.

* 대부분의 Kubernetes 플랫폼을 위한 Snyk 통합
* Amazon Elastic Kubernetes Service (EKS) 클러스터와 함께 Amazon Elastic Container Registry (ECR)를 사용할 때 통합을 위한 추가 구성 단계

**전제 조건**

{% hint style="info" %}
**기능 사용 여부**\
이 기능은 모든 유료 플랜에서 사용할 수 있습니다. 자세한 내용은 [pricing plans](https://snyk.io/plans/)를 참조하십시오.
{% endhint %}

* Snyk 조직의 관리자 계정입니다.
* 클러스터에서 [emptyDir](https://kubernetes.io/docs/concepts/storage/volumes/#emptydir) 형식으로 최소 50GB의 스토리지를 사용할 수 있어야 합니다.
* kubernetes 클러스터는 HTTPS를 통해 Snyk outbound와 통신할 수 있어야 합니다.
* Amazon Elastic Kubernetes Service (EKS) 클러스터와 통합하도록 Snyk을 구성할 때 Amazon Elastic Container Registry (ECR)에서 호스팅되는 이미지를 스캔하려면 먼저 [AWS documentation](https://docs.aws.amazon.com/AmazonECR/latest/userguide/ECR\_on\_EKS.html)에 설명된 전제 조건을 따라야합니다.

**진행 단계**

1.  Kubernetes 환경에 액세스하고 다음 명령을 실행하여 Snyk Charts 저장소를 Helm에 추가합니다.

    ```
    helm repo add snyk-charts https://snyk.github.io/kubernetes-monitor
    ```
2.  저장소가 추가되면 Snyk 컨트롤러에 대한 고유한 네임스페이스를 생성합니다.

    ```
    kubectl create namespace snyk-monitor
    ```

    **Tip:** 컨트롤러 리소스를 보다 쉽게 분리하려면 고유한 네임스페이스를 사용하세요. 이는 일반적으로 Kubernetes 애플리케이션에 대한 모범 사례입니다. 네임스페이스는 snyk-monitor라고 하며 나중에 다른 리소스를 구성할 때 필요합니다.
3. 이제 Snyk 계정에 로그인하고 **Integrations**로 이동합니다.
4. **Kubernetes**를 검색하여 클릭하십시오.
5. 를**Connect** 을 클릭하고 **Integration ID**를 복사하세요. Snyk **Integration ID**는: `abcd1234-abcd-1234-abcd-1234abcd1234`형식과 유사한 UUID입니다. 다음 단계에서 Kuernetes 환경에서 사용할 수 있도록 저장하세요.
6.  Snyk monitor는 Snyk **Integration ID**를 사용하고 `Dockercfg`파일을 사용하여 실행합니다. 개인 레지스트리를 사용하지 않는경우 다음 명령어를 실행하여 이전 단계의 Snyk **Integration ID**가 포함된 `snyk-monitor`라는 Kubernetes 암호를 생성합니다.

    ```
    kubectl create secret generic snyk-monitor -n snyk-monitor \
            --from-literal=dockercfg.json={} \
            --from-literal=integrationId=abcd1234-abcd-1234-abcd-1234abcd1234
    ```

    **Note:** 통합이 작동하기 위해서는 secret을 `snyk-monitor`라고 불러야합니다.
7. 스캔해야 할 이미지가 개인 레지스트리에 있는 경우 Snyk Integration ID와 `dockercfg.json` 파일을 모두 사용하여 암호(snyk-monitor)를 생성하여 이러한 레지스트리에 액세스할 수 있는 자격 증명을 제공해야 합니다. 모니터가 개인 레지스트리에서 이미지를 조회할 수 있도록 하려면 `dockercfg.json` 파일이 필요합니다. 일반적으로 이증 정보는 `$HOME/.docker/config.json`에 있습니다. 이러한 인증 정보는 `dockerconfig.json`파일에도 추가해야 합니다.
   1.  `dockercfg.json`파일을 생성합니다. 인증정보를 저장하세요. 내용은 다음과 같습니다.

       ```
       {
         // If your cluster does not run on GKE or it runs on GKE and pulls images from other private registries, add the following:
         "auths": {
           "gcr.io": {
             "auth": "BASE64-ENCODED-AUTH-DETAILS"
           }
           // Add other registries as necessary
         },
         
         // If your cluster runs on GKE and you are using GCR, add the following:
         "credHelpers": {
           "us.gcr.io": "gcloud",
           "asia.gcr.io": "gcloud",
           "marketplace.gcr.io": "gcloud",
           "gcr.io": "gcloud",
           "eu.gcr.io": "gcloud",
           "staging-k8s.gcr.io": "gcloud"
         }
         
         // If your cluster runs on EKS and you are using ECR, add the following:
         {
           "credsStore": "ecr-login"
         }
         
         With Docker 1.13.0 or greater, you can configure Docker to use different credential helpers for different registries.
         To use this credential helper for a specific ECR registry, create a credHelpers section with the URI of your ECR registry:
         {
           "credHelpers": {
             "public.ecr.aws": "ecr-login",
       	"<aws_account_id>.dkr.ecr.<region>.amazonaws.com": "ecr-login"
           }
         }
       }
       ```

       2\. 추가한 파일로 암호를 생성합니다.

       ```
       kubectl create secret generic snyk-monitor \
               -n snyk-monitor --from-file=dockercfg.json \
               --from-literal=integrationId=abcd1234-abcd-1234-abcd-1234abcd1234
       ```
8.  레지스트리 자체가 서명된 인증서 또는 기타 추가 인증서를 사용하는 경우 Snyk monitor에서 인증서를 사용할 수 있도록 해야 합니다. 먼저 디렉토리에 `.crt`, `.cert`, 및/또는 `.key` 파일을 배치하고 ConfigMap을 작성합니다.

    ```
    kubectl create configmap snyk-monitor-certs \
            -n snyk-monitor --from-file=<path_to_certs_folder>
    ```
9.  안전하지 않은 레지스트리를 사용하거나 레지스트리가 정규화되지 않은 이미지를 사용하는 경우 `registries.conf` 파일을 제공할 수 있습니다.

    ```
    [[registry]]
    location = "internal-registry-for-example.net/bar"
    insecure = true
    ```

    형식 및 추가 예제에 대한 자세한 내용은 [documentation](https://github.com/containers/image/blob/master/docs/containers-registries.conf.5.md)을 참조하세요. 파일을 생성한 후에는 이 파일을 사용하여 다음 ConfigMap을 생성할 수 있습니다.

    ```
    kubectl create configmap snyk-monitor-registries-conf \
            -n snyk-monitor \
            --from-file=<path_to_registries_conf_file>
    ```
10. Snyk Helm Chart를 설치합니다.

    ```
    helm upgrade --install snyk-monitor snyk-charts/snyk-monitor \
                 --namespace snyk-monitor \
                 --set clusterName="Production cluster"
    ```

    자신의 Snyk 인스턴스를 실행하는 경우 컨트롤러를 설치할 때 API endpoint를 지정해야 합니다. 다음에서 Snyk 인스턴스의 전체 호스트 이름을 변경합니다.

    ```
    helm upgrade --install snyk-monitor snyk-charts/snyk-monitor \
                 --namespace snyk-monitor \
                 --set clusterName="Production cluster" \
                 --set integrationApi=https://<server>/kubernetes-upstream
    ```

    **Tip**: **Production cluster** 이름을 모니터링 중인 클러스터를 기반으로 하는 이름으로 바꾸세요. 이 레이블을 사용하여 나중에 Snyk에서 워크로드를 찾을 수 있습니다. 클러스터는 이름에 `/` 를 허용하지 않습니다. 클러스터 이름에 있는 임의의 `/`가 제거됩니다.\
    Also, to avoid naming the cluster on every update, you can use Helm's existing option fo또한 모든 업데이트에서 클러스터 이름을 지정하지 않으려면 **--reuse-values**에 대해 Helm의 기존 옵션을 사용할 수 있습니다. 즉, 업그레이드할 때 마지막 릴리스의 값을 재사용하고 명령줄에서 **--set** 및 -f를 통해 병합합니다. 만약 '**--reset-values**'가 지정된 경우에는 무시합니다.
11. Snyk에 대한 outbound 연결에 프록시를 사용하는 경우 해당 프록시를 사용하도록 통합을 구성해야 합니다 프록시 세트를 구성하려면 Helm Charts에 제공된 다음 값을 선택합니다.

    * `http_proxy`
    * `https_proxy`
    * `no_proxy`

    인스턴스는 다음과 같습니다.

    ```
    helm upgrade --install snyk-monitor snyk-charts/snyk-monitor \
                 --namespace snyk-monitor \
                 --set clusterName="Production cluster" \
                 --set https_proxy=http://192.168.99.100:8080
    ```

    통합은 `no_proxy`값의 와일드카드 또는 CIDR 주소 범위를 지원하지 않습니다. 정확하게 일치하는 항목만 지원합니다.
12. 로깅 상세도를 변경하려는 경우 다음과 같이 진행할 수 있습니다. 유효한 수준은 `INFO`, `WARN`,`ERROR`입니다. 기본 값은 `INFO`입니다.

    ```
    helm upgrade --install snyk-monitor snyk-charts/snyk-monitor \
                 --namespace snyk-monitor \
                 --set clusterName="Production cluster" \
                 --set log_level="WARN"
    ```
13. 기본적으로 컨트롤러는 [Pod Security Policy](https://kubernetes.io/docs/concepts/policy/pod-security-policy/)없이 실행됩니다. 그러나 설정을 전달하여 활성화할 수 있습니다.

    ```
    helm upgrade --install snyk-monitor snyk-charts/snyk-monitor \
                 --namespace snyk-monitor \
                 --set clusterName="Production cluster" \
                 --set psp.enabled=true
    ```

    이름을 지정하여 기본 포드 보안 정책을 재사용할 수 있습니다. 이름을 지정하지 않으면 새로운 정책이 자동으로 만들어집니다.

    ```
    helm upgrade --install snyk-monitor snyk-charts/snyk-monitor \
                 --namespace snyk-monitor \
                 --set clusterName="Production cluster" \
                 --set psp.enabled=true \
                 --set psp.name=something
    ```
14. 이미지를 일시적으로 꺼내기 위해 기본 emptyDIr 저장 매체 대신 **PersistentVolumeClaim** (PVC)를 사용하도록 Snyk 컨트롤러를 구성할 수 있습니다. PVC는 Snyk chart에서 제공하는 Helm 템플릿으로생성하거나 이미 프로비저닝된 PVC를 사용할 수있습니다.

    다음 플래그를 사용하여 PVC를 제어합니다.

    * pvc.enabled - Helm chart에 emptyDir 대신 PVC를 사용하도록 지시합니다.
    * pvc.create - PVC 생성 여부 - 처음 프로비저닝할 때 유용합니다.
    * pvc.storageClassName - PVC의 StrorageCloss를 제어합니다.
    * pvc.name - Kubernetes에서 사용할 PVC 이름입니다.

    예를 들어 설치 시 다음 명령어를 실행하여 PVC를 프로비저닝/생성할 수 있습니다.

    ```
    helm upgrade --install snyk-monitor snyk-charts/snyk-monitor \
                 --namespace snyk-monitor \
                 --set pvc.enabled=true \
                 --set pvc.create=true \
                 --set pvc.name="snyk-monitor-pvc"
    ```

    다음 업그레이드에서는 PVC가 이미 있으므로 "pvc.create" 플래그를 삭제할 수 있습니다.

    ```
    helm upgrade --install snyk-monitor snyk-charts/snyk-monitor \
                 --namespace snyk-monitor \
                 --set pvc.enabled=true \
                 --set pvc.name="snyk-monitor-pvc"
    ```
15. 기본적으로 \_**kube-\***\_로 시작하는 모든 네임스페이스는 [여기](https://github.com/snyk/kubernetes-monitor/blob/master/src/supervisor/watchers/internal-namespaces.ts)서 찾을 수 있으며, Kube-\*로 시작하는 모든 네임스페이스는 일부러 무시합니다. 이 설정을 변경하려면 제외된 네임스페이스를 구성할 수 있습니다.\
    제외된 네임스페이스 설정을 사용하여 제외할 사용자 고유의 네임스페이스 목록을 추가하면 기본 설정을 무시하고 사용자가 제공하는 네임스페이스 목록을 사용합니다.

    ```
    helm upgrade --install snyk-monitor snyk-charts/snyk-monitor \
                 --namespace snyk-monitor \
                 --set excludedNamespaces="{kube-node-lease,local-path-storage,some_namespace}"
    ```
16. 컨트롤러를 배포하기 위해 더 많은 리소스가 필요한 경우 `--set`플래그를 사용하여 요청 및 제한에 대한 Helm Charts 기본 값을 구성합니다.

    ```
    helm upgrade --install snyk-monitor snyk-charts/snyk-monitor \
                 --namespace snyk-monitor \
                 --set requests."ephemeral-storage"="50Gi"
                 --set limits."ephemeral-storage"="50Gi"
    ```

![](../../../../.gitbook/assets/uuid-26f9c2cd-2755-07d5-61a0-bdb0261d87ab-en.gif)
