# CI/CD 파이프라인

## GitHub Actions 파이프라인 시작하기

SDLC의 각 단계는 애플리케이션을 운영 환경에 가깝게 이동하며 이러한 단계는 애플리케이션의 취약점과 라이선스 컴플라이언스를 평가하고 평가할 수 있는 또 다른 기회를 나타냅니다. Snyk provides numerous integration points along the SDLC to enforce security gates. A security gate is an organizational policy to help AppSec teams assess the risks of releasing code to production. In the exercise below, we will review the GitHub Actions pipeline and examine how to apply the security gates to your pipeline. When the pipeline executes it will send Synk test results to the Snyk UI, we will review the results in further exercises.

GitHub workflow diagram:

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/github\_workflow\_diagram\_56-.png)

### Workshop exercises

We will complete the following steps.

1. Populate the pipeline with GitHub secrets. We will add a Synk API token and Docker Hub API token.
2. Edit pipeline environment variables to build or container image, commit changes to the pipeline, and execute the pipeline.
