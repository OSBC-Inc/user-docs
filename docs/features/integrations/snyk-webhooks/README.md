# Snyk Webhooks

### Snyk API용 Snyk Webhooks

사용, 검증 및 예제에 대한 정보를 얻으려면[ Snyk API documentation for Webhooks](https://snyk.docs.apiary.io/#introduction/consuming-webhooks)를 방문하십시오.

{% embed url="https://snyk.docs.apiary.io/#introduction/consuming-webhooks" %}

Webhooks를 사용하면 Snyk 시스템 이벤트에 대한 알림을 받을 수 있으므로 알림을 작성하고 프로젝트의 변경 사항에 대응할 수 있습니다.

이벤트가 트리거되면 Snyk는 HTTP POST 요청을 필요한 모든 정보와 함께 해당 이벤트에 대해 구성한 URL로 보냅니다.

### 사용 사례 예시

#### 알림

조직의 비즈니스 커뮤니케이션/협업 소프트웨어에서 즉각적인 알림/경보를 받을 수 있습니다. 단계별 지침은 [Microsoft Teams](../../../tutorials/microsoft-azure/notifications-in-microsoft-teams/)와 함께 이 설정을 위한 무료 튜토리얼을 참조하십시오.

#### 사고 대응

비즈니스에 영향을 미치기 전에 중요한 문제에 대응하십시오. 최신 인시던트 관리 및 Snyk를 채택하여 애플리케이션 보안보다 앞서십시오. 이 사용 사례에 대한 자세한 내용은 블로그 ["Shifting left security incident management with the Snyk & Opsgenie integration"](https://snyk.io/blog/security-incident-management-snyk-opsgenie-integration/) 과 통합 구성에 대한 안내를 제공하는 무료 [Opsgenie](../../../tutorials/atlassian/opsgenie/) 가이드를 참조하십시오.

#### SIEM(보안 정보 및 이벤트 관리)

다양한 소스에 걸쳐 실시간 보안 경고를 단일 플랫폼으로 통합하십시오. Snyk과 Rapid7의 파트너십 및 NAT이 함께 보안 위험을 줄이는 방법에 대해 자세히 알아보십시오.

#### 취약점 관리 및 집계

다양한 [Snyk Partner integrations](../vulnerability-management-tools/)에서 포괄적인 솔루션 목록을 찾아보십시오.

### Webhook 헤더

이벤트 메시지는 요청 본문에 이벤트 페이로드가 JSON으로 있는 `application/json`의 `Content-Type​`과 함께 전달됩니다. 또한 다음 헤더를 보냅니다.

* `X-Snyk-Event` 이벤트 이름 및 `ping/v1`과 같은 페이로드 버전입니다.
* `X-Snyk-Transport-ID` delivery를 식별하기 위한 GUID입니다.
* ​ `X-Snyk-Timestamp`an ISO 8601 타임스탬프 이벤트 발생 시간(예: `2020-09-25T15:27:53Z`)입니다.
* `X-Hub-Signature` webhooks를 보호하고 실제로 Snyk에서 요청이 전송되었는지 확인하는 데 사용되는 요청 본문의 HMAC 16진수 다이제스트입니다.
* `User-Agent​` 요청의 출처를 식별합니다(예: ​`Snyk-Webhooks/XXX`).

각 webhook은 모든 이벤트를 수신합니다.

### 보안 SSL

Webhooks는 HTTPS 프로토콜을 사용하는 URL에 대해서만 구성할 수 있습니다. HTTP가 허용되지 않습니다.

### 서명요청

webhook을 만들 때 비밀을 제공해야 합니다. 이 문자열은 Snyk에서 전송되도록 사용자에게 서명하는 데 사용할 문자열입니다. 비밀은 다음과 같습니다.

* 엔트로피가 높은 임의의 문자열입니다.
* 다른 용도로는 사용되지 않습니다.
* Snyk 및 webhook 전송 소비 코드만 알 수 있습니다.

webhooks로 전송되는 모든 전송에는 전송에 대한 해시 서명이 포함된 ​`X-Hub-Signature` ​헤더가 있습니다. 서명은 요청 본문의 HMAC 16진수이며, sha256과 사용자의 암호를 HMAC 키로 사용하여 생성됩니다.

{% hint style="info" %}
`X-Hub-Signature​`는 항상 `sha256=`으로 시작합니다.
{% endhint %}
