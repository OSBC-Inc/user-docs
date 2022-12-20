# 환경 변수 구성 및 변경 사항 Commit

## 레지스트리를 지원하도록 환경 변수 변경

SPC 인터페이스에서 github/workflow 폴더와 main.yml 파일을 선택합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/env\_var\_change.png)

워크플로 상단의 환경 변수를 Docker Hub 레지스트리/사용자 ID로 업데이트합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/screen-shot-2020-08-25-at-3.35.08-pm.png)

변경 사항 Commit 및 GitHub 작업 워크플로 유효성 검사가 시작되었습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/actions\_running\_purple\_circle.png)

{% hint style="info" %}
이 파이프라인은 SPC를 빌드하고 테스트하므로 실행하는 데 약 5분이 걸립니다.
{% endhint %}
