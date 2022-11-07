---
description: Bitbucket Pipeline을 실행하여 자동화된 결과를 확인하고 애플리케이션 배포
---

# Pipeline 작업 활성화

### Bitbucket Pipelines 활성화

기본값이 비활성화된 Pipeline으로 시작하는 경우 저장소에 대해 [Bitbucket Pipelines](../../../getting-started/atlassian-integrations/atlassian-bitbucket-pipeline-variables.md)을 활성화해야 할 수 있습니다.

[Snyk Bitbucket Pipelines Docs](../../../../features/integrations/ci-cd-integrations/bitbucket-pipelines-integration-overview.md) 및 [Snyk Bitbucket Pipelines Video](../../../../features/integrations/ci-cd-integrations/bitbucket-pipelines-integration-overview.md)에는 추가 통합 정보가 포함되어 있으며 Pipeline 작업을 활성화하려면 저장소에 대한 권한이 필요합니다.

Pipeline을 활성화하면 main 또는 master라는 이름의 기본 분기에 중점을 둡니다. 참조 저장소의 루트 디렉터리에는 이미 bitbucket\_pipelines.yaml이 포함되어 있으며 작동하려면 일부 변수를 구성해야 합니다. Pipeline이 활성화되면 변수를 수정할 수 있으며 이에 대해서는 다음 섹션에서 다룹니다.
