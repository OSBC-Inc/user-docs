# Dockerfile 수정

Snyk 앱에서 각 통합을 확장하고 프로젝트를 전체적으로 볼 수 있는 **Projects** 메뉴로 이동합니다. 여기서는 Amazon ECR 저장소에서 _**container image**_를 선택합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-projects-02.png)

사소한 구성 항목 하나를 완료하라는 메시지가 표시됩니다. **Settings** 탭을 클릭하여 이 문제를 해결해 보겠습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-docker-fix-01.png)

**Configure Dockerfile** 버튼을 클릭하여 진행합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-docker-fix-02.png)

**Bitbucket Cloud**를 소스로 선택합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-docker-fix-03.png)

저장소를 선택하고 **Update Dockerfile**을 클릭합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-docker-fix-04.png)

Dockerfile의 경로로 기본 경로를 업데이트합니다. 이 경우 경로는 `/app/goof/Dockerfile`이거나 아래와 같습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-docker-fix-05.png)

설정이 성공적으로 적용되었다는 확인 메시지를 받게 됩니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-docker-fix-06.png)

기본 이미지 업그레이드에 대한 권장 사항이 제공됩니다. 여기에서 Dockerfile에 정의된 **현재 이미지**와 컨테이너 이미지의 총 취약성 수를 줄이기 위한 **주요 업그레이드** 제안을 확인할 수 있습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-docker-fix-07.png)

이 연습의 목적을 위해 작업을 단순하게 유지하고 Bitbucket의 내장 편집기를 사용하여 변경합니다. Bitbucket 저장소에서 Dockerfile로 이동해 보겠습니다. 경로는 `./app/goof/Dockerfile`입니다. 여기에서 파일을 편집하고 변경 사항을 저장할 수 있습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/bitbucket-edit-dockerfile.png)

다음과 같이 **1행**을 업데이트하겠습니다.

* **OLD VALUE:** `node:6-stretch`
* **NEW VALUE:** `node:12.18-stretch`

**Commit**을 클릭합니다.
