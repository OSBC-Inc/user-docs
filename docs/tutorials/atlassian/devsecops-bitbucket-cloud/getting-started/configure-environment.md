# 환경 구성

## AWS CLI (AWS Command Line Interface) 설치

이 연습에서는 [AWS CLI (AWS Command Line Interface)](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-welcome.html) 와 kubectl 및 eksctl을 사용합니다. AWS CLI 설치에 대한 자세한 설명서는 [AWS Documentation](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html)과 Linux 및 Windows용 설치 단계를 자세히 설명하는 [eksctl 시작 안내서](https://docs.aws.amazon.com/eks/latest/userguide/getting-started-eksctl.html)에서 확인할 수 있습니다. 이 예제는 macOS를 기반으로 합니다. 샘플 코드, 템플릿 및 기타 리소스는 이 워크숍과 함께 제공되는 [Bitbucket 저장소](https://bitbucket.org/snyk/patterns-library-atlassian-aws)에서 제공됩니다.

### AWS CLI가 설치되었는지 확인

AWS CLI가 올바르게 설치되었는지 확인해 보겠습니다.

```bash
aws --version
```

{% hint style="info" %}
AWS 자격 증명을 설정하려면 `aws configure`를 실행해야 합니다.
{% endhint %}

### Amazon EKS용 공식 CLI인 eksctl 설치

[Homebrew](https://docs.brew.sh/Installation.html)와 함께 `eksctl`을 설치하겠습니다.

```bash
brew tap weaveworks/tap && \
brew update && \
brew install weaveworks/tap/eksctl
```

{% hint style="info" %}
Homebrew와 함께 `eksctl`을 설치하면 `kubectl`명령줄 유틸리티도 설치됩니다.
{% endhint %}

## Installing the Snyk CLI

Snyk CLI는 Snyk 계정으로 시스템을 인증합니다. 이 도구는 수동으로 그리고 지속적 통합 빌드 서버의 일부로 종속성에서 알려진 취약점을 찾고 수정하는 데 도움이 됩니다.

```bash
brew tap snyk/tap && \
brew update && \
brew install snyk
```

Snyk 계정을 CLI와 연결하려면 먼저 시스템을 인증해야 합니다. 이 단계에서는 저장소 권한이 필요하지 않습니다. 다음 명령을 실행하기만 하면 됩니다.

```bash
snyk auth
```

웹 브라우저 탭이 열리고 계정에 사용할 CLI를 인증하도록 리디렉션됩니다. `Authenticatef`를 클릭합니다. 인증이 완료되면 단말기로 돌아가 작업을 계속할 수 있습니다.

## Amazon ECR 리포지토리 생성

Docker 이미지를 Amazon ECR로 푸시하려면 먼저 이미지를 저장할 [리포지토리를 생성](https://docs.aws.amazon.com/AmazonECR/latest/userguide/repository-create.html)해야 합니다. AWS Management Console 또는 AWS CLI 및 AWS SDK를 사용하여 Amazon ECR 리포지토리를 생성할 수 있습니다. 이 워크숍에서는 AWS Management Console을 사용하여 저장소를 생성합니다.

1. [https://console.aws.amazon.com/ecr/repositories](https://console.aws.amazon.com/ecr/repositories) 에서 Amazon ECR 콘솔을 엽니다.
2. 탐색 모음에서 저장소를 생성할 Region을 선택합니다.
3. 탐색 창에서 Repositories를 선택합니다.
4. Repositories 페이지에서 Create Repository를 선택합니다.
5. Repository name에 저장소의 고유한 이름을 입력합니다.
6. 태그 불변성에서 저장소의 태그 가변성 설정을 선택합니다. 변경할 수 없는 태그로 구성된 저장소는 이미지 태그를 덮어쓰는 것을 방지합니다. 자세한 내용은 이미지 태그 변경 가능성을 참조하세요.
7. 푸시 시 스캔에서 저장소의 이미지 스캔 설정을 선택합니다. 푸시할 때 스캔하도록 구성된 저장소는 이미지가 푸시될 때마다 이미지 스캔을 시작합니다. 그렇지 않으면 이미지 스캔을 수동으로 시작해야 합니다. 자세한 내용은 이미지 스캐닝을 참조하십시오.
8. Create repository를를 선택합니다.

## 추가 실습 리소스

이 워크샵에 포함된 연습에는 특정 모듈 페이지 내에서 공유되는 명령 또는 코드 스니펫의 조합과 공용 Bitbucket 저장소에서 사용할 수 있는 템플릿 및 소스 코드가 포함됩니다. Bitbucket Cloud 계정이 설정되면 이러한 리소스를 계정에 복사합니다. 이렇게 하려면 다음 단계를 따르십시오.

### Step 1 - 저장소 포크

`upstream` 저장소를 Bitbucket 계정으로 포크하려면 [여기](https://bitbucket.org/snyk/patterns-library-atlassian-aws/fork)를 클릭하세요. 저장소를 분기하는 방법에 대한 자세한 지침은 Atlassian 설명서를 참조하세요.

### Step 2 - 포크를 로컬로 복제

Once **Step 1** is complete, you will need to `clone` your forked repository. Please review Atlassian's documentation on how to [clone a repository](https://confluence.atlassian.com/bitbucket/clone-a-repository-223217891.html) for detailed instructions.

**Step 1**이 완료되면 분기된 저장소를 복제해야 합니다. 자세한 지침은 [저장소를 복제](https://confluence.atlassian.com/bitbucket/clone-a-repository-223217891.html)하는 방법에 대한 Atlassian 설명서를 참조하세요.
