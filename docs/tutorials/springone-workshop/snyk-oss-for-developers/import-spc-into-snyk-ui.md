# SPC를 Snyk UI로 가져오기

## GitHub 저장소용 Snyk에 프로젝트 추가

Snyk은 루트 폴더 및 사용자 지정 파일 위치를 평가하여 지원되는 언어로 된 GitHub 저장소를 테스트하고 모니터링합니다.

**Snyk에 프로젝트 추가**

1\) Projects로 이동하여 Add projects를 클릭합니다. 그 다음 프로젝트를 가져올 도구 선택

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/project\_import.png)

2\) 선택한 통합에서 사용 가능한 모든 저장소가 있는 팝업 화면이 열립니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/select\_repo.png)

{% hint style="info" %}
Spring-Petclinic\_\*\*\_repository를 선택합니다.
{% endhint %}

3\) Snyk으로 가져올 저장소를 선택하십시오. 이렇게 하면 보안 및 라이선스 문제에 대해 저장소를 모니터링합니다. 특정 조직의 모든 저장소를 가져오려면 조직을 선택 표시합니다.

4\) 선택한 저장소 추가를 클릭합니다. Snyk는 루트 폴더와 사용자 지정 파일 위치를 평가합니다. 루트 수준 또는 구성한 경로에서 매니페스트 파일을 찾을 수 없는 경우 Snyk는 가져올 수 있는 파일이 없다고 알려줍니다.

## 가져온 프로젝트

Snyk은 프로젝트를 가져올 때 가져오기 상태 표시줄과 화면 새로고침을 묻는 녹색 상자가 표시됩니다.

{% hint style="info" %}
새로 고침 녹색 상자가 표시되지 않음
{% endhint %}

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/import\_bar.png)

새로고침하면 Snyk UI에 가져온 프로젝트가 표시됩니다. 프로젝트를 확장하여 패키지 관리자 파일(여기서는 **pom.xml**)을 확인합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/screen-shot-2020-08-21-at-4.43.05-pm%20\(1\).png)
