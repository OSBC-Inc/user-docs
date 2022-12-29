# YAML pipelines

{% hint style="info" %}
Azure Pipelines용 YAML 스키마에 대한 포괄적인 설명서는 [Microsoft의 Azure DevOps 설명서 페이지](https://docs.microsoft.com/en-us/azure/devops/pipelines/yaml-schema?view=azure-devops\&tabs=schema%2Cparameter-schema)에서 사용할 수 있습니다.
{% endhint %}

azure-pipelines.yml 예제는 아래에서 사용할 수 있습니다:

```yaml
trigger:
- master

resources:
- repo: self

variables:
  dockerRegistryServiceConnection: '$(Your-GUID)'
  imageRepository: '$(Your-Repo-Name)'
  containerRegistry: '$(Your-Registry-Name)'
  dockerfilePath: '$(Build.SourcesDirectory)/Dockerfile'
  manifestfilePath: '$(Build.SourcesDirectory)/manifests/**/*'
  namespaceApp: '$(Your-Name)'
  tag: '$(Build.BuildId)'
  vmImageName: 'ubuntu-latest'

stages:
- stage:
  jobs:
  - job:
    pool:
      vmImage: $(vmImageName)
    steps:
    - task: SnykSecurityScan@0
      inputs:
        serviceConnectionEndpoint: 'Snyk'
        testType: 'app'
        monitorOnBuild: true
        failOnIssues: true
    - task: Docker@2
      inputs:
        command: 'buildAndPush'
        repository: $(imageRepository)
        dockerfile: $(dockerfilePath)
        containerRegistry: $(dockerRegistryServiceConnection)
        tags: |
          $(tag)
    - task: KubernetesManifest@0
      inputs:
        action: 'deploy'
        kubernetesServiceConnection: '$(Your-Name)'
        namespace: '$(namespaceApp)'
        manifests: '$(manifestfilePath)'
        containers: '$(tag)'
```

위의 예는 참고용일 뿐입니다. 파이프라인이 다를 수 있습니다. 이 예제에서는 Azure Repo에서 소스 코드를 스캔하고 컨테이너 이미지를 ACR로 Push하고 AKS에 배포합니다. Snyk 스캔은 위의 24-29행에 정의되어 있습니다.
