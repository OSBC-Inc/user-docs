# CircleCI 구성에 Snyk Orb 추가

In the CircleCI Academy Orbs module you learned about Orbs, packages of configuration that simplify your builds. [Snyk's Orb](https://circleci.com/developer/orbs/orb/snyk/snyk) exposes the [Snyk CLI](https://support.snyk.io/hc/en-us/articles/360003812578-CLI-reference), allowing you to find and fix known vulnerabilities in app dependencies, container images, and infrastructure as code.

CircleCI Academy Orbs 모듈에서 빌드를 단순화하는 구성 패키지인 Orbs에 대해 배웠습니다. [Snyk's Orb](https://circleci.com/developer/orbs/orb/snyk/snyk)는 [Snyk CLI](https://support.snyk.io/hc/en-us/articles/360003812578-CLI-reference)를 노출하여 앱 종속성, 컨테이너 이미지 및 코드형 인프라에서 알려진 취약점을 찾아 수정할 수 있습니다.

## CircleCI 구성 YML에 Snyk Orb 추가

[learn-iac](https://github.com/datapunkz/learn\_iac) 저장소의 포크에서 `.circleci/config.yml` 파일을 엽니다. `@x.y.z`를 Orb Registry에서 최신 버전의 Snyk Orb로 대체하여 Snyk Orb를 맨 위에 추가합니다.

```
version: 2.1

orbs:
  snyk: snyk/snyk@x.y.z

jobs:
  ...
```

Orb를 추가하면 `snyk` 명령 및 작업이 워크플로에 노출됩니다. 워크플로에서 추가할 위치를 선택할 때 요구 사항을 고려하십시오.

## 워크플로우에 스캔 IAC 작업 추가

이 예에서는 `gke-create-cluster` 작업 전에 `snyk/scan-iac` 작업을 추가하여 클라우드 인프라를 만들기 전에 Terraform 파일이 올바르게 구성되었는지 확인합니다. `args` 매개변수는 구성 오류를 확인할 파일을 가리키며 [다른 Snyk CLI 인수](https://support.snyk.io/hc/en-us/articles/360018728618-Test-your-configuration-files)를 전달하는 데 사용할 수도 있습니다.

```
workflows:
  build_test:
    jobs:
      - run_tests
      - build_docker_image
      - snyk/scan-iac:
          args: part03/iac_gke_cluster/
      - gke_create_cluster:
          requires:
            - run_tests
            - build_docker_image
            - snyk/scan-iac
```

{% hint style="info" %}
Snyk Infrastructure as Code는 Kubernetes 및 AWS CloudFormation 파일에서 구성 오류를 확인할 수도 있습니다. [Snyk IAC 설명서](https://support.snyk.io/hc/en-us/articles/360018728618-Test-your-configuration-files)에서 자세히 알아보십시오.
{% endhint %}

준비가 되면 변경 사항을 커밋하고 병합하여 워크플로 실행을 트리거합니다.

## 결과 작업

워크플로가 실행되면 출력이 CircleCI 프로젝트 실행에 표시됩니다. 스캔한 `main.tf` 파일에서 문제가 발견되어 작업이 실패합니다.

![CircleCI UI의 Snyk Orb 출력](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/iac-job-run-fail.png)

{% hint style="info" %}
Snyk Orb에 전원을 공급하는 Snyk IAC CLI의 출력 해석에 대해 자세히 알아보려면 [Snyk Docs의 구성 스캔 문제 이해](https://support.snyk.io/hc/en-us/articles/360012499738-Understanding-configuration-scan-issues)를 방문하십시오.
{% endhint %}

### Snyk UI에서 결과 보기

GitHub 통합을 사용하여 `learn-iac` 저장소의 포크를 Snyk UI로 가져옵니다. 방법을 알아보려면 [Snyk IAC 설명서](https://support.snyk.io/hc/en-us/articles/360011018938-Configure-your-integration-to-find-security-issues-in-your-Terraform-files)를 참조하십시오. 가져오면 Snyk UI에 매니페스트 파일이 표시됩니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/imported-iac-project.png)

`main.tf` 파일을 클릭하면 구성의 영향 및 해결 방법과 같은 추가 정보와 함께 발견된 문제에 대한 인라인 보기가 표시됩니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/iac-result-details.png)

다음 섹션에서는 이 분석을 조정하여 테스트의 통과/실패 기준을 조정하는 방법을 보여줍니다.
