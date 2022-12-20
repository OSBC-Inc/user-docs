# 프로젝트 Issue 검토

## 애플리케이션 Issue 검토

Snyk UI를 사용하면 애플리케이션 취약점과 프로젝트별 라이선스 Issue를 쉽게 볼 수 있습니다. 먼저 프로젝트 탭에서 애플리케이션을 찾고 프로젝트를 확장한 다음 프로젝트와 연결된 **패키지 매니저 파일**을 선택합니다. 샘플 애플리케이션 SPC에서 **pom.xml** 파일을 선택합니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/screen-shot-2020-08-21-at-4.43.05-pm.png)

Snyk은 프로젝트에 대한 자세한 정보를 표시합니다. 다음은 Snyk이 애플리케이션에 대해 알고 있는 중요한 정보 중 일부입니다.

* **Vulnerabilities** - 애플리케이션에 대한 알려진 총 취약점 수입니다.
* **Dependencies** - 애플리케이션의 총 디펜던시 수입니다. 여기에는 오픈소스의 직접적이고 전이적인 디펜던시가 포함됩니다.
* **Source** - 개발자 툴체인에서 프로젝트가 제공되는 위치입니다. 이 예에서는 GitHub입니다.
* **Branch** - 프로젝트에 해당하는 branch입니다. 이는 SCM에서 소싱된 프로젝트에만 적용됩니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/screen-shot-2020-08-21-at-4.48.13-pm.png)

프로젝트 세부 정보를 검토한 후 Snyk 사용자는 애플리케이션 취약점 및 라이선스 Issue를 포함하는 알려진 Issue를 검토하기 시작합니다. Issue 섹션은 가장 중요한 취약점과 라이선스 Issue를 먼저 식별하도록 구성할 수 있습니다. 우선순위는 중요하며 사용자는 Issue 유형, 심각도, 취약점 성숙도 및 상태를 선택하여 가장 중요한 정보를 먼저 필터링할 수 있습니다.

각 취약점을 검토하면 취약점 목록 하단에 _**more about this issue**_ 옵션이 표시됩니다. 이는 [Snyk의 취약점 데이터베이스](https://snyk.io/product/vulnerability-database/)를 사용하여 취약점에 대한 자세한 정보를 제공하고 심각도 및 취약점 성숙도에 대한 통찰력을 제공합니다. 자세한 설명과 CVSS 점수 정보를 보려면 해당 옵션을 선택하십시오.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/screen-shot-2020-08-21-at-4.47.15-pm.png)
