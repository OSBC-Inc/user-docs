# CI/CD 파이프라인

## GitHub Actions 파이프라인 시작하기

SDLC의 각 단계는 애플리케이션을 운영 환경에 가깝게 이동하며 이러한 단계는 애플리케이션의 취약점과 라이선스 컴플라이언스를 평가하고 평가할 수 있는 또 다른 기회를 나타냅니다. Snyk은 보안 게이트를 시행하기 위해 SDLC를 따라 수많은 통합 지점을 제공합니다. 보안 게이트는 AppSec 팀이 프로덕션에 코드를 릴리스할 때의 위험을 평가하는 데 도움이 되는 조직 정책입니다. 아래에서는 GitHub Actions 파이프라인을 검토하고 보안 게이트를 파이프라인에 적용하는 방법을 검토합니다. 파이프라인이 실행되면 Snyk test 결과를 Snyk UI로 전송합니다.

GitHub 워크플로우 다이어그램:

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/github\_workflow\_diagram\_56-.png)

### Workshop 실행

다음 단계를 완료합니다.

1. Populate the pipeline with GitHub secrets. We will add a Synk API token and Docker Hub API token.
2. Edit pipeline environment variables to build or container image, commit changes to the pipeline, and execute the pipeline.
