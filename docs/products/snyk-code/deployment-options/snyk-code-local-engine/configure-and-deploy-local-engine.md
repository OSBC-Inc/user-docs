# 로컬 엔진 구성 및 배포

### Helm Chart 설치

release 이름을 `my-release`로 chart를 설치하려면 다음을 수행하십시오.:

```
$ helm install my-release <gziped-chart>
```

`local-code-engine` 이러한 명령은 기본 구성의 쿠버네티스 클러스터에 배포됩니다. **Parameters** 섹션에는 설치 중에 구성할 수 있는 매개변수가 나열됩니다.

chart 실행의 기본값 파일을 인쇄하는 방법:

```
$ helm show values <gziped-chart>
```

#### Helm Chart 제거

my-release 리소스를 제거/삭제하는 방법:

```
$ helm delete my-release
```

이 명령은 chart와 연결된 모든 쿠버네티스 구성 요소를 제거하고 release를 삭제합니다. 모든 기록도 삭제하려면 `--purge` 옵션을 사용합니다.

### 전역 매개변수

#### 전역 필수 매개변수

| Name                                          | Description        | Default Value |
| --------------------------------------------- | ------------------ | ------------- |
| `global.imagePullSecret.credentials.username` | 도커 허브 레지스트리 사용자 이름 | `""`          |
| `global.imagePullSecret.credentials.password` | 도커 허브 레지스트리 비밀번호   | `""`          |

#### Broker 필수 매개 변수

다음 SCM 구성 중 하나를 사용하십시오.:

| Name                        | Description                                                                                            | Default Value |
| --------------------------- | ------------------------------------------------------------------------------------------------------ | ------------- |
| `broker-client.brokerToken` | 고유한 broker client 토큰                                                                                   | `""`          |
| `broker-client.brokerType`  | 사용할 broker client 유형입니다. 지원되는 옵션: github-com, github-enterprise, gitlab, bitbucket-server, azure-repos | `""`          |

#### GitHub.com 매개변수

| Name                        | Description                                | Default Value |
| --------------------------- | ------------------------------------------ | ------------- |
| `broker-client.githubToken` | [http://github.com](http://github.com)용 토큰 | `""`          |

#### GitHub Enterprise 매개변수

| Name                          | Description                                | Default Value                                     |
| ----------------------------- | ------------------------------------------ | ------------------------------------------------- |
| `broker-client.githubToken`   | [http://github.com](http://github.com)용 토큰 | `""`                                              |
| `broker-client.githubHost`    | GitHub 서버의 호스트명                            | `""`                                              |
| `broker-client.githubApi`     | GitHub REST API URL, 스키마 제외                | `"{{ .Values.broker-client.githubHost }}/api/v3"` |
| `broker-client.githubGraphql` | GitHub GraphQL API URL, 스키마 제외             | `"{{ .Values.broker-client.githubHost }}/api"`    |

#### Gitlab 매개변수

| Name                        | Description     | Default Value |
| --------------------------- | --------------- | ------------- |
| `broker-client.gitlabToken` | gitlab 호스트      | `""`          |
| `broker-client.gitlabHost`  | gitlab 서버의 호스트명 | `""`          |

#### Bitbucket server 매개변수

| Name                              | Description        | Default Value |
| --------------------------------- | ------------------ | ------------- |
| `broker-client.bitbucketUsername` | bitbucket 사용자명     | `""`          |
| `broker-client.bitbucketPassword` | bitbucket 비밀번호     | `""`          |
| `broker-client.bitbucketHost`     | bitbucket 서버의 호스트명 | `""`          |

#### Azure Repos 매개변수

| Name                            | Description      | Default Value |
| ------------------------------- | ---------------- | ------------- |
| `broker-client.azureReposToken` | Azure Repos용 토큰  | `""`          |
| `broker-client.azureReposHost`  | Azure Repos 호스트명 | `""`          |
| `broker-client.azureReposOrg`   | Azure 조직 이름      | `""`          |

### Snyk Code 로컬 엔진 매개변수

#### codeapi

| Name                                 | Description                                         | Default Value |
| ------------------------------------ | --------------------------------------------------- | ------------- |
| `codeapi.imagePullSecrets`           | 도커 레지스트리 암호명을 배열로                                   | `[]`          |
| `codeapi.nameOverride`               | names.fullname 템플릿을 부분적으로 재정의하는 문자열(release 이름 유지함) | `""`          |
| `codeapi.fullnameOverride`           | names.fullname 템플릿을 완전히 재정의하는 문자열                   | `""`          |
| `codeapi.serviceAccount.create`      | ServiceAccount 생성 여부를 지정                            | `true`        |
| `codeapi.serviceaccount.name`        | 생성할 ServiceAccount의 이름                              | `""`          |
| `codeapi.serviceAccount.annotations` | 추가 Service Account 주석(템플릿으로 평가됨)                    | `{}`          |
| `codeapi.podAnnotations`             | Pod 주석                                              | `{}`          |
| `codeapi.podSecurityContext`         | pod에 대한 보안 컨텍스트                                     | `{}`          |
| `codeapi.securityContext`            | 컨테이너에 적용될 보안 구성을 보유                                 | `{}`          |
| `codeapi.nodeSelector`               | pod 할당을 위한 집계 노드 레이블                                | `{}`          |
| `codeapi.tolerations`                | pod 할당을 위한 집게 허용 오차                                 | `[]`          |
| `codeapi.affinity`                   | pod 할당을 위한 전달자 선호도                                  | `{}`          |

#### bundle

| Name                                   | Description                                        | Default Value |
| -------------------------------------- | -------------------------------------------------- | ------------- |
| `bundle.imagePullSecrets`              | 도커 레지스트리 암호명을 배열로                                  | `[]`          |
| `bundle.nameOverride`                  | names.fullname 템플릿을 부분적으로 재정의하는 문자열(release명을 유지함) | `""`          |
| `bundle.fullnameOverride`              | names.fullname 템플릿을 완전히 재정의하는 문자열                  | `""`          |
| `bundle.serviceAccount.create`         | ServiceAccount 생성 여부 지정                            | `true`        |
| `bundle.serviceaccount.name`           | 생성할 ServiceAccount의 이름                             | `""`          |
| `bundle.serviceAccount.annotations`    | 추가 서비스 계정 주석(템플릿으로 평가됨)                            | `{}`          |
| `bundle.podAnnotations`                | Pod 주석                                             | `{}`          |
| `bundle.podSecurityContext`            | pod에 대한 보안 컨텍스트                                    | `{}`          |
| `bundle.securityContext`               | 컨테이너에 적용될 보안 구성을 보유합니다.                            | `{}`          |
| `bundle.nodeSelector`                  | Pod 할당을 위한 집계 노드 레이블                               | `{}`          |
| `bundle.tolerations`                   | Pod 할당에 대한 집계 허용 오차                                | `[]`          |
| `bundle.affinity`                      | Pod 할당을 위한 전달자 선호도                                 | `{}`          |
| `bundle.terminationGracePeriodSeconds` | Pod가 정상적으로 종료되어야 하는 기간(초)                          | `10`          |

#### suggest

| Name                                 | Description                                      | Default Value |
| ------------------------------------ | ------------------------------------------------ | ------------- |
| `suggest.imagePullSecrets`           | 도커 레지스트리 암호명을 배열로                                | \`\[]         |
| `suggest.nameOverride`               | names.fullname 템플릿을 부분적으로 재정의하는 문자열(릴리스 이름을 유지함) | `""`          |
| `suggest.fullnameOverride`           | names.fullname 템플릿을 완전히 재정의하는 문자열                | `""`          |
| `suggest.serviceAccount.create`      | names.fullname 템플릿을 완전히 재정의하는 문자열                | `true`        |
| `suggest.serviceaccount.name`        | 생성할 ServiceAccount의 이름                           | `""`          |
| `suggest.serviceAccount.annotations` | 추가 서비스 계정 주석(템플릿으로 평가됨)                          | `{}`          |
| `suggest.podAnnotations`             | Pod 주석                                           | `{}`          |
| `suggest.podSecurityContext`         | pod에 대한 보안 컨텍스트                                  | `{}`          |
| `suggest.securityContext`            | 컨테이너에 적용될 보안 구성을 보유합니다.                          | `{}`          |
| `suggest.nodeSelector`               | pod 할당을 위한 집계 노드 레이블                             | `{}`          |
| `suggest.tolerations`                | pod 할당에 대한 집계 허용 오차                              | `[]`          |
| `suggest.affinity`                   | pod 할당을 위한 전달자 선호도                               | `{}`          |

#### broker-client

| Name                                       | Description                                      | Default Value |
| ------------------------------------------ | ------------------------------------------------ | ------------- |
| `broker-client.codeSnippet.enabled`        | 코드 스니펫 활성화                                       | `false`       |
| `broker-client.imagePullSecrets`           | Docker 레지스트리 암호명을 배열로                            | `[]`          |
| `broker-client.nameOverride`               | names.fullname 템플릿을 부분적으로 재정의하는 문자열(릴리스 이름을 유지함) | `""`          |
| `broker-client.fullnameOverride`           | names.fullname 템플릿을 완전히 재정의하는 문자열                | `""`          |
| `broker-client.serviceAccount.create`      | ServiceAccount 생성 여부 지정                          | `true`        |
| `broker-client.serviceaccount.name`        | 생성할 ServiceAccount의 이름                           | `""`          |
| `broker-client.serviceAccount.annotations` | 추가 서비스 계정 주석(템플릿으로 평가됨)                          | `{}`          |
| `broker-client.podAnnotations`             | Pod 주석                                           | `{}`          |
| `broker-client.podSecurityContext`         | pod에 대한 보안 컨텍스트                                  | `{}`          |
| `broker-client.securityContext`            | <p>컨테이너에 적용될 보안 구성을 보유합니다.</p><p> </p>           | `{}`          |
| `broker-client.nodeSelector`               | pod 할당을 위한 집계 노드 레이블                             | `{}`          |
| `broker-client.tolerations`                | pod 할당에 대한 집계 허용 오차                              | `[]`          |
| `broker-client.affinity`                   | pod 할당을 위한 전달자 선호도                               | `{}`          |

### 서드파티 charts

당사가 사용하는 일부 타사 서비스를 구성하려는 경우 다음에서 예제를 참조하십시오:

* [Ambassador](https://github.com/emissary-ingress/emissary/tree/master/charts/emissary-ingress)
* [Redis](https://github.com/bitnami/charts/tree/master/bitnami/redis)
* [Fluentd](https://github.com/bitnami/charts/tree/master/bitnami/fluentd)

### Chart 사용

필요에 따라 제공된 YAML 파일을 편집할 수 있습니다.

또는 chart를 설치하는 동안 매개변수 값을 지정하는 고유한 YAML 파일을 사용할 수 있습니다. 예를 들어,

`$ helm install my-release -f your-values.yaml`

### Logging

Fluentd는 모든 서비스의 로그를 하나의 파일로 집계하는 데 사용됩니다.

로그 파일이 `fluentd-umbrella.logrotate.fileMaxSizeInMb` (기본값 500)을 초과하고 logrotate가 유지되는 파일 수가 `fluentd-umbrella.logrotate.filesToKeep` (기본값 14)인 경우를 제외하고 로그 파일은 매일 순환됩니다. 따라서 `fileMaxSizeInMb`를 초과하지 않는 한 하루 동안의 로그 파일은 다음 날에만 생성됩니다.

Logrotate는 로그 파일 수가 `filesToKeep`과 같을 때 가장 오래된 로그 파일을 제거하여 로그 파일 수가 `fluentd-umbrella.logrotate.filesToKeep`를 초과하지 않는지 확인합니다.

파일이 순환할 때 순환 날짜와 시간은 파일 이름에 접미사로 추가됩니다. 현재 로그를 보려면 `code.log` 파일을 추적해야 합니다. 과거에 작성된 로그를 가져오려면 보려는 시간 이후의 날짜 및 시간이 포함된 로그 파일을 선택합니다.

모든 로그 파일을 현재 디렉터리에 가져오려면 다음을 실행합니다:

```
kubectl cp <your-namespace>/<your-release>-fluentd-0:/var/log/snyk/logs ./
```

특정 날짜에 대한 로그 파일을 가져오려면 먼저 기존 로그 목록을 가져옵니다:

```
kubectl exec -it on-prem-fluentd-0 -- ls -l /var/log/snyk/logs
```

그 후 다음을 실행하여 가져올 로그 파일을 복사합니다:

```
kubectl cp <your-namespace>/<your-release>-fluentd-0:/var/log/snyk/logs/<file-name> ./<target-file-name>
```

{% hint style="info" %}
모든 파일을 복사하는 데 몇 분 정도 걸릴 수 있습니다.
{% endhint %}

### Snyk Code PR 스캔을 위해 broker client에 웹훅을 사용하도록 설정

SCM 웹훅을 만들고 처리할 수 있으려면 `broker-client`가 외부에 노출되어야 합니다.

기본 수신을 사용할 수 있으며, `broker-client.ingress.enabled`를 `true`로 설정하고 `broker-client.ingress.host`를 통해 broker client의 endpoints를 사용할 호스트(예: "broker-client.example.com")를 지정하여 활성화할 수 있습니다.기본 수신은 `broker-client` 서비스에서 `/webhook/*` 및 `/healthcheck` endpoints 노출합니다.

Note that the ingress IP still has to be made available on the specified host via a DNS A record, which will depend on your cloud provider or server setup.

By default, the ingress endpoints are insecure. In order to secure them using TLS, set `broker-client.ingress.tls.enabled` to `true`.

You can specify the name of the secret you wish to use with `broker-client.ingress.tls.secret.name`, or leave it empty to default to the name of the service suffixed with `-tls-secret`.

If you do not already have a secret created for that host, you can set the `key` and `cert` values to the key and certificate, respectively, that you created for use with the host that the ingress will be using (they will be Base64 encoded for you

Read more about securing an ingress with TLS [here](https://kubernetes.io/docs/concepts/services-networking/ingress/#tls).\
\\
