# Amazon Elastic Container Registry (ECR): Snyk과 함께 통합 구성

IAM 역할을 생성하거나 업데이트 한 후에는 진행하기 전에 AWS가 서버에서 역할을 업데이트할 때까지 몇 분 정도 대기하십시오.

1. AWS에서 Summary 섹션 상단에 나타나는**Role ARN**키를 복사합니다(**Role** 영역 내부).
2. Snyk 계정에 로그인합니다.
3. 상단의 메뉴 모음에서 **Integrations**로 이동하여 Amazon ECR 옵션을 찾아 클릭합니다.
4. 설정 영역의 Amazon ECR 구성 페이지가 로드됩니다.
5. 다음과 같이 인증 정보를 입력하십시오.
   1. **AWS Region**—region-part-# 형식을 사용합니다. eu-west-3으로 예를 들면, 저장소 및 이미지를 가져올 수 있으려면 AWS 계정에 구성된 기본 영역을 입력해야 합니다.
   2. **Role ARN**—`arn:aws:iam:::role/` 형식으로 AWS 계정에서 복사합니다.
6. **Save**를 클릭합니다.

다음은 예시입니다.

```
   arn:aws:iam::881001789406:role/TestSnykIntegration_role
```

Snyk은 연결 값과 페이지 다시 로드를 테스트하여 입력한 Amazon ECR 통합 세부 정보를 표시합니다. 세부 정보가 저장되었다는 확인 메시지도 화면 상단에 녹색으로 표시됩니다.

![](../../../../.gitbook/assets/uuid-49671392-b5d5-389d-66c8-86b3daf9a2e1-en.png)

또한 AWS에 연결하지 못한 경우 **Connected to Amazon ECR**에 알림이 나타납니다.
