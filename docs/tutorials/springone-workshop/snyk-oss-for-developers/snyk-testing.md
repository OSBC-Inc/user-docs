# GitHub에서 Snyk 테스트

## pull request에 대한 Snyk test

Snyk은 merge 프로세스에서 취약점 및 라이선스 확인에 대한 pull request를 테스트합니다. 이렇게 하면 보안 게이트를 설정하고 pull request가 조직의 라이선스 정책을 충족하지 않는 새로운 취약점 또는 준수하지 않은 오픈소스 라이브러리를 소스코드 baseline에 추가하는 것을 방지할 수 있습니다. Snyk test 검사의 결과는 소프트웨어 개발 팀에 미치는 영향과 속도를 최소화하면서 보안 게이트 프로세스에 유연성을 제공하도록 구성할 수 있습니다.

이전 단계에서는 아래 스크린샷으로 이동하는 pull request 워크플로우를 완료했습니다. PR 워크플로우가 완료되면 Snyk은 프로젝트에 설정된 취약점과 라이선스 정책을 검증했습니다. 정책에 따라 검사가 통과 또는 실패하고 GitHub UI에 표시됩니다.

샘플 애플리케이션의 경우 모든 검사가 통과되고 merge pull request 버튼을 사용하여 pull request를 master 브랜치와 merge할 수 있습니다.

{% hint style="info" %}
[Snyk Test for Pull Request](https://support.snyk.io/hc/en-us/articles/360004032117-GitHub-integration#UUID-58e66c47-1931-675e-6437-c48fc9b71438\_section-5dc5a2318c45e-idm44771256643696)에 대한 자세한 내용은 제품 설명서를 참조하십시오.
{% endhint %}

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/screen-shot-2020-08-22-at-1.08.53-pm.png)
