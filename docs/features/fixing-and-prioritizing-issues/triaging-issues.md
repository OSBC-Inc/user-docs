# Issues 분류

### 소개

모든 취약점에는 해당 취약점이 위협(악용 가능)을 제기하기 위해 충족되어야 하는 조건이 있습니다.

취약한 상태의 예는 다음과 같습니다:

* 사용자 상호 작용 필요
* 특정 포트 번호 열기
* 특정 CPU 아키텍처 필요
* 특정 설정 활성화

#### 모든 것은 컨텍스트에 관한 것입니다

일부 취약점에는 해당 취약점이 악용될 수 있으려면 모두 충족되어야 하는 여러 가지 조건이 있습니다. 취약한 오픈 소스 패키지는 일부 응용 프로그램에서 악용될 수 있지만 다른 응용 프로그램에서는 악용될 수 없습니다.

악용 가능성은 컨텍스트(예: 환경, 설정 및 개발자가 이 패키지를 사용하는 방식)에 따라 다릅니다.

악용할 수 없는 취약점은 애플리케이션에 보안 위협이 될 가능성이 낮으므로 그에 따라 우선 순위를 낮출 수 있습니다.

### 분류 도우미

{% hint style="info" %}
현재 이 기능은 **GitHub**를 소스로 사용하고 **Snyk Code**가 활성화된 경우 **Java**(Gradle 및 Maven) 생태계에서만 사용할 수 있습니다.
{% endhint %}

응용 프로그램의 컨텍스트에서 Triage Assistant는 취약한 조건을 평가하여 응용 프로그램의 악용 가능성을 결정하는 데 도움이 됩니다.

Snyk Code ([SAST](https://snyk.io/learn/application-security/sast-vs-dast/)) 엔진은 자사 코드를 읽고 SCA(Snyk Open Source)가 발견한 취약성에 대한 조건을 확인하는 데 사용됩니다.

{% hint style="info" %}
이 기능을 제공하기 위해 Snyk는 Git 저장소 콘텐츠의 임시 복사본을 가져옵니다. 자세한 내용은 [how-snyk-handles-your-data.md](../../more-info/how-snyk-handles-your-data.md "mention")을 참조하십시오.
{% endhint %}

#### 취약한 조건

Jackson Vulnerable 조건:

* **Vulnerable version**: [Jackson 패키지](https://snyk.io/vuln/maven:com.fasterxml.jackson.core%3Ajackson-databind)(**com.fasterxml.jackson.core:jackson-databind vulnerabilities**)는 취약한 것으로 알려진 특정 버전에 있어야 합니다.
* **Specific setting**: 특정 설정 또는 기능을 활성화해야 합니다. 이 경우에는 [**Polymorphic Type Handling**](https://github.com/FasterXML/jackson-docs/wiki/JacksonPolymorphicDeserialization) 기능입니다.
* **User interactivity**: 애플리케이션은 사용자의 JSON 입력을 수락해야 합니다.
* **Specific gadget**: 클래스 또는 함수인 “gadget”은 애플리케이션의 실행 범위 내에서 사용할 수 있어야 합니다.

취약점을 악용하려면 모든 조건이 충족되어야 합니다.

{% hint style="info" %}
이 기능은 현재 **미리보기** 상태이며 변경될 수 있습니다.
{% endhint %}

#### Exploit Maturity가 있지만 악용할 수 없는 취약점이 있습니까?

취약성에는 악용이 가능하거나 악용 방법에 대한 자세한 설명이 있을 수 있지만 모든 조건이 충족되지 않는 한 취약성은 악용할 수 없습니다.
