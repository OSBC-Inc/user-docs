# SPC를 Snyk UI로 가져오기

## GitHub 저장소용 Snyk에 프로젝트 추가

Snyk은 루트 폴더 및 사용자 지정 파일 위치를 평가하여 지원되는 언어로 된 GitHub 저장소를 테스트하고 모니터링합니다.

**Snyk에 프로젝트 추가**

1\) Projects로 이동하여 Add projects를 클릭합니다. 그 다음 프로젝트를 가져올 도구 선택

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/project\_import.png)

2\) A popup screen opens with all the available repositories under the selected integration

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/select\_repo.png)

{% hint style="info" %}
Select the Spring-Petclinic \_\*\*\_repository.
{% endhint %}

3\) Select the repository to import into Snyk. This will monitor the repositories for security and license issues. To import all repositories for a specific organization, checkmark the organization.

4\) Click add selected repositories. Snyk evaluates root folders and custom file locations. If no manifest files are found on the root level or in the paths you configure, Snyk notifies you that no files can be imported.

## Imported projects

As Snyk is importing your project you will see the import status bar followed by a **green box** asking you to refresh the screen.

{% hint style="info" %}
Refresh green box not shown
{% endhint %}

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/import\_bar.png)

After refreshing, you will see the imported projects in the Snyk UI. Expand the project to see the package manager file, in our case _**pom.xml**_

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/screen-shot-2020-08-21-at-4.43.05-pm%20\(1\).png)
