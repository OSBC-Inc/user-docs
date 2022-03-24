# Pushing a bundle

사용자 지정 규칙 bundle을 생성한 후 `push` 명령어를 사용하여 지원되는 OCI 레지스트리 중 하나에 자동으로 배포할 수 있습니다.

```
snyk-iac-rules push -r docker.io/example/test bundle.tar.gz
```

{% hint style="info" %}
먼저 컨테이너 레지스트리에 로그인하십시오. 예를 들어, Docker를 사용하면 `snyk-iac-rules` push 명령어을 실행하기 전에 `docker login`을 실행합니다.
{% endhint %}

[OCI 아티팩트 사양](https://github.com/opencontainers/artifacts)을 지원하는 OCI 레지스트리를 사용하고 [ORAS](https://github.com/oras-project/oras)를 활용하여 이를 달성합니다. 현재 지원하는 레지스트리는 다음과 같습니다.

* [Google Container Registry](https://cloud.google.com/container-registry)
* [DockerHub](https://hub.docker.com)
* [Elastic Container Registry](https://aws.amazon.com/ecr/)
* [Azure Container Registry](https://azure.microsoft.com/en-us/services/container-registry/)
* [JFrog Artifactory ](https://www.jfrog.com/confluence/display/JFROG/Docker+Registry)(note: OCI 아티팩트는 Artifactory v7.11.1 이상에서 지원)
* [Harbor](https://goharbor.io)
* [GitHub Container Registry](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-container-registry)

{% hint style="warning" %}
안전하지 않은 레지스트리는 지원하지 않습니다. 지원하는 유일한 프로토콜은 HTTPS입니다.
{% endhint %}

명령어를 실행하면 `latest` 태그를 사용하여 사용자 지정 규칙 bundle이 OCI 레지스트리에 push됩니다.

bundle을 버전을 지정하려는 경우 고유한 태그를 제공할 수도 있습니다.

```
snyk-iac-rules push -r docker.io/example/test:v0.0.1 bundle.tar.gz
```

이제 새로 구축된 [custom bundle로 snyk iac test를 실행할 수 있습니다](../use-iac-custom-rules-with-cli/).
