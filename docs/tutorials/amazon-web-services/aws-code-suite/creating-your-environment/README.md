# 환경 구축하기

{% hint style="danger" %}
You are responsible for the cost of the AWS services used while running this workshop in your AWS account.
{% endhint %}

이 워크숍에서 성공하려면 환경을 올바르게 설정하고 구성하기 위해 몇 가지 단계를 거쳐야 합니다. 이러한 단계에는 일부 서비스 프로비저닝, 일부 도구 설치 및 일부 종속성 다운로드가 포함됩니다. [AWS Cloud9](https://aws.amazon.com/cloud9/)부터 시작하겠습니다. 기술적으로 터미널을 올바르게 구성한 경우 이러한 모듈의 많은 단계를 완료할 수 있어야 합니다. 그러나 경력의 어느 시점에서 분명히 경험한 "works on my machine" 응답을 피하기 위해 Cloud9 출시를 계속 진행할 것을 강력히 권장합니다.

[AWS Cloud9](https://aws.amazon.com/cloud9/)은 브라우저만으로 코드를 작성, 실행 및 디버그할 수 있는 클라우드 기반 통합 개발 환경(IDE)입니다. 여기에는 코드 편집기, 디버거 및 터미널이 포함됩니다. Cloud9에는 JavaScript, Python, PHP 등을 포함하여 널리 사용되는 프로그래밍 언어를 위한 필수 도구가 사전 패키징되어 있으므로 새 프로젝트를 시작하기 위해 파일을 설치하거나 개발 시스템을 구성할 필요가 없습니다.

## AWS Cloud9 배포 및 시작

[CloudFormation 템플릿을 사용하여 배포하려면 여기를 클릭하십시오.](https://console.aws.amazon.com/cloudformation/home?region=us-west-2#/stacks/new?stackName=ModernizationWorkshop\&templateURL=https://modernization-workshop-west-2.s3-us-west-2.amazonaws.com/devops/cfn/modernization-workshop.yaml)

* Create stack을 클릭 합니다.
* 스택 세부 정보를 지정하고 **Next**를 클릭합니다.
* 스택 옵션을 구성하고 **Next**를 클릭합니다.
* UnicornDevSecOpsWorkshop을 검토하고 **Capabilities** 아래 섹션으로 스크롤한 다음 두 상자를 모두 선택하고 **Create stack**을 클릭합니다.

> 배포 프로세스를 완료하는 데 약 2-3분이 걸립니다. 그 동안 기다리는 동안 [배포 가이드](https://aws-quickstart.s3.amazonaws.com/quickstart-cloud9-ide/doc/aws-cloud9-cloud-based-ide.pdf)를 검토할 수 있습니다.

설치가 완료되면 콘솔 내 Cloud9으로 이동하여 WorkshopIDE로 시작하는 이름에서 **Open IDE**를 클릭합니다.

## 이 워크샵의 소스 저장소  복제

이제 이 워크샵을 완료하는 데 필요한 모든 콘텐츠와 파일이 포함된 저장소를 복제하려고 합니다.

```bash
cd ~/environment && \
git clone https://github.com/jamesbland123/workshop-sample modernization-workshop
cd modernization-workshop
git submodule init
git submodule update
```

## AWS Cloud9 디스크/스토리지 늘리기

```bash
cd ~/environment/modernization-workshop/modules/20_getting_started
./resize.sh 50
```

## 일부 도구 업데이트 및 설치

이 단계에서는 워크샵을 완료하는 데 필요한 다양한 도구를 업데이트하고 설치합니다. 무엇이 업데이트되고 설치되는지 궁금하다면 자유롭게 스크립트를 살펴보십시오.

```bash
./getting_started.sh
```

다음으로 소스 .bashrc가 현재 작업 환경에 .net PATH를 추가하도록 합니다.

```bash
. ~/.bashrc
```
