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

1. **Artifactory**(공개적으로 액세스 가능) 스위치를 전환하면 이제 Artifactory Broker 토큰을 생성하기 위한 양식이 표시됩니다.
2. **Generate and Save** 버튼 클릭
3. 생성된 토큰을 복사합니다. 새 브로커 클라이언트를 설정하는 데 필요합니다.
4.  Dockerhub에서 Broker Artifactory 이미지 가져오기:

    ```
    docker pull snyk/broker:artifactory
    ```
5.  도커 이미지 실행 및 브로커 변수 제공

    ```
    docker run --restart=always \
      -p 8000:8000 \
      -e BROKER_TOKEN=secret-broker-token \
      -e ARTIFACTORY_URL=acme.com/artifactory \
      -e RES_BODY_URL_SUB=http://acme.com/artifactory \ 
      snyk/broker:artifactory
    ```
6. Artifactory Integration 설정 페이지를 새로 고쳐 연결 상태를 확인하십시오. 연결 오류가 표시되지 않아야 합니다.

## 브로커 변수

| 변수                 | 설명                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `BROKER_TOKEN`     | settings ![](../../../.gitbook/assets/cog\_icon.png)**> Integrations > Artifactory 에서 생성된 토큰**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| `ARTIFACTORY_URL`  | <p>다음과 같은 형식의 Artifactory 인스턴스 URL:<br><code>[http://][username:password@]hostname[:port]/artifactory</code></p><p><code></code></p><p><strong>선택 필드</strong></p><ol><li><em>Protocol</em>: 기본값은 <code>https://</code> 인증서가 없고 인스턴스에 대신 <code>http://</code>가 필요한 경우에만 지정해야 합니다.</li><li>기본 인증: 기본 인증이 필요하지 않은 경우 생략합니다.<br>URL은 인증을 방해할 수 있는 오류를 방지하기 위해 사용자 이름과 비밀번호 정보를 모두 인코딩합니다.</li></ol><ol><li><em>Port</em>: 포트 번호가 필요하지 않은 경우 생략</li></ol><p><strong>쉬운 예</strong><br><code>acme.com/artifactory</code></p><p><br><strong>복잡한 예</strong><br><code>http://alice:mypassword@acme.com:8080/artifactory</code></p> |
| `RES_BODY_URL_SUB` | <p>http://를 포함하고 기본 인증 자격 증명이 없는 Artifactory 인스턴스의 URL입니다.<br><br>npm/Yarn 통합에만 필요합니다.</p><p><br><strong>예</strong><br><code>http://acme.com/artifactory</code></p>                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
