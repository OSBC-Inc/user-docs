# Tool: Snyk-SCM- Contributors-Count

## 이 Tool은 무엇을 합니까?

이 Tool은 다음 SCM에 대해 지난 90일 동안의 기여자 수 요약을 계산하고 출력합니다:

* Azure Devops
* Bitbucket Cloud
* Bitbucket Server
* GitHub
* GitHub Enterprise
* GitLab
* GitLab Server

{% hint style="info" %}
명명 규칙과 관련하여 SCM 간에 약간의 차이가 있습니다. 예를 들어 GitHub의 "Orgs"는 Azure의 "Projects"이고 Bitbucket의 "Workspaces"일 수 있습니다. 이러한 차이점은 Tool이 각 SCM에 대해 허용하는 command에 반영됩니다.
{% endhint %}

## **SCM-Contributors-Count Tool의 작동 방식**

이 Tool은 두 가지 모드로 작동합니다: **Onboarding**전 사용 범위 지정 과 **Snyk License Consumption.**

* **Onboarding**전 사용 범위 지정**:** Snyk에 onboard하고 SCM 전체의 개발자 수를 추정하고 싶은 사용자를 위한 것입니다.\
  이 모드에서 Tool 사용자가 제공한 자격 증명을 사용하여 SCM에서 직접 모든 정보를 가져옵니다.
* **Snyk License Consumption (Bitbucket 및 Azure에만 유효):** license consumption(기여자 수, 이름, 이메일 등)에 대한 일부 명확성과 세부 정보를 원하는 기존 Snyk 계정이 있는 사용자의 경우.\
  이 모드에서 Tool은 Snyk이 모니터링하는 SCM 관련 프로젝트를 가져온 다음 SCM의 저장소와 일치시키고 해당 저장소/프로젝트에 대해서만 기여자를 계산합니다.

## Tool 다운로드

다음 command를 실행하세요:

```
npm i -g snyk-scm-contributors-count
```

릴리스 페이지에서 [바이너리 파일](https://github.com/snyk-tech-services/snyk-scm-contributors-count/releases)을 얻을 수도 있습니다.
