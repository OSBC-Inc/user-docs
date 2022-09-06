# AWS CLI

## AWS CLI (AWS Command Line) 인터페이스 설치

이러한 연습에는 [AWS CLI (AWS Command Line Interface)](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-welcome.html)와 `kubectl` 및 `eksctl`을 사용합니다. AWS CLI 설치에 대한 자세한 설명서는 [AWS 설명서](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html)와 Linux 및 Windows의 설치 단계를 자세히 설명하는 [eksctl 시작하기 가이드](https://docs.aws.amazon.com/eks/latest/userguide/getting-started-eksctl.html)에서 확인할 수 있습니다. 이러한 예제는 macOS를 기반으로 합니다. 샘플 코드, 템플릿 및 기타 리소스는 이 워크샵과 함께 제공되는 [Bitbucket 저장소](https://bitbucket.org/snyk/patterns-library-atlassian-aws)에서 제공됩니다.

### AWS CLI가 설치되었는지 확인

아래 명령어를 통해 AWS CLI가 올바르게 설치되었는지 확인합니다.

```bash
aws --version
```

{% hint style="info" %}
AWS 인증 정보를 설정하려면 `aws configure`를 실행해야 합니다.
{% endhint %}

##
