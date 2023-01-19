# Kubernetes Workload 추가

컨트롤러가 AKS 클러스터에 설치되었으므로 이제 보안 검색을 위한 Workload를 추가할 수 있습니다. 이 주제에 대한 추가 정보는 [Snyk Knowledge Center](https://support.snyk.io/hc/en-us/articles/360003947117-Adding-Kubernetes-workloads-for-security-scanning)를 방문하십시오. 이 Section의 목적을 위해 일부 Workload를 수동으로 추가합니다. 이렇게 하려면 Snyk 웹 콘솔로 이동하여 `Integrations`으로 이동합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk\_integrations\_02.png)

검색창에 `Kubernetes`를 입력하거나 아래로 스크롤합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk\_integrations\_03.png)

여러 환경에서 여러 클러스터를 모니터링할 수 있습니다. 컨트롤러가 Snyk API와 통신하는 경우 Snyk 콘솔에 표시됩니다. 모니터링하려는 적절한 클러스터, 관련 네임스페이스 및 특정 Workload를 선택합니다. 마지막으로 아래 그림과 같이 모든 항목을 선택했으면 오른쪽 상단 모서리에 있는 `Add selected workloads` 버튼을 클릭합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk\_integrations\_04.png)

Workload를 추가하면 결과를 보고 조치를 취할 수 있는 Snyk 콘솔의 `Projects` 페이지로 리디렉션됩니다. 자세한 진행 상태에 대한 `Import log`를 볼 수도 있습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk\_integrations\_05.png)
