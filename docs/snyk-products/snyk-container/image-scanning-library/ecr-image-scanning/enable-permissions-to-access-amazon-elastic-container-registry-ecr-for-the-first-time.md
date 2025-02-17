# Amazon ECR에 액세스할 수 있는 권한 활성화

이 프로세스에서는 AWS에서 리소스 역할을 설정하는 방법과 필요한 정책을 설명합니다. 자세한 내용은 [Amazon ECR 설명서](https://docs.aws.amazon.com/AmazonECR/latest/userguide/what-is-ecr.html)를 참조하십시오.

1. AWS Management Console에 로그인하려면 [여기](https://signin.aws.amazon.com/signin?redirect\_uri=https%3A%2F%2Fconsole.aws.amazon.com%2Fiam%2Fhome%3Fstate%3DhashArgs%2523%252Fpolicies%26isauthcode%3Dtrue\&client\_id=arn%3Aaws%3Aiam%3A%3A015428540659%3Auser%2Fiam\&forceMobileApp=0\&code\_challenge=8MHkyBbsvlrprSFBU3Pxe6hD\_Wh55wIbVaGbl7Bgvfc\&code\_challenge\_method=SHA-256)를 클릭하고 로그인 후 IAM 서비스로 이동한 다음 정책 페이지로 이동하여 다음과 같이 JSON 파일을 업데이트하여 정책을 생성하십시오.
   1. 새로운 정책을 생성합니다.
   2. JSON 탭으로 이동합니다.
   3. JSON 파일의 기본 텍스트를 모두 선택하고 삭제합니다.
   4. Snyk 계정의 UI에서 표시되는 스크립트를 복사하여 JSON 파일에 붙여 넣습니다.
   5. 이름을 **AmazonEC2ContainerRegistryReadOnlyForSnyk**으로 설정합니다.
   6. Snyk에게 Amazon EC2 컨테이너 레지스트리 저장소에 대한 읽기 전용 액세스 권한을 제공합니다.
   7. Create Policy를 클릭합니다.
2. 정책을 구현하는 데 사용할 역할을 생성합니다.
   1. [AWS Management Console](https://aws.amazon.com/console/)에서 역할 페이지로 이동하여 새로운 역할을 생성합니다.
   2. AWS 서비스를 신뢰할 수 있는 엔티티로 선택하고 EC2를 이 역할에 대한 서비스로 선택합니다.
   3. Next:permissions를 클릭합니다.
   4. 표시된 정책 목록에서 이전에 생성한 **AmazonEC2ContainerRegistryReadOnlyForSnyk** 정책을 검색하여 선택합니다.
   5. 프로세스의 마지막 단계(Review)로 이동합니다.
   6. 역할 이름을 **SnykServiceRole**로 지정하고 EC2 인스턴스가 사용자 대신 Snyk AWS 서비스를 호출할 수 있도록 허용을 입력한 다음 Create 역할을 입력합니다.
3. 역할에 대한 사용 적합성 범위를 강화합니다.
   1. Roles 페이지에서 이전에 생성한 역할의 링크를 찾아 클릭하여 구성을 업데이트하고 Trust relationships 탭으로 이동합니다.
   2. Edit trust relationship을 클릭합니다.
   3. 정책 문서에서 전체 스크립트를 선택하여 삭제한 다음 Snyk 계정의 UI에 표시되는 다음 스크립트를 복사하여 붙여 넣습니다.

![](../../../../.gitbook/assets/uuid-4b683f44-0a5e-0d13-f369-f7edecf98ce9-en.gif)
