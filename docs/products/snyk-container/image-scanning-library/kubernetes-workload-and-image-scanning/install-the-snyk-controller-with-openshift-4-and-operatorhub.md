# OpenShift 4 및 OperatorHub와 함께 Snyk 컨트롤러 설치

Kubernetes 워크로드에 대한 취약점 세부 정보를 얻으려면 Snyk 관리자가 먼저 클러스터에 Snyk 컨트롤러를 설치해야합니다. 대부분의 kubernetes 플랫폼에서 Snyk monitor는 올바르게 작동하기 위해 몇 가지 최소 구성 항목만 요구합니다.

모든 Kubernetes 배포와 마찬가지로 Snyk 컨트롤러는 단일 네임스페이스 내에서 실행합니다.

## 전제 조건

{% hint style="info" %}
**기능 사용 여부**\
이 기능은 모든 유료 플랜에서 사용할 수 있습니다. 자세한 내용은 [pricing plans](https://snyk.io/plans/)를 참조하세요.
{% endhint %}

* Snyk 컨트롤러는 RedHat OpenShift 4를 통해 OperatorHub를 사용하여 설치합니다.
* 시작하기 전에 Snyk 계정이 필요합니다.
* Snyk에서 통합을 구성하려면 계정의 관리자여야 합니다.
* 클러스터에서 [emptyDir](https://kubernetes.io/docs/concepts/storage/volumes/#emptydir) 형식으로 최소 50GB의 스토리지를 사용할 수 있어야 하며 클러스터를 구성하는 사람은 관리자여야 합니다.
* Kubernetes 클러스터에서 외부 인터넷 액세스를 사용할 수 있어야 합니다.

## 진행 단계

1. Kubernetes command-line tool(`kubectl`)이 관련 클러스터를 가리키는지 확인합니다.
2.  클러스터 범위에서 Snyk 컨트롤러에 고유한 네임스페이스를 생성하여 컨트롤러가 모든 배포를 모니터링할 수 있도록 합니다.

    ```
    kubectl create namespace snyk-monitor
    ```

    **Tip**

    Use a unique namespace to isolate the controller resources more easily. This is generally good practice for Kubernetes applicatio고유한 네임스페이스를 사용하여 컨트롤러 리소스를 보다 쉽게 분리할 수 있습니다. 일반적으로 Kubernetes 애플리케이션에 적합한 방법입니다. 네임스페이스는 snyk-monitor라고 하며, 추후에 다른 리소스를 구성할 때 사용합니다.

    **Tip**

    Cluster scope is the default scope and we recommend you use this when installing the namespace so that we can scan the entire cluster. You can choose Namespaced scope, in whic클러스터 범위가 기본 범위이며 전체 클러스터를 검색할 수 있도록 네임스페이스를 설치할 때 범위를 설정하는 것이 좋습니다. Namespaced scope를 선택할 수 있습니다. 이 경우 Snyk 컨트롤러는 배포된 네임스페이스에서만 워크로드를 감시합니다.
3. Snyk 계정에 로그인하고 Integrations로 이동합니다.
4. kubernetes를 검색하고 클릭합니다.
5. Connect를 클릭하고 나타나는 페이지에서 Integration ID를 복사합니다. Snyk Integration ID는 `abcd1234-abcd-1234-abcd-1234abcd123`형식과 유사한 UUID입니다.
6. 다음 단계에서 Kubernetes 환경에서 사용할 수 있도록 저장합니다.
7.  Snyk monitor는 Snyk Integration ID를 사용하고 Dockercfg 파일을 사용하여 실행합니다. 개인 레지스트리를 사용하지 않는 경우 이전 단계의 Snyk Integration ID가 포함된 `snyk-monitor`라는 Kubernetes 암호를 생성하고 다음 명령어를 실행합니다.

    ```
    kubectl create secret generic snyk-monitor -n snyk-monitor --from-literal=dockercfg.json={} --from-literal=integrationId=abcd1234-abcd-1234-abcd-1234abcd1234
    ```

    개인 레지스트리를 사용하지 않는 경우 다음 단계를 건너뜁니다.\
    **Note**: Integration이 작동하려면 secret을 `snyk-monitor`라고 불러야합니다.
8. 스캔해야 할 이미지가 개인 레지스트리에 존재하는 경우 Snyk Integration ID와 `Dockercfg` 파일을 모두 사용하여 암호(`snyk-monitor`)를 만들어 해당 레지스트리에 액세스할 수 있는 자격 증명을 제공합니다. monitor가 개인 레지스트리에서 이미지를 조회하려면 Dockercfg 파일이 필요합니다. 일반적으로 `Dockercfg` 복사본은 `$HOME/.docker/config.json`에 있습니다.
   1.  `Dockercfg` 구성 파일을 생성합니다.

       ```
       {
         "auths": {
           "gcr.io": {
             "auth": "BASE64-ENCODED-AUTH-DETAILS"
           }
           // Add other registries as necessary
         }
       }
       ```
   2.  추가한 파일로 암호를 생성합니다.

       ```
       kubectl create secret generic snyk-monitor -n snyk-monitor --from-file=dockercfg.json --from-literal=integrationId=abcd1234-abcd-1234-abcd-1234abcd1234
       ```
9.  레지스트리가 자체 서명된 인증서 또는 기타 추가 인증서를 사용하는 경우 Snyk monitor에서 인증서를 사용할 수 있도록 해야합니다. 먼저 티렉토리에 `.crt`, `.cert` 및/또는 `.key` 파일을 배치하고 ConfigMap을 작성합니다.

    ```
    kubectl create configmap snyk-monitor-certs \
            -n snyk-monitor --from-file=
    ```
10. 안전하지 않은 레지스트리를 사용하거나 레지스트리가 정규화되지 않은 이미지를 사용하는 경우 `registries.conf` 파일을 제공할 수 있습니다.

    ```
    [[registry]]
    location = "internal-registry-for-example.net/bar"
    insecure = true
    ```

    형식 및 추가 예제에 대한 자세한 내용은 [documentation](https://github.com/containers/image/blob/master/docs/containers-registries.conf.5.md)을 참조하세요. 파일을 생성한 후에는 이 파일을 사용하여 다음과 같이 ConfigMap을 생성할 수 있습니다.

    ```
    kubectl create configmap snyk-monitor-registries-conf \
            -n snyk-monitor \
            --from-file=
    ```
11. OCP(OpenShift Container Platform) 웹 콘솔에 로그인하고 OperatorHub에서 **Snyk**을 검색하여 **Snyk Operator**를 설치합니다.
12. **Installed Operators** 영역이 성공적으로 설치되었는지 두번 확인합니다.
13. 이제 **Subscription** 탭에서 **Snyk controller**에 대한 Operator Subscription을 설치합니다. 필요에 따라 "A specfic namespace on the cluster"를 사용하거나 기본값인 “All namespaces on the cluster”를 사용합니다.\
    **Tip**:\
    클러스터 범위가 기본 범위이며 전체 클러스터를 검색할 수 있도록 네임스페이스를 설치할 때 이 범위를 사용하는 것이 좋습니다. Namespaced scope를 선택할 수 있습니다. 이 경우 Snyk 컨트롤러는 배포된 네임스페이스에서만 워크로드를 감시합니다.

    **Note**:\
    워크로드를 검색할 때 Snyk은 항상 안정적은 채널을 사용합니다.

    1. 나머지 기본 구성은 그대로 유지합니다.
    2. OpenShift Container Platform 클러스터의 네임스페이스에서 연산자를 사용할 수 있게 하려면 Subscribe를 클릭합니다.
14. **Snyk Monitor**의 인스턴스를 생성합니다. **Snyk Monitor** 사용자 정의 리소스에서 Create instance를 클릭하세요.
15. 클러스터에서 성공적으로 설치되었는지 두번 확인합니다.
16. **Snyk Operator** 및 **Snyk Monitor** 인스턴스를 성공적으로 설치한 후에는 Snyk에서도 클러스터를 확인할 수 있습니다.

![Example of successful installation from the cluster.](<../../../../.gitbook/assets/image (40).png>)
