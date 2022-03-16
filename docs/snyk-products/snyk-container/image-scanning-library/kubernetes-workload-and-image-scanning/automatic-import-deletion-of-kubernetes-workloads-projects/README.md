# Kubernetes 워크로드 프로젝트 자동으로 가져오기/삭제

{% hint style="info" %}
이 기능은 현재 베타 버전입니다. 피드백을 보내주시면 감사하겠습니다.
{% endhint %}

스캔한 워크로드를 자동으로 가져오고 Snyk에서 직접 업데이트하도록 Snyk 컨트롤러를 구성하여 취약점을 테스트하고 모니터링할 수 있습니다.

## 워크로드 자동으로 가져오기/삭제 활성화

Snyk 컨트롤러의 Helm Charts에는 Jobs 및 Pods를 제외한 모든 워크로드에 대한 이벤트를 처리하기위한 기본 정책이 이미 프로비저닝되어 있습니다. 이 기능을 활성화하려면 Helm Charts 설치에서 Snyk 조직 공개 ID를 제공하세요.

```
helm upgrade --install snyk-monitor snyk-charts/snyk-monitor \
    --namespace snyk-monitor \
    --set clusterName="Production cluster" \
    --set policyOrgs={19982df2-0ed5-4a16-b355-e6535cfc41ef}
```

_**policyOrgs**_는 조직 공개 ID 목록입니다. 자동으로 가져오기 및 삭제 기능을 사용하기 위해둘 이상의 조직을 추가할 수 있습니다. 조직의 설정 페이지에서 이 공개 ID를 찾을 수 있습니다.

{% hint style="info" %}
Snyk 컨트롤러를 프로비저닝하는 데 사용된 것과 동일한 Kubernetes 통합 ID를 공유하는 조직만 사용할 수 있습니다.
{% endhint %}
