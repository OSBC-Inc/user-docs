# 결과 보고서

## Dynatrace

Dynatrace environment에서 **Application Security** 메뉴 및 **Vulnerabilities** 하위 메뉴로 이동하여 모니터링되는 리소스를 봅니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/dynatrace-vuln-01.png)

영향을 받는 노드와 같은 추가 컨텍스트 정보를 보려면 링크를 클릭하고 자세한 내용은 Snyk 링크를 클릭하여 특정 취약성을 드릴다운할 수 있습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/dynatrace-vuln-02.png)

위와 같이 **More details provided by Snyk** 버튼을 클릭하면 특정 취약점에 대한 자세한 보고서가 제공됩니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/dynatrace-vuln-03.png)

## Snyk

또한 Dynatrace OneAgent와 함께 이 클러스터에 Snyk Monitor를 배포했기 때문에 컨테이너 기본 이미지 업그레이드 권장 사항, 응용 프로그램 구성 오류, 이들 및 응용 프로그램 코드 전반에 대한 수정 조언과 같은 추가 세부 정보를 얻을 수 있습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/snyk-vulns-01.png)

위의 예에서 Kubernetes 프로젝트를 가져오고 [Snyk SCM 통합 모범 사례 가이드의 지침](https://support.snyk.io/hc/en-us/articles/360018010597-Snyk-SCM-integration-good-practices)에 따라 GitHub의 소스도 가져왔습니다.

이러한 통합을 통해 우리 환경에서 실행되는 특정 취약성과 악용을 신속하게 식별할 수 있으며 더 중요한 것은 이를 수정하는 방법입니다!
