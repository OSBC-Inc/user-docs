---
description: >-
  워크플로에 Snyk IAC를 추가한 후 스캔의 민감도 또는 규칙에 할당된 심각도를 변경할 수 있습니다. 이 섹션에서는 이를 수행하는 방법을
  보여줍니다.
---

# Snyk IAC 스캔 매개변수 조정

## CLI Severity Threshold 조정

Snyk Orb에 대한 통과/실패 기준을 변경하는 한 가지 방법은 `--severity-threshold` 인수를 전달하는 것입니다. 이를 통해 빌드를 중단하기 위해 발견해야 하는 심각도 구성 오류를 선택할 수 있습니다.

이 예에서는 심각도가 High인 구성 오류만 식별하도록 Snyk에 지시합니다:

```
workflows:
  build_test:
    jobs:
      - run_tests
      - build_docker_image
      - snyk/scan-iac:
          args: part03/iac_gke_cluster --severity-threshold=high
      - gke_create_cluster:
```

발견된 결함이 모두 Medium 및 Low 심각도이므로 워크플로의 Snyk 단계를 통과합니다.

![Snyk 워크플로는 발견된 문제가 0개로 통과되었습니다.](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/image%20\(4\).png)

이 예에서는 심각도가 High인 문제가 발견된 경우에만 파이프라인을 중단합니다.

## Snyk UI에서 Rule Thresholds 조정

Snyk에서 제공하는 [기본 심각도 임계값](https://snyk.io/security-rules)을 재정의하려는 경우 Snyk UI에서 수행할 수 있습니다. 이를 통해 조직 수준에서 각 IAC 보안 규칙의 심각도를 변경할 수 있습니다.

이렇게 하려면 Organization -> Settings -> Infrastructure as Code로 이동합니다. 아래 목록이 표시됩니다.

![Snyk UI에서 Rule Thresholds 조정](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/image%20\(3\).png)

적절하다고 생각되는 대로 규칙을 조정하십시오. 다음에 워크플로가 실행되면 Snyk Orb는 새 심각도 수준에 따라 Terraform 파일을 평가합니다.

### Snyk Orb에서 사용하는 Snyk 조직 구성

Snyk Orb 출력은 보안 규칙 평가에 사용되는 Snyk Org를 식별합니다.

![Orb에서 사용하는 Snyk Org](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/image%20\(1\).png)

다른 조직에서 규칙을 사용하려면 `--org` 매개변수를 `args`에 전달하십시오.

{% hint style="info" %}
Snyk Orb는 SNYK\_TOKEN이 생성된 조직의 심각도 수준을 평가합니다. 다른 조직을 지정하는 경우 토큰이 해당 조직에 액세스할 수 있어야 합니다.
{% endhint %}

```
workflows:
  build_test:
    jobs:
      - run_tests
      - build_docker_image
      - snyk/scan-iac:
          args: part03/iac_gke_cluster --severity-threshold=high --org=neworg
      - gke_create_cluster:
```

This allows you to have different rulesets for different environments where your applications run.
