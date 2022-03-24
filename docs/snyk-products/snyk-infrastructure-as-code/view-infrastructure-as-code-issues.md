# Infrastructure as Code Issue 보고서 보기

[Snyk reports](https://docs.snyk.io/reports/reports)를 사용하여 Infrastructure as Code의 구성 파일에서 구성 Issue를 확인할 수 있습니다.

{% hint style="info" %}
**기능 지원 여부**\
****이 기능은 모든 유료 요금제에서 사용할 수 있습니다. 자세한 내용은 [pricing plans](https://snyk.io/plans/)를 참조하십시오.
{% endhint %}

### Summary 페이지

Infrastructure as Code 구성 Issue는 기본적으로 요약 통계 및 그래프가 나타나 프로젝트 및 Issue 유형 전반에 걸쳐 미해결 상태인 모든 Issue를 표시합니다.

![](../../.gitbook/assets/image4.png)

IaC Issue만 보려면 **Summary filters** 드롭다운에서 **Configuration**을 선택합니다.

![](../../.gitbook/assets/screenshot\_2021-02-17\_at\_14.22.50.png)

Summary 탭에 대한 자세한 내용은 [Summary tab](../../features/general-reports/reports/summary-tab.md) 설명서를 참조하십시오.

### Issues 페이지

모든 프로젝트에서 미해결 상태의 Issue에 대한 자세한 정보를 보려면 **Issues** 페이지를 선택합니다.

IaC Issue만 보려면 **Issue filters** 드롭다운에서 **Configuration**을 선택합니다.

![](../../.gitbook/assets/image3.png)

여기에는 각 Issue 및 유형의 제목과 심각도가 표시됩니다.

그룹화되지 않은 Issue도 볼 수 있습니다. 이렇게 하면 Issue가 발견된 프로젝트 파일에 대한 자세한 정보와 Issue가 처음 도입된 시기에 대한 상세 정보가 표시됩니다.

![](<../../.gitbook/assets/image2-3- (1) (2) (2) (2) (3) (4) (4) (3) (1) (1) (10).png>)

Issues 탭에 대한 자세한 내용은 [Issues tab](../../features/general-reports/reports/issues-tab.md) 설명서를 참조하십시오.

### 데이터 내보내기

**Export** 버튼을 사용하여 Issue를 취약점과 동일한 형식의 CSV 파일로 내보낼 수 있습니다.

### API 액세스

[latest issues endpoint](https://snyk.docs.apiary.io/#reference/reporting-api/latest-issues/get-list-of-latest-issues?console=1)를 사용하여 API를 통해 Issue의 전체 목록에 액세스할 수 있습니다.

Infrastructure as Code Issue만 검색하려면 body 페이로드를 제출하십시오.

```
{
  "filters": {
    "orgs": ["my-public-org-id"],
    "types": [
      "configuration"
    ]
  }
}
```

{% hint style="info" %}
대상 조직을 볼 때 Snyk UI **Settings** 페이지에서 **public-org-id**를 얻을 수 있습니다.
{% endhint %}

파라미터의 전체 목록은 [API Documentation](https://snyk.docs.apiary.io/#reference/reporting-api/latest-issues/get-list-of-latest-issues?console=1)을 참조하십시오.
