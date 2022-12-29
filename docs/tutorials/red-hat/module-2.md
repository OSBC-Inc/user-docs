# Module 2

## Red Hat Quay 프라이빗 컨테이너 레지스트리

Quay.io를 사용하여 GitHub, Bitbucket 등과 통합하여 컨테이너 빌드를 자동화할 수 있습니다. 로봇 계정을 사용하면 자동화된 액세스를 잠그고 각 배포를 감사할 수 있습니다. 이 예에서는 Quay.io 클라우드 계정을 사용하여 CLI를 사용하여 빌드, 스캔 및 레지스트리에 푸시할 이미지를 저장합니다.

### 취약점에 대한 컨테이너 이미지 스캔

먼저 Quay 레지스트리에 [`docker login`](https://docs.docker.com/engine/reference/commandline/login/)합니다. Quay를 처음 사용하는 경우 Docker CLI와 함께 사용할 암호화된 암호를 생성하는 방법을 배울 수 있는 [실습](https://quay.io/tutorial/)을 완료하는 것이 좋습니다.

{% hint style="info" %}
Docker CLI는 명령줄에 입력한 암호를 **일반 텍스트**로 저장합니다. 따라서 `docker login`에 사용할 암호화된 버전의 암호를 생성하는 것이 좋습니다.
{% endhint %}

아래 명령을 실행하여 `<QUAY_USER>`를 고유한 `Quay.io` 사용자 이름으로 대체하고 를 암호화된 암호로 대체하십시오.

```bash
docker login -u="<QUAY_USER>" -p="<GUID>" quay.io
```

그런 다음 터미널에서 이전에 복제한 goof repo의 디렉터리로 이동합니다. 이 디렉터리의 루트에 [`Dockerfile`](https://github.com/snyk/goof/blob/master/Dockerfile)이 표시됩니다. 아래와 같이 [`docker build`](https://docs.docker.com/engine/reference/commandline/build/) 명령을 사용하여 이 Dockerfile에서 이미지를 빌드하고 태그를 지정합니다. 다시 `<QUAY_USER>`를 사용자 이름으로 바꿉니다.

```bash
docker build -t <QUAY_USER>/goof .
```

이 시점에서 일반적으로 이미지를 레지스트리에 푸시합니다. 그러나 그렇게 하기 전에 한 가지 추가적이고 중요한 단계를 수행할 것입니다. 취약점을 식별하고 기본 이미지 권장 사항을 제공하기 위해 Snyk을 사용하여 컨테이너 이미지를 스캔합니다. 이를 위해 터미널에서 다음 명령을 실행합니다.

```bash
snyk monitor --docker quay.io/<QUAY_USER>/goof \
--file=submodules/goof/Dockerfile --org=<SNYK_ORG> \
--project-name=quay-cli-container-image
```

잠시 시간을 내어 위 명령에서 수행하는 작업을 분석해 보겠습니다. `monitor` 명령은 나중에 해당 결과를 검토할 수 있도록 [snyk.io](https://snyk.io/)의 계정에 대한 종속성 및 취약성의 상태를 기록합니다:

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/quay-cli-container-scan.gif)

완료되면 이미지를 Quay 레지스트리에 푸시할 준비가 된 것이며 아래와 같이 [`docker push`](https://docs.docker.com/engine/reference/commandline/push/) 명령을 호출하여 푸시합니다:

```bash
docker push quay.io/<QUAY_USER>/goof
```

Upon successful completion you should see results similar to the following:

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/docker-push.gif)

선택적으로 Quay.io에 로그인하고 적절한 이미지가 태그되었는지 확인하여 이미지가 실제로 성공적으로 Push되었는지 확인할 수 있습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/rh-quay.png)

Dockerfile에 대해 `snyk monitor`를 실행했을 때 `--org` 및 `--project-name`이라는 두 개의 매개변수를 전달했습니다. 이 작업을 통해 CLI의 결과를 Snyk 계정에 저장할 수 있었습니다. 결과 보고서는 이제 Snyk 계정에 로그인하고 가져온 프로젝트를 확인하여 사용할 수 있습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/container-image-scan-results.png)

메이저, 마이너 및 대체 업그레이드를 포함한 기본 이미지 수정 조언과 이미지를 다시 빌드해야 할 때의 조언을 받으려면 선호하는 Git 저장소와 통합하고 관련 Dockerfile이 포함된 저장소를 가져오십시오. 또한 [이미지에 Dockerfile을 추가](https://support.snyk.io/hc/en-us/articles/360003916218-Adding-your-Dockerfile-and-test-your-base-image)해야 합니다.

완료되면 **기본 이미지 업그레이드에 대한 권장 사항**이 표시됩니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/base-image-recommend.png)
