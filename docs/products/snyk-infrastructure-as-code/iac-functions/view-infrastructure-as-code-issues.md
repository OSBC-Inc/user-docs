# Infrastructure as Code 이슈 확인

[Snyk reports](https://docs.snyk.io/reports/reports)를 사용하여 Infrastructure as Code 구성 파일에서 이슈를 확인할 수 있습니다.

{% hint style="info" %}
**지원 가능 여부**\
해당 기능은 모든 유료 plan에서 사용할 수 있습니다. 자세한 내용은 [pricing plans](https://snyk.io/plans/)를 참조하세요.
{% endhint %}

## Summary Page

Infrastructure as Code 구성 이슈는 기본적으로 요약 통계 및 그래프에 나타나며 프로젝트 및 이슈 유형 전반에 걸쳐 미해결 이슈를 모두 보여줍니다.

![](../../../.gitbook/assets/image4.png)

IaC 이슈만 확인하려면 **Summary filters** 드롭다운에서 **Configuration**을 선택합니다.

![](../../../.gitbook/assets/screenshot\_2021-02-17\_at\_14.22.50.png)

Summary 탭에 대한 자세한 내용은 [Summary tab](https://docs.snyk.io/reports-1/reports/summary-tab) 문서를 참조하세요.

## Issues page

**Issues** 페이지를 선택하여 모든 프로젝트에서 미해결 이슈에 대한 자세한 정보를 확인할 수 있습니다.

IaC 이슈만 확인하려면 **Issue filters**에서 **Configuration**을 선택합니다.

![](../../../.gitbook/assets/image3.png)

각 이슈의 제목과 유형, 심각도를 확인할 수 있습니다.

그룹 해제된 이슈를 확인할 수 있습니다. 이곳에는 이슈가 발견된 프로젝트 파일에 대한 추가 정보와 이슈가 처음 발생한 시기에 대한 세부정보가 표시됩니다.

![](<../../../.gitbook/assets/image2-3- (1) (2) (2) (2) (3) (4) (4) (3) (1) (1) (10).png>)

issues 탭에 대한 자세한 내용은 [Issues tab](https://docs.snyk.io/reports-1/reports/issues-tab) 문서를 참조하세요.

## 데이터 Export

**Export** 버튼을 클릭하면 이슈의 취약점과 동일한 형식의 CSV 파일로 저장할 수 있습니다.

## API 액세스

[latest issues endpoint](https://snyk.docs.apiary.io/#reference/reporting-api/latest-issues/get-list-of-latest-issues?console=1)를 사용하여 API를 통해 전체 이슈 목록에 액세스할 수 있습니다.

Infrastructure as Code 이슈만 검색하려면 페이로드를 입력하세요.

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
대상 조직을 확인할 때 Snyk UI **Settings** 페이지에서 **public-org-id**를 얻을 수 있습니다.
{% endhint %}

전체 파라미터 목록을 확인하려면 [API Documentation](https://snyk.docs.apiary.io/#reference/reporting-api/latest-issues/get-list-of-latest-issues?console=1) 문서를 참조하세요.
