# 애플리케이션 스캔

다음 작업은 작업 공간을 연결하고 몇 가지 매개 변수로 `snyk/scan`을 호출하는 것으로 시작됩니다. `fail-on-issues`를 `false`로 설정하고 `severity-threshold`를 `high`로 설정하는 것과 같은 몇 가지 선택을 했습니다.

```yaml
  scan_app:
    <<: *defaults
    steps:
      - attach_workspace:
          at: ~/repo
      - snyk/scan:
          fail-on-issues: false
          monitor-on-build: true
          project: '${CIRCLE_PROJECT_REPONAME}/${CIRCLE_BRANCH}-app'
          severity-threshold: high
          token-variable: SNYK_TOKEN
          target-file: ./submodules/goof/package.json
```

{% hint style="info" %}
A detailed list of all supported parameters is available in the [Snyk orb documentation](https://circleci.com/orbs/registry/orb/snyk/snyk#commands-scan) page.
{% endhint %}
