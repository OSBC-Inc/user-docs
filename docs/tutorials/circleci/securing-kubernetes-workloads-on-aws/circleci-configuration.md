# CircleCI 구성

아직 이 워크숍과 연결된 저장소의 [fork](https://github.com/snyk-partners/snyk-circleci-eks/fork)가 없다면 지금 수행해야 합니다. 이 Git 리포지토리의 콘텐츠에는 `.circleci/config.yml` 파일이 포함됩니다. `config.yml` 파일에서 사용되는 CircleCI 2.x 구성 키에 대한 포괄적인 참조 문서는 [CircleCI](https://circleci.com/docs/2.0/configuration-reference/)에서 사용할 수 있습니다. 샘플 `config.yml` 파일의 연습에서 일부 구성 키를 참조합니다.

## 환경 변수

이 연습에 표시된 예제 전체에서 몇 가지 환경 변수에 대한 참조를 볼 수 있습니다. 이들은 [CircleCI 프로젝트 설정](https://circleci.com/docs/2.0/env-vars/?utm\_medium=SEM\&utm\_source=gnb\&utm\_campaign=SEM-gb-DSA-Eng-ni\&utm\_content=\&utm\_term=dynamicSearch-\&gclid=EAIaIQobChMI\_LT0qqj16QIVUB-tBh0J-gxoEAAYASAAEgJdxfD\_BwE#setting-an-environment-variable-in-a-project)에서 정의되며 CircleCI, AWS 및 Snyk 간의 보안 인증을 허용하기 위해 `config.yml`에서 참조됩니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/circleci\_project\_settings.png)

필요한 특정 변수는 다음과 같습니다:

1. AWS Identity & Access Management User [key and secret](https://docs.aws.amazon.com/IAM/latest/UserGuide/id\_credentials\_access-keys.html) for secure authenticated interactions with the AWS API: `ACCESS_KEY_ID_ENV_VAR_NAME` & `SECRET_ACCESS_KEY_ENV_VAR_NAME`
2. AWS API와의 안전한 인증 상호 작용을 위한 AWS Identity & Access Management 사용자 키 및 암호: ACCESS\_KEY\_ID\_ENV\_VAR\_NAME 및 SECRET\_ACCESS\_KEY\_ENV\_VAR\_NAME
3. [AWS Elastic Container Registry (ECR) URL](https://docs.aws.amazon.com/AmazonECR/latest/userguide/Registries.html) for accessing your default registry: (SEE WARNING BELOW) `AWS_ECR_ACCOUNT_URL_ENV_VAR_NAME`
4. AWS region you will be deploying to: AWS\_REGION\_ENV\_VAR\_NAME
5. API token for authenticating with your Snyk account: `SNYK_TOKEN`

{% hint style="warning" %}
Ensure that you use the general ECR URL in the following format:

`https://aws_account_id.dkr.ecr.region.amazonaws.com`
{% endhint %}

{% hint style="warning" %}
It is recommended that you use [Snyk Service accounts](https://support.snyk.io/hc/en-us/articles/360004037597-Service-accounts) and [AWS IAM best practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html) when creating accounts.
{% endhint %}
