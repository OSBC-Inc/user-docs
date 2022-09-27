# Dependencies 탭

영역은 선택한 조직의 모든 프로젝트에 있는 모든 직접 의존성에 대한 BOM 역할을 합니다. 다음과 유사합니다.

![](../../.gitbook/assets/dependencies-tab.png)

이 영역은 패키지당 중요한 세부 정보를 표시하여 디펜던시 상태, 즉 패키지 상태를 확인하는 데 도움이 됩니다.

표시되는 세부 정보는 다음과 같습니다.

* 프로젝트에 포함된 패키지에 대한 일반 세부 정보(예: 전체 이름, 프로젝트에 현재 사용되는 패키지 버전, 해당 패키지가 사용되는 프로젝트, 포함된 취약점 및 라이선스 Issue에 대한 요약(있는 경우))
* 간접 의존성 및 이러한 의존성에 포함된 취약점(관련된 경우)
* 지원되는 패키지의 경우 다음과 같이 프로젝트에 사용된 버전뿐만 아니라 패키지의 전반적인 상태에 대한 디펜던시 상태 세부 정보도 다음과 같이 표시됩니다.
  * 더 이상 사용되지 않는 패키지에 대해 경고 아이콘이 표시되며 이는 유지 관리자들이 더 이상 패키지를 업데이트하지 않는다는 의미입니다.

![Reports\_DependenciesDeprecated.png](../../.gitbook/assets/uuid-11be17d2-361f-7354-3c87-535f46cd2324-en.png)

* 최신 버전 및 최신 게시 날짜입니다. 이 날짜를 사용하면 활동 빈도뿐만 아니라 패키지의 성숙도를 더 쉽게 확인할 수 있습니다.

![Reports\_Dependencies\_LastVersionLastPublish.png](../../.gitbook/assets/uuid-a1fa7b20-b64d-6aa6-72be-54477241b434-en.png)

* 프로젝트에 사용된 버전과 사용 가능한 최신 버전이 모두 나열되므로 현재 패키지 버전과 사용 가능한 최신 패키지 버전 사이의 차이를 이해하고 오래된 버전을 평가할 수 있습니다.

![Reports\_Dependencies\_VersionLastVersion.png](../../.gitbook/assets/uuid-095a82e8-5858-4247-78a5-da9e80d3e291-en.png)

이에 대한 자세한 내용은 [Elements](dependencies-tab.md)에 자세히 설명되어 있습니다.

{% hint style="info" %}
**Note**\
네 개의 탭 각각에 있는 데이터는 보고 있는 그룹이나 조직뿐만 아니라 Reports 영역 상단에서 적용한 필터를 기반으로 표시됩니다.
{% endhint %}

## Dependencies 탭 요소

다음은 Reports 영역의 처음 4개 열을 확대한 것입니다.

![](../../.gitbook/assets/uuid-6ed50791-bb66-c746-ab11-d7edfcacdd4d-en.png)

다음 표에서는 그룹화되거나 그룹화되지 않은 Issue를 볼 때 표시되는 Dependencies 영역의 여러 부분에 대해 설명합니다.

| **Element**              | **Possible values**                                                                                                                                                                                                                                                                                                              | **Description**                                                                                                                                                        |
| ------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Dependency               |                                                                                                                                                                                                                                                                                                                                  | <p>하나 이상의 프로젝트에 포함된 디펜던시의 전체 패키지 이름입니다. 상세 패키지 페이지를 보려면 링크를 클릭하십시오.</p><p>예<em>: boom</em></p>                                                                         |
| Warning icon             |                                                                                                                                                                                                                                                                                                                                  | <p>패키지가 더 이상 사용되지 않는 경우 패키지 이름 옆에 경고 아이콘이 나타납니다.<br></p><p><strong>Note:</strong><br>JavaScript 프로젝트에 대한 데이터를 제공합니다.</p>                                               |
| Version                  |                                                                                                                                                                                                                                                                                                                                  | <p>프로젝트에 사용되는 해당 패키지의 버전입니다.</p><p>예: <em>0.4.2</em></p>                                                                                                               |
| Latest version           |                                                                                                                                                                                                                                                                                                                                  | <p>저장소에서 이 패키지에 대해 유지 관리자가 업데이트한 최신 버전입니다.</p><p>예: <em>7.3.0</em></p><p><br><strong>Note:</strong><br>이 필드는 현재 JavaScript, Maven 및 PIP 프로젝트에 대한 데이터만 제공합니다.</p>       |
| Last publish             |                                                                                                                                                                                                                                                                                                                                  | <p>유지 관리자에 의해 패키지의 새 버전이 마지막으로 게시된 시간입니다.</p><p>예: <em>7 months ago</em><br></p><p><strong>Note:</strong><br>이 필드는 현재 JavaScript, Maven 및 PIP 프로젝트에 대한 데이터만 제공합니다.</p> |
| Vulnerabilities          | <p><img src="../../.gitbook/assets/mceclip2-7-.png" alt="mceclip2.png" data-size="original"></p><p><img src="../../.gitbook/assets/mceclip3-3-.png" alt="mceclip3.png" data-size="original"></p><p><img src="../../.gitbook/assets/image (12) (1).png" alt=""></p><p><img src="../../.gitbook/assets/image (13).png" alt=""></p> | 해당 Issue와 관련된 심각도(critical/high/medium/low) 아이콘입니다.                                                                                                                    |
| License                  |                                                                                                                                                                                                                                                                                                                                  | 해당 패키지에서 사용하는 라이선스입니다.                                                                                                                                                 |
| Projects                 |                                                                                                                                                                                                                                                                                                                                  | 해당 패키지를 사용하는 프로젝트입니다.                                                                                                                                                  |
| Dependencies with issues |                                                                                                                                                                                                                                                                                                                                  | Issue가 있는 패키지의 디펜던시에 대한 링크와 해당 Issue에 대한 세부 정보를 제공합니다.                                                                                                                 |

## Dependencies 탭 작업

다음 작업은 아래와 같습니다.

![](../../.gitbook/assets/mceclip7.png)

* **Dependencies 검색** - 입력을 통해 패키지를 검색할 수 있습니다. 여러 패키지의 결과를 보려면 필드를 클릭할 때 열리는 드롭다운 목록에서 패키지를 선택합니다. 또한 드롭다운 목록의 오른쪽 상단 모서리에 있는 Select All 또는 Deselect All을 클릭할 수도 있습니다.
*   **Dependency filters** - 특정 프로젝트 유형 및 디펜던시 상태별로 패키지를 선택하여 표시할 수 있습니다. 선택한 모든 기준과 일치하는 Issue만 표시됩니다.

    Deprecated를 선택하면 더 이상 사용되지 않는 것으로 표시된 패키지만 나타납니다.
* **Hidden fields** - 현재 작업에 중요한 세부 정보에 초점을 맞추려면 화면에서 기본 열을 제거합니다.
* **Export as CSV** - Issue 데이터를 CSV 파일 형식으로 내보냅니다.
