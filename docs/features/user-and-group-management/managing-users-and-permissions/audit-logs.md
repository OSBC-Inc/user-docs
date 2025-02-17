# Audit 로그

Audit logsSnyk은 [API를 통해 감사 로그에 액세스](https://snyk.docs.apiary.io/)할 수 있는 엔드포인트를 제공합니다. 다음과 같은 사용자 작업에 대한 데이터를 쿼리할 수 있습니다:

* 사용자 로그인 및 로그아웃
* 사용자의 역할이 변경
* 라이센스 정책 수정, 누구에 의한 수정인지
* 서비스 계정 생성 또는 삭제

최대 지난 90일 동안 사용자가 시작한 활동을 쿼리할 수 있습니다. 더 이전에 쿼리해야 하는 경우 [지원 팀](https://support.snyk.io/hc/en-us/requests/new)에 문의하세요. 누가 대신 콜드 스토리지에서 이 데이터에 액세스할 수 있습니다.

이 끝점을 사용하여 예기치 않은 활동을 소급하여 분류하고, 온보딩을 지원할 수 있도록 새 사용자가 추가될 때마다 확인하거나, 비정상적인 행동 보고서에 대한 조기 경고를 받기 위해 사용자 역할의 변경 사항을 모니터링할 수도 있습니다.

## **지원**

{% hint style="info" %}
**기능 가용성**

Snyk API는 모든 유료 플랜에서 사용할 수 있습니다. 자세한 내용은 [요금제](https://snyk.io/plans/)를 참조하세요.
{% endhint %}
