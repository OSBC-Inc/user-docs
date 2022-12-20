---
description: Bitbucket에 코드 가져오기
---

# Bitbucket 저장소 추가

### 저장소 가져오기

Bitbucket 환경으로 리포지토리를 가져오는 것부터 시작하겠습니다. 이것은 모든 워크샵 사용자를 위한 공통 시작 위치를 설정합니다. 참조 리포지토리에는 Goof라는 인기 있는 Snyk 샘플 애플리케이션 라인을 모델로 한 의도적으로 취약한 애플리케이션이 포함되어 있습니다. 우리 워크샵에서 구현은 Java로 이루어지며 저장소는 적절한 이름으로 java-goof입니다. java-goof 저장소도 매개변수화되어 실행 환경에 더 쉽게 추가할 수 있습니다.

소스 리포지토리는 다음 위치에서 공개적으로 사용할 수 있습니다:

{% embed url="https://github.com/snyk-labs/java-goof" %}

Bitbucket에서 작업 공간으로 이동하고 저장소를 가져오면 저장소 보기에서 "저장소 만들기" 버튼을 클릭하여 자유롭게 변경할 수 있습니다.

![](<../../../../.gitbook/assets/image (93).png>)

다음으로 작업 공간 및 기타 세부 정보를 선택하는 화면이 표시됩니다. 이 화면에서 **Import repository** 링크를 클릭합니다.

![](<../../../../.gitbook/assets/image (91) (1).png>)

새 화면에서 이전 저장소의 URL을 묻습니다. 해당 필드에 [https://github.com/snyk-labs/java-goof](https://github.com/snyk-labs/java-goof)를 입력하고 Workspace 및 Project를 선택합니다. 외부 저장소에는 인증이 필요하지 않으며 개인 또는 공개 액세스 수준을 선택합니다. 원하는 경우 저장소의 이름을 바꿉니다.

![](<../../../../.gitbook/assets/image (67).png>)

**Import repository**를 클릭하여 프로세스를 완료합니다.

다음 단계는 Snyk과 Bitbucket 간의 통합을 활성화하는 것입니다.
