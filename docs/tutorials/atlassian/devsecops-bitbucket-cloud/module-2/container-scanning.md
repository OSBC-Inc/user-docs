# Container Scanning

## 배경

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-container-01.png)

### SDLC\*의 다양한 단계에서 취약점 테스트

테스트 구현을 위한 몇 가지 전략이 있습니다. 다음 차트는 이에 대한 유용한 요약을 제공합니다. 이 워크숍의 예는 아래에 제시된 두 가지 예에 초점을 맞출 것입니다.

| Stage          | 설명                                                                                                                                     | 비용 | 피드백 | Completeness |
| -------------- | -------------------------------------------------------------------------------------------------------------------------------------- | -- | --- | ------------ |
| Local          | 디버깅 및 개발자 간의 지식 구축에 적합하지만 개별 개발자 작업이 필요하며 시행할 방법이 없습니다.                                                                                | 중간 | 빠름  | Low          |
| CI/CD\*\*      | 관문으로서 훌륭하고 개발자를 위한 빠른 피드백은 조직에서 파이프라인 관리가 표준화된 방식에 따라 달라지는 파이프라인별 구현이 필요합니다. 빌드를 손상시키는 낮은 심각도 문제에 대해 생산성이 저하될 수 있으므로 다른 피드백 주기도 필요합니다. | 중간 | 빠름  | Variable     |
| Registry\*\*\* | 단일 소유자인 경우가 많기 때문에 빌드 방법에 관계없이 모든 자사 이미지를 쉽게 통합하고 처리할 수 있습니다. 이미지가 사용되지 않을 수 있으므로 노이즈가 발생할 수 있습니다.                                     | 낮음 | 중간  | Medium       |
| Production     | 타사 콘텐츠를 포함하여 실행 중인 항목에 대한 정확한 그림이지만 개발 팀에 대한 잠재적인 느린 피드백 주기 및 위험 취약성은 실행 중인 애플리케이션에서 악용될 수 있습니다.                                       | 높음 | 느림  | High         |

**Application Scanning**에 대한 이전 모듈과 유사하게 이 모듈에서는 [bitbucket-pipelines.yml](https://bitbucket.org/snyk/patterns-library-atlassian-aws/src/192a4d2412a4330b9f634e9d45a546ec1add61fb/bitbucket-pipelines.yml#lines-32:56) 파일을 구성하여 애플리케이션용 Docker 이미지를 빌드하고 이미지를 스캔한 다음 해당 이미지를 레지스트리에 푸시합니다. 컨테이너 이미지 스캔 단계를 자세히 살펴보겠습니다.

```yaml
scan-push-image: &scan-push-image
  - step:
      name: "Scan and push container image"
      services:
        - docker
      script:
        - docker build -t $IMAGE ./app/goof/
        - docker tag $IMAGE $IMAGE:${BITBUCKET_COMMIT}
        - pipe: snyk/snyk-scan:0.4.3
          variables:
            SNYK_TOKEN: $SNYK_TOKEN
            LANGUAGE: "docker"
            IMAGE_NAME: $IMAGE
            PROJECT_FOLDER: "app/goof"
            TARGET_FILE: "Dockerfile"
            CODE_INSIGHTS_RESULTS: "true"
            SEVERITY_THRESHOLD: "high"
            DONT_BREAK_BUILD: "true"
            MONITOR: "false"
        - pipe: atlassian/aws-ecr-push-image:1.1.3
          variables:
            AWS_ACCESS_KEY_ID: '$AWS_ACCESS_KEY_ID'
            AWS_SECRET_ACCESS_KEY: '$AWS_SECRET_ACCESS_KEY'
            AWS_DEFAULT_REGION: '$AWS_DEFAULT_REGION'
            IMAGE_NAME: $IMAGE
            TAGS: '${BITBUCKET_COMMIT}'
```

여기에서는 컨테이너 이미지를 빌드하고 태그를 지정한 다음 파이프라인에서 [Snyk Scan](https://bitbucket.org/product/features/pipelines/integrations?p=snyk/snyk-scan) 파이프를 활용하여 컨테이너 이미지 스캔을 수행합니다. `CODE_INSIGHTS_RESULTS`, `SEVERITY_THRESHOLD` 및 `DONT_BREAK_BUILD`에 대해 동일한 값을 유지합니다. 또한 애플리케이션 스캔 대신 컨테이너 이미지 스캔을 요청하고 있음을 이해하기 위해 Snyk Pipe와 관련된 몇 가지 추가 [지원 변수](https://bitbucket.org/snyk/snyk-scan)를 전달하고 있습니다. 즉, `LANGUAGE`를 `docker`로 설정하고, `IMAGE_NAME`을 선언하고, 적절한 리포지토리 변수를 전달하고, `TARGET_FILE`을 `Dockerfile`로 설정합니다. Snyk에서 이미지를 스캔하고 Code Insights에서 결과를 사용할 수 있게 되면 Amazon ECR [푸시 이미지 파이프](https://bitbucket.org/atlassian/aws-ecr-push-image)를 호출하여 리포지토리로 푸시합니다.

**각주:**

1. **\*Snyk Blog -** [SDLC의 여러 단계에서 취약점 테스트](https://snyk.io/blog/container-security-throughout-the-sdlc/)
2. **\*\***Bitbucket 파이프라인 예제에서는 이 단계에 중점을 둘 것입니다.
3. **\*\*\***Amazon ECR 예제에 대한 Snyk 통합에서 이 단계에 중점을 둘 것입니다.
