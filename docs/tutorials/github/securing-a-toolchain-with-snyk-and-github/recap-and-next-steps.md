# 요약 및 다음 단계

## 축하합니다! <a href="#congratulations" id="congratulations"></a>

이 실습의 끝에 도달했습니다. 대단한 여정이었습니다! 실습을 진행하면서 Snyk과 GitHub Actions가 함께 소프트웨어 제공 관행을 위한 안전한 지속적 통합 및 지속적 제공 패러다임을 촉진하는 데 어떻게 도움이 되는지 확인하셨기를 바랍니다.‌

이 실습이 마음에 드셨기를 바랍니다. 아래에서 귀하가 달성한 내용을 요약하고 Snyk에서 더 많은 가치를 얻는 데 도움이 되는 추가 리소스를 제공합니다.

## Snyk Open Source <a href="#snyk-open-source" id="snyk-open-source"></a>

Part 1에서는 Snyk 오픈 소스를 사용하여 샘플 애플리케이션의 오픈 소스 구성 요소에서 취약점을 찾았습니다. GitHub Integration을 구성하고 수정 Pull Request를 생성하고 릴리스 프로세스에 게이트를 구축하여 문제가 프로덕션 Branch로 전달되지 않도록 했습니다.‌

우리가 다루지 않은 몇 가지 사항:

### Automatic Dependency Upgrade Pull Requests <a href="#automatic-dependency-upgrade-pull-requests" id="automatic-dependency-upgrade-pull-requests"></a>

Why wait until vulnerabilities are published to upgrade your dependencies? Snyk can be configured to [automatically open pull requests on your behalf](https://support.snyk.io/hc/en-us/articles/360006581898-Upgrading-dependencies-with-automatic-PRs), to keep your dependencies up to date and healthy.‌

### 수정된 GitHub 계정을 사용하여 Snyk Pull Request 열기

Snyk allows you to [configure a specific GitHub account](https://support.snyk.io/hc/en-us/articles/360010843797-Opening-fix-and-upgrade-pull-requests-from-a-fixed-GitHub-account-) on whose behalf the fix and upgrade PRs will be opened. Our research shows that this increases the likelihood of a Fix PR getting merged, so check it out!‌

## Snyk Container <a href="#snyk-container" id="snyk-container"></a>

In Part 2, you used Snyk Container to find issues introduced by your choice of base image. You imported your Dockerfile into Snyk, and selected a less vulnerable base image for your application.

If you're working with containers, some resources worth checking out that we didn't cover:

Container Registry와 통합

Snyk can integrate with your Container Registry to easily import your container images for scanning with Snyk. We support [Docker Hub](https://support.snyk.io/hc/en-us/articles/360003916058-Configure-integration-for-Docker-Hub), [Azure Container Registry](https://support.snyk.io/hc/en-us/articles/360003915958-Configure-integration-for-ACR), [Google Container Registry](https://support.snyk.io/hc/en-us/articles/360003916118-Configure-integration-for-GCR), [Artifactory Container Registry](https://support.snyk.io/hc/en-us/articles/360003915998-Configuring-your-JFrog-Artifactory-container-registry-integration), and [AWS Elastic Container Registry](https://support.snyk.io/hc/en-us/articles/360003916078-Configure-integration-for-Amazon-Elastic-Container-Registry-ECR-).

### Docker의 도구와 함께 Snyk 사용

Snyk and Docker partnered to bring Snyk scanning into Docker Desktop and Docker Hub. If you're using those tools in your development process, and want to learn more, check out our [Lab: Build Secure Containers with Docker and Snyk](https://github.com/snyk/user-docs/tree/695c746d1b207ffdf923b84e4590d31b29e2cc73/docs/docker/lab-build-secure-containers-with-docker-and-snyk/README.md) to see it in action!

## Snyk Infrastructure as Code

In Part 3, you used Snyk Infrastructure as Code to find and fix configuration issues in your Kubernetes deployment manifests, and set up a gate that can prevent configuration issues from accidentally making their way into a Production environment.

### IaC Rule Severity 구성

Infrastructure as Code rules are not meant to be one-size-fits-all. Different workloads have different security requirements and tolerances, that's why we allow you to change how Snyk IaC scores your application configurations. Learn how to [adjust the severity scoring for IaC](https://support.snyk.io/hc/en-us/articles/360006402818#UUID-c1919782-6bfa-b84b-a638-3913cee39fc5) rules in our Docs.

### Kubernetes Integration

An extension of Snyk Container and Snyk IaC, we offer a Kubernetes Monitor that can identify configuration issues and container vulnerabilities in running workloads. To learn more, check out the [Snyk Kubernetes Integration Overview](https://support.snyk.io/hc/en-us/articles/360003916138-Kubernetes-integration-overview).

### Terraform Support

We didn't cover it in this Lab, but Snyk can also scan Terraform files for configuration issues. To learn more about our Terraform support, check out how to [Scan and Fix issues in your Terraform files](https://support.snyk.io/hc/en-us/articles/360010916577-Scan-and-fix-security-issues-in-your-Terraform-files).
