# Artifactory Registry 설정

## **개요**

{% hint style="info" %}
**기능 가용성**

이 기능은 엔터프라이즈 플랜에서 사용할 수 있습니다. 자세한 내용은 [요금제](https://snyk.io/plans/)를 참조하세요.
{% endhint %}

{% hint style="success" %}
Artifactory Package Repository 통합은 현재 [Maven](../../../products/snyk-open-source/language-and-package-manager-support/snyk-for-java-gradle-maven.md) **** 및 [Node.js](../../../products/snyk-open-source/language-and-package-manager-support/snyk-for-javascript.md)(npm 및 Yarn) 프로젝트를 지원합니다.
{% endhint %}

사용자 지정 Artifactory Package Repository를 연결하면 Snyk이 사용자 지정 레지스트리에서 호스팅되는 패키지의 모든 직접적 및 전이적 종속성을 해결하고 보다 완전하고 정확한 종속성 그래프 및 관련 취약성을 계산할 수 있습니다.

두 가지 유형의 Artifactory 패키지 저장소를 구성할 수 있습니다:

1. 기본 인증으로 보호되는 공개적으로 액세스 가능한 인스턴스
2. Snyk Broker를 통해 액세스되는 사설 네트워크의 인스턴스(기본 인증 포함 또는 미포함)

## 시작하기

1. settings ![](../../../.gitbook/assets/cog\_icon.png) > **Integrations > Package Repositories > Artifactory**로 이동합니다.
2. 처음에 이 화면을 봐야 합니다

![](../../../.gitbook/assets/screenshot\_2020-04-17\_at\_14.38.12.png)

{% hint style="info" %}
"Snyk Broker" 스위치가 표시되지 않으면 필요한 권한이 없는 것이며 공개적으로 액세스 가능한 인스턴스만 추가할 수 있습니다.

개인 레지스트리를 추가하려는 경우, [지원팀에 문의하세요](https://support.snyk.io/hc/en-us/requests/new).
{% endhint %}

### 공개적으로 액세스 가능한 인스턴스 설정

1. Artifactory 인스턴스의 URL을 입력하십시오. 이것은 반드시 **/artifactory**로 끝나야 합니다.
2. 사용자 이름 입력
3. 암호 입력
4. **저장** 누르기

### 중개된 인스턴스 설정

1. Toggle **Artifactory (publicly accessible)** switch, you should now see a form for generating an Artifactory Broker token
2. Click on **Generate and Save** button
3. Copy the token that was generated for you, it will be needed to set up a new Broker Client
4.  Pull Broker Artifactory image from Dockerhub:

    ```
    docker pull snyk/broker:artifactory
    ```
5.  Run docker image and provide [broker variables](artifactory-registry-setup.md#broker-variables)

    ```
    docker run --restart=always \
      -p 8000:8000 \
      -e BROKER_TOKEN=secret-broker-token \
      -e ARTIFACTORY_URL=acme.com/artifactory \
      -e RES_BODY_URL_SUB=http://acme.com/artifactory \ 
      snyk/broker:artifactory
    ```
6. Check connection status by refreshing Artifactory Integration Settings page, no connection error should be displayed

#### Broker variables

| Variable           | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| ------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `BROKER_TOKEN`     | The token generated in settings ![](../../../.gitbook/assets/cog\_icon.png)**> Integrations > Artifactory**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| `ARTIFACTORY_URL`  | <p>The URL to your Artifactory instance in the format:<br><code>[http://][username:password@]hostname[:port]/artifactory</code></p><p><strong>Optional fields</strong></p><ol><li><em>Protocol</em>: Defaults to <code>https://</code><br>This should only be specified when no certificate is present and <code>http://</code> is required instead for your instance</li><li><em>Basic auth</em>: Omit if no basic auth required.<br>URL encode both username and password info to avoid errors that may prevent authentication.</li><li><em>Port</em>: Omit if no port number is needed</li></ol><p><strong>Minimal example</strong><br><code>acme.com/artifactory</code></p><p><br><strong>Complex example</strong><br><code>http://alice:mypassword@acme.com:8080/artifactory</code></p> |
| `RES_BODY_URL_SUB` | <p>The URL of the Artifactory instance, including http:// and without basic auth credentials.<br><br>Required for npm/Yarn integrations only.</p><p><br><strong>Example</strong><br><code>http://acme.com/artifactory</code></p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
