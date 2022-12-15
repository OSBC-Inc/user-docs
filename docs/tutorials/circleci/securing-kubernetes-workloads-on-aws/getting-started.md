# 시작 하기

이 연습에서는 [AWS CLI (AWS Command Line Interface)](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-welcome.html)와 `kubectl` 및 `eksctl`을 사용합니다. AWS CLI 설치에 대한 자세한 설명서는 [AWS 설명서](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html)와 Linux 및 Windows용 설치 단계를 자세히 설명하는 [`eksctl` 시작 안내서](https://docs.aws.amazon.com/eks/latest/userguide/getting-started-eksctl.html)에서 확인할 수 있습니다. 이 예제는 macOS를 기반으로 합니다. 샘플 코드, 템플릿 및 기타 리소스는 이 워크숍과 함께 제공되는 [Git 저장소](https://github.com/snyk-partners/snyk-circleci-eks)에서 제공됩니다. 이 연습 전체에서 해당 콘텐츠를 참조하므로 이 저장소를 [`clone`](https://github.com/snyk-partners/snyk-circleci-eks.git)하거나 [fork](https://github.com/snyk-partners/snyk-circleci-eks/fork)하는 것이 좋습니다.

## 로컬 환경 구성

터미널에서 AWS CLI가 설치되었는지 확인하겠습니다:

```bash
aws --version
```

{% hint style="danger" %}
잠깐! AWS CLI 자격 증명을 구성하려면 [`aws configure`](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-configure.html)를 실행해야 합니다.
{% endhint %}

### Homebrew 설치

아직 없는 경우 Homebrew를 설치한 다음 `eksctl`을 설치합니다.

```bash
brew tap weaveworks/tap && \
brew update && \
brew install weaveworks/tap/eksctl
```

{% hint style="info" %}
Homebrew와 함께 `eksctl`을 설치하면 `kubectl` 명령줄 유틸리티도 설치됩니다.
{% endhint %}

이제 설치가 잘 되었는지 확인해보겠습니다.

```bash
eksctl version
```

이제 Amazon EKS 클러스터 및 작업자 노드를 생성할 준비가 되었습니다!
