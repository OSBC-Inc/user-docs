# Section 2: Container 스캔 결과 살펴보기

저장소에는 이제 Goof를 컨테이너로 패키징하는 데 필요한 모든 파일이 있습니다. 또한 Snyk Container 스캔을 Workflow에 도입하여 애플리케이션을 컨테이너에 패키징하기로 결정함으로써 코드베이스에 도입된 문제를 식별하는 데 도움을 주었습니다. 조치를 취하기 전에 스캔 결과를 자세히 살펴보겠습니다.

## Step 1: GitHub에서 Container Scan 결과 검토

### GitHub Security Code Scanning

이전 단계에서 수정한 CI 파일에서 다음 Section을 발견했을 수 있습니다.

```
      - name: Upload Container Scan results to GitHub Code Scanning
        uses: github/codeql-action/upload-sarif@v1
        with:
          sarif_file: snyk.sarif
```

이렇게 하면 Snyk Container 스캔의 결과가 GitHub's Security Code Scanning 패널로 업로드되어 GitHub UI 내에서 바로 존재하는 취약성을 볼 수 있습니다. 이전 스캔의 결과를 보려면 Security -> Code Scanning Alerts으로 이동하십시오.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/gh-container-codescanning.png)

이를 통해 컨테이너 기본 이미지 선택으로 인해 발생하는 위험을 초기에 빠르게 엿볼 수 있습니다.

## Step 2: Snyk UI에서 Container Scan 결과 검토

컨테이너 기본 이미지로 인해 발생하는 위험을 살펴볼 때 컨테이너에 가능한 최상의 기본 이미지를 사용하고 있는지 확인하는 것부터 시작하는 것이 가장 좋습니다. Snyk CLI, Docker CLI 또는 Snyk UI를 사용할 때 Snyk은 사용 가능한 경우 더 안전한 기본 이미지를 권장합니다.

### Dockerfile을 Snyk으로 가져오기

Snyk UI에서 Part 1에서 만든 프로젝트를 엽니다. 모든 것을 깔끔하게 유지하기 위해 Dockerfile을 이 프로젝트에 추가합니다. 이렇게 하려면 프로젝트 항목에서 + 기호를 클릭하고 Dockerfile에 대한 경로를 제공합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-container-adddockerfile.png)

가져온 후에는 프로젝트 목록에 Dockerfile이 표시되어야 합니다. 그것을 클릭하십시오.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-container-dockerfile.png)

### Base Image Suggestions 검토

Project view에서 특히 컨테이너를 스캔할 때 나타나는 새 상자를 볼 수 있습니다. 이는 현재 기본 이미지가 취약성이 더 적은 다른 옵션과 어떻게 비교되는지 보여줍니다.

애플리케이션과의 호환성 정도에 따라 다음과 같이 그룹화됩니다:

* `Minor` 업그레이드는 작은 작업과 호환될 가능성이 가장 높으며,
* `Major` 업그레이드는 이미지 사용에 따라 주요 변경 사항을 도입할 수 있습니다.
* 더 많은 기술 사용자가 조사할 수 있도록 `Alternative` 아키텍처 이미지가 표시됩니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-container-baseimagerecs.png)

다음 Section에서는 컨테이너 이미지를 빌드하는 데 사용하는 기본 이미지를 업그레이드하여 애플리케이션의 일부 취약성을 해결하고 조치를 취할 것입니다. 준비가 되면 Section 3으로 진행하십시오!
