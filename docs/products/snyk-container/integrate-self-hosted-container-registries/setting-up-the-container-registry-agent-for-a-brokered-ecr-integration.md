# 중개 ECR 통합을 위한 Container Registry Agent 설정

## 소개

### 용어 사전

**Container Registry Agent IAM Role / IAM User:** Container Registry Agent가 ECR에 대한 액세스 권한이 있는 역할을 맡는 데 사용하는 IAM Role / IAM User입니다.

**Snyk ECR Service Role:** ECR에 대한 액세스 권한이 있는 IAM Role이며 Container Registry Agent의 “IAM Role” / “IAM User”를 사용하여 ECR에 대한 읽기 전용 액세스 권한을 얻습니다.

### 단계 요약

다음 단계를 통해 단일 Container Registry Agent 인스턴스가 다른 계정에 있는 ECR 저장소에 액세스할 수 있습니다.

1. **(**이 단계는 한 번만 실행**)** 역할을 맡을 권한이 있는 Container Registry Agent IAM Role / IAM　User를 생성합니다. IAM Role / IAM User를 사용하여 Container Registry Agent를 실행합니다. **각 ECR 계정에 대해 별도의 broker 인스턴스를 사용하여 각 계정에 대해 다음 단계를 실행합니다.**
2. ECR이 있는 AWS 계정에서 ECR에 대한 읽기 액세스 권한을 가진 Snyk ECR Service Role을 만들고 이 역할은 이전 단계에서 만든 특정 Container Registry Agent IAM Role / IAM User만 이 역할을 맡도록 제한합니다.
3. Container Registry Agent IAM Role / IAM User가 Snyk ECR Service Role(s)만 맡을 수 있도록 제한합니다.
4. Broker Client에 Snyk ECR Service Role의 Role ARN을 제공합니다. Broker Client는 이 Role ARN을 Container Registry Agent로 전달하고 Container Registry Agent는 ECR에 액세스하기 위해 이를 맡습니다.

### 아키텍처

다음 이미지는 중개된 ECR 솔루션의 아키텍처를 설명합니다.

![중개된 ECR 아키텍처](../../../.gitbook/assets/ecr-arch.png)

## 1단계: IAM User / IAM Role로 Container Registry Agent 실행

이 단계에서는 Container Registry Agent에서 사용할 IAM Role / IAM User를 생성합니다. IAM Role / IAM User는 [여기](https://docs.aws.amazon.com/sdk-for-javascript/v2/developer-guide/setting-credentials-node.html)에 설명된 방법을 통해 Container Registry Agent에 제공될 수 있습니다.

다음 예에서는 다음 방법 중 하나를 사용하여 IAM Role / IAM User를 제공하는 방법을 설명합니다.

* **예 a:** 전용 EC2 role을 생성하고 AWS IAM(Identity and Access Management) Role의 자격 증명을 Container Registry Agent 이미지를 실행하는 EC2 인스턴스로 로드합니다.
* **예 b:** 전용 사용자를 만들고 환경 변수를 통해 자격 증명을 제공합니다.

**참고:** Amazon ECS 작업에서 전용 역할을 제공할 수도 있습니다. 자세한 내용은 [여기](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/task-iam-roles.html)를 참조하십시오.

### 예 **a:** Amazon EC2에 대한 전용 EC2 Service Role을 생성하고 AWS IAM(Identify and Access Management) Role에서 자격 증명을 로드합니다.

#### 1단계: Role 생성

1. IAM 서비스로 AWS Management Console에 로그인하고 **Roles** 페이지로 이동하려면 [여기](https://console.aws.amazon.com/iam/home?#/policies)를 클릭하십시오.
2. **create a role**을 선택합니다.
3. **type of trusted entity**으로 **AWS service**를 선택합니다.
4. **use case**로 **EC2**를 선택합니다.
5. 권한 및 태그를 사용하여 다음으로 이동합니다.
6. role 이름을 검토하고 제공합니다. **SnykCraEc2Role**.
7. role을 만듭니다.
8. role의 **Summary** 페이지에서 **Instance Profile ARN** (예: arn:aws:iam::\<aws-account>:instance-profile/SnykCraEc2Role) 및 Role ARN (예: arn:aws:iam::\<aws-account>:role/SnykCraEc2Role) 을 나중에 사용할 수 있습니다.

#### 2단계: EC2 role이 다른 역할을 맡도록 허용하는 정책 생성

1. 새로 생성된 role 페이지의 **Permissions** 탭에서 **Inline policy**를 생성합니다.
2. **Service**에서 **STS**를 선택합니다.
3. **Actions**에서 **Write → AssumeRole**을 선택합니다.
4. **Resources**에서 **All resources**를 선택합니다. (마지막 단계에서 리소스를 강화합니다).
5.  **JSON** 탭에서 정책에 다음이 포함되어 있는지 확인합니다.

    ```
    {
      "Version": "2012-10-17",
      "Statement": [
        {
          "Sid": "SnykCraAssumeRolePolicy",
          "Effect": "Allow",
          "Action": "sts:AssumeRole",
          "Resource": "*"
        }
      ]
    }
    ```
6. 정책을 검토하고 정책 이름을 제공합니다. **SnykCraAssumeRolePolicy**.
7. 정책 생성을 선택합니다.

#### 3단계: Container Registry Agent를 실행하는 EC2 시스템에 role 연결

1. **EC2 Management Console**로 이동하여 Container Registry Agent 컨테이너를 실행하는 인스턴스를 선택합니다.
2. **Actions → Security → Modify IAM Role**을 클릭합니다.
3. **IAM role** 드롭다운 목록의 첫 번째 단계에서 생성된 IAM role의 인스턴스 프로필(예: arn:aws:iam::\<aws-account>:instance-profile/SnykCraEc2Role)을 선택하고 **Save**를 클릭합니다.

EC2 시스템에서 Container Registry Agent 이미지를 실행할 때 연결된 role의 자격 증명은 실행중인 Container Registry Agent에 의해 자동으로 선택됩니다. 따라서 추가 단계가 필요하지 않습니다. 자세한 내용은 [Amazon docs](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/iam-roles-for-amazon-ec2.html#instance-metadata-security-credentials)에서 확인할 수 있습니다.

### 예 b: 전용 사용자 생성 및 환경 변수를 통해 자격 증명 제공

#### 1단계: 사용자 생성

1. IAM 서비스로 AWS Management Console에 로그인하고 **Users** 페이지로 이동하려면 [여기](https://console.aws.amazon.com/iam/home?#/policies)를 클릭하십시오.
2. **Add users**를 클릭합니다.
3. 사용자 이름 입력: **SnykCraUser**.
4. **Access type**으로 **Programmatic access**를 선택합니다.
5. 권한 및 태그를 사용하여 다음으로 이동합니다.
6. 사용자를 검토하고 생성합니다.
7. 사용자가 생성되면 나중에 사용할 수 있도록 인증 정보(액세스 키 ID 및 비밀 액세스 키)를 저장합니다.
8. 사용자의 **Summary** 페이지에서 나중에 사용할 수 있도록 **User ARN**을 복사합니다(예: arn:aws:iam::\<aws-account>:user/SnykCraUser)

#### 2단계: 사용자가 역할을 맡도록 허용하는 정책 생성

1. 새로 생성된 사용자 페이지의 **Permissions** 탭에서 **Inline policy**를 생성합니다.
2. **Service**에서 **STS**를 선택합니다.
3. **Actions**에서 **Write→AssumeRole**을 선택합니다.
4. **Resources**에서 **All resources**를 선택합니다.(마지막 단계에서 리소스를 강화합니다.
5.  **JSON** 탭에서 정책에 다음 명령문이 포함되어 있는지 확인합니다.

    ```
    {
      "Version": "2012-10-17",
      "Statement": [
        {
          "Sid": "SnykCraAssumeRolePolicy",
          "Effect": "Allow",
          "Action": "sts:AssumeRole",
          "Resource": "*"
        }
      ]
    }
    ```
6. 정책을 검토하고 정책 이름을 제공합니다. **SnykCraAssumeRolePolicy**.
7. 정책 생성을 선택합니다.

#### 3단계: Container Registry Agent를 실행할 때 인증 정보 사용

Container Registry Agent 이미지를 실행할 때 다음과 같은 환경 변수를 설정하여 인증 정보를 제공할 수 있습니다.

* AWS\_ACCESS\_KEY\_ID=<사용자 액세스 키 ID>
* AWS\_SECRET\_ACCESS\_KEY=<사용자 보안 액세스 키>

## 2단계: Snyk ECR Service Role을 만들고 ECR에 대한 계정 간 액세스 활성화

이 단계에서는 ECR 저장소가 있는 계정에 Role을 만듭니다. 이 Role은 저장소에 대한 읽기 전용 액세스를 허용하며, 이전 단계에서 만든 Role을 맡을 수도 있습니다.

### **1.** Snyk ECR Service Role이 사용할 읽기 전용 ECR 정책 생성

1. IAM 서비스를 사용하여 AWS Management Console에 로그인하고 **Policies** 페이지로 이동하려면 [여기](https://console.aws.amazon.com/iam/home?#/policies)를 클릭하십시오.
2. 새로운 정책을 생성합니다.
3. JSON 데이터 편집을 선택합니다.
4.  기본 데이터를 삭제하고 대신 다음을 복사하여 붙여넣습니다.

    ```
    {
      "Version":"2012-10-17",
      "Statement": [
        {
          "Sid":"SnykAllowPull",
          "Effect":"Allow",
          "Action": [
            "ecr:GetLifecyclePolicyPreview",
            "ecr:GetDownloadUrlForLayer",
            "ecr:BatchGetImage",
            "ecr:DescribeImages",
            "ecr:GetAuthorizationToken",
            "ecr:DescribeRepositories",
            "ecr:ListTagsForResource",
            "ecr:ListImages",
            "ecr:BatchCheckLayerAvailability",
            "ecr:GetRepositoryPolicy",
            "ecr:GetLifecyclePolicy"
          ],
          "Resource":"*"
        }
      ]
    }
    ```
5. 정책 검토를 선택합니다.
6. **Name**으로**AmazonEC2ContainerRegistryReadOnlyForSnyk** 을 설정합니다.
7. **description**으로 **"Provides Container Registry Agent with read-only access to Amazon EC2 Container Registry repositories"**을 설정합니다.
8. 정책 생성을 선택합니다.

### 2. 정책을 구현할 Snyk ECR Service Role을 생성

1. AWS Management Console에서 다시 **Roles** 페이지로 이동합니다. [여기](https://console.aws.amazon.com/iam/home?#/roles)를 클릭하여 이동할 수 있습니다.
2. 새로운 role을 생성합니다.
3. Select **AWS service** as the trusted entity and **EC2** as the service for this role.
4. Choose to go next with permission.
5. Check the policy **AmazonEC2ContainerRegistryReadOnlyForSnyk** from the list.
6. Choose to go next with tags and review.
7. Set **SnykEcrServiceRole** as the Name.
8. Set **"Allows EC2 instances to call ECR AWS services on your behalf"** as the Description.

### 3. Snyk ECR Service Role의 사용성 범위 강화

This step will harden the usability of the Snyk ECR Service Role so that it could only be assumed by the Container Registry Agent IAM Role / IAM Role.

1. Again from the **Roles** page, find and click the [SnykEcrServiceRole](https://console.aws.amazon.com/iam/home?#/roles/SnykEcrServiceRole) to enter the role configurations.
2. Select the **Trust relationships** tab.
3. Edit the trust relationship.
4.  Delete all of the data and replace it with the following JSON:

    ```
    {
      "Version":"2012-10-17",
      "Statement": [
        {
          "Effect":"Allow",
          "Principal":{
            "AWS":"<ARN of Container Registry Agent IAM User / IAM Role>"
          },
          "Action":"sts:AssumeRole",
          "Condition":{
            "StringEquals": {
              "sts:ExternalId":"<optional external ID>"
            }
          }
        }
      ]
    }
    ```

    * In **Statement.Principal.AWS** enter the IAM Role / IAM User created in the Step 1 (e.g. arn:aws:iam::\<aws-account>:user/SnykCraEc2Role or arn:aws:iam::\<aws-account>:role/SnykCraUser, respectively)
    * In **Condition.StringEquals.sts:ExternalId** you may use an external ID of your choice, which will be used when providing the credentials object to the Broker Client.
    * To support multiple external IDs, enter a list of IDs in a square brackets. For example: _\*\*_`"sts:ExternalId": [ "11111111-1111-1111-1111-111111111111", "22222222-2222-2222-2222-222222222222" ]`
5. Update the trust policy.

## 3단계: Container Registry Agent에서 사용하는 IAM Role / IAM User의 사용성 범위 강화

This step will harden the usability of the IAM Role / IAM User used by the Container Registry Agent so that it could only assume the[ SnykEcrServiceRole](https://console.aws.amazon.com/iam/home?#/roles/SnykEcrServiceRole).

1. Copy the Role ARN key that appears at the top of the **Summary** section of the[ SnykEcrServiceRole](https://console.aws.amazon.com/iam/home?#/roles/SnykEcrServiceRole).
2. In the AWS account where the IAM Role / IAM User was created for running the Container Registry Agent, edit the **SnykCraAssumeRolePolicy**: 1. In case an IAM Role was created: 1. Go to **Roles** and choose the **SnykCraEc2Role** role. 2. In the **SnykCraAssumeRolePolicy** choose to edit the JSON. 3. Add the role ARN of[ SnykEcrServiceRole](https://console.aws.amazon.com/iam/home?#/roles/SnykEcrServiceRole) as the resource: `"Resource": "<Role ARN of SnykEcrServiceRole>"` 2. In case an IAM User was created:
   1. Go to **Users** and choose the SnykCraUser user.
   2. In the **SnykCraAssumeRolePolicy** choose to edit the JSON
   3.  Add the role ARN of[ SnykEcrServiceRole](https://console.aws.amazon.com/iam/home?#/roles/SnykEcrServiceRole) as the resource: `"Resource": "<Role ARN of SnykEcrServiceRole>"`

       \*\*\*\*

**Note:** in case the Container Registry Agent needs to access multiple ECR registries found in different accounts, a separate item will need to be added to the Statement list, so that each ECR account has a separate statement. For example:

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "SnykCraAssumeRolePolicyAccountA",
      "Effect": "Allow",
      "Action": "sts:AssumeRole",
      "Resource": "<Role ARN of SnykEcrServiceRole of account A>"
    },
    {
      "Sid": "SnykCraAssumeRolePolicyAccountB",
      "Effect": "Allow",
      "Action": "sts:AssumeRole",
      "Resource": "<Role ARN of SnykEcrServiceRole of account B>"
    },
  ]
}
```

## 4단계: Broker Client에 Snyk ECR Service Role ARN 및 외부 ID 제공

In the last step, the Role ARN of the SnykEcrServiceRole \_\*\*\_will be used by providing it to the broker client. The broker client will pass it to the Container Registry Agent, which will assume it to connect to ECR.

1. Copy the **Role ARN** key that appears at the top of the **Summary** section of the[ SnykEcrServiceRole](https://console.aws.amazon.com/iam/home?#/roles/SnykEcrServiceRole).
2. When running the Broker Client, provide the following environment variables the allow the Container Registry Agent to access your ECR account (note that no username/password are needed):
   * CR\_TYPE=ecr
   * CR\_ROLE\_ARN=\<the role ARN of SnykEcrServiceRole>
   * CR\_REGION=\<AWS Region of ECR>
   * CR\_EXTERNAL\_ID=\<Optional. The external ID found in the trust relationship condition>
