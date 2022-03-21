# 언어 및 프레임워크

## Snyk Code AI 엔진을 통한 언어 지원

Snyk Code는 AI를 활용한 심층 코드 시맨틱 코드 분석 엔진을 기반으로 하여 글로벌 개발 커뮤니티에서 수십억 줄의 코드와 수억 개의 코드 수정을 통해 지속적으로 학습합니다. Snyk Code AI 엔진은 Snyk의 보안 연구원과 엔지니어가 주도하는 인간 주도의 강화 학습 사이클을 지속적으로 발전시킵니다. 자세한 내용은 [이 블로그 기사](https://snyk.io/blog/advanced-technologies-behind-snyk-code/)를 참조하십시오.

분석을 위해 파일이 제공되면 엔진은 언어 독립적인 공통 중간 형식으로 어떤 파서에 어떤 파일을 넣을지 결정합니다. 이 형식은 스캔한 소스 코드의 특성을 보존하고 노출합니다.

이 기술을 통해 Snyk Code는 다음을 수행할 수 있습니다.

* 모든 프로그래밍 언어를 쉽게 지원합니다.
* 다양한 언어에 대한 보안 스캔에 걸쳐 여러 언어의 프로젝트를 지원합니다.
* 일반적으로 특히 추적하기 어려운 여러 소스 파일에 퍼져 있는 Issue 패턴과 같은 파일 간 Issue를 밝힙니다.
* Snyk Code 엔진을 사용하여 Issue 패턴을 찾고 발견된 Issue를 보고서로 컴파일합니다.

Snyk Code는 현재 다음을 지원합니다:

* **Java**
* **JavaScript**
* **TypeScript**
* **Python**
* **PHP**
* **C#**

_베타 지원은 다음과 같습니다. Go, Ruby 및 Kotlin은 자세한 내용이나 기타 필요한 사항이 있으면 당사에 문의하십시오._

## 언어 유형 및 프레임워크 지원

Snyk Code는 다양한 관련 언어 유형에서 사용할 수 있습니다.

* JavaScript 및 Python과 같은 동적 유형 언어.
* TypeScript와 같은 강력한 유형의 언어(옵션).
* Java와 같은 강력한 유형의 언어.

프레임워크, 라이브러리 및 취약점 유형에 대한 전체 지원 목록은 Snyk에 문의하십시오.

## 지원하는 확장자

지원하는 확장자는 다음과 같습니다.

{% hint style="info" %}
c,cc,cpp,cxx,h,hpp,hxx,ejs,es,es6,htm,html,js,jsx,ts,tsx,vue,java,erb,haml,rb,rhtml,slim,py,go,ASPX,Aspx,CS,Cs,aspx,cs,php, xml
{% endhint %}

\*Snyk Code는 파일당 3줄 이하의 파일은 무시합니다. 또한 4MB보다 큰 단일 파일은 무시됩니다.

### 프레임워크 지원

특정 프레임워크를 지원하려면 Snyk Code가 관련 언어를 지원하고 프레임워크를 사용하는 프로젝트에 대해 교육을 받아야 합니다. 발견된 패턴은 보안 팀에 의해 주석 처리 되고 선별된 컨텐츠로 확장됩니다.

대부분의 프레임워크는 즉시 지원되며, Snyk Code는 코드를 분석하기 위해 구문 분석만 하면 됩니다. 경우에 따라 특정 규칙이 필요하거나 특정 프로그램 분석 엔진 업데이트 또는 둘 다 필요할 수 있습니다. 특정 프레임워크 지원에 공백이 있는 경우 세부 정보/예시를 [알려주시면](https://support.snyk.io/hc/en-us/requests/new) 저희 팀에서 해결해 드리겠습니다.

### JavaScript 프레임워크

{% hint style="info" %}
다음은 JavaScript에 대해 명시적으로 지원되는 프레임워크 중 일부입니다. 이는 모든 프레임워크에 대한 일반적인 지원에 추가됩니다.
{% endhint %}

* **React**: 웹사이트 및 모바일 애플리케이션을 위한 사용자 인터페이스 또는 UI 구성 요소를 구축하기 위한 오픈 소스, front-end, JavaScript 라이브러리
* **Vue.js**: 사용자 인터페이스 및 단일 페이지 애플리케이션을 구축하기 위한 오픈소스 model–view–viewmodel front-end JavaScript 프레임워크
* **Express**: 자유 및 오픈 소스 소프트웨어로 출시된 Node.js용 back-end 웹 애플리케이션 프레임워크(Node.js의 사실상의 표준 서버 프레임워크)
* **jQuery:** 빠르고 작으며 기능이 풍부한 JavaScript 라이브러리. HTML 문서 순회 및 조작, 이벤트 처리, 애니메이션 등을 만듭니다.

### 자바 프레임워크

{% hint style="info" %}
다음은 Java에 대해 명시적으로 지원되는 프레임워크 중 일부입니다. 이는 모든 프레임워크에 대한 일반적인 지원에 추가됩니다.
{% endhint %}

* **Apache Camel**: 규칙 기반 라우팅 및 중개 엔진을 갖춘 메시지 지향 미들웨어용 오픈소스 프레임워크
* **Apache Struts**: 현대적인 Java 웹 애플리케이션을 만들기 위한 오픈 소스 MVC 프레임워크
* **Spring MVC**: Spring 웹 MVC(model-view-controller) 프레임워크
* **Spring JDBC**: Spring JDBC 데이터 접근 계층, 단순한 ORM
* **Jakarta XML Services**: XML 기반 웹 서비스를 구현하기 위한 프레임워크

### 파이썬 프레임워크

{% hint style="info" %}
다음은 명시적으로 지원되는 Python용 프레임워크 중 일부입니다. 이는 모든 프레임워크에 대한 일반적인 지원에 추가됩니다.
{% endhint %}

* [Django](https://www.djangoproject.com): 풀 스택 웹 애플리케이션 개발 및 서버 개발을 위한 프레임워크
* [Flask](https://palletsprojects.com/p/flask/): 경량 [WSGI](https://wsgi.readthedocs.io) 웹 애플리케이션 프레임워크

### C# 프레임워크

{% hint style="info" %}
다음은 C#에 대해 명시적으로 지원하는 프레임워크 중 일부입니다. 이는 모든 프레임워크에 대한 일반적인 지원에 추가됩니다.
{% endhint %}

* **.NET framework**: .NET은 Microsoft에서 만들고 다양한 애플리케이션 유형을 빌드하는 데 사용되는 오픈 소스 개발자 플랫폼입니다. .Net은 다양한 언어를 지원하지만 Snyk Code는 C# 인터페이스를 사용하여 .NET을 지원합니다.
* **ASP.NET (version 4.x)**: ASP.NET은 .NET을 사용하여 웹 앱 및 서비스를 빌드하기 위한 자유 및 오픈 소스 프레임워크입니다. Snyk Code는 버전 4.x를 지원합니다
* **.NET Core**: Microsoft는 .NET 프레임워크를 교차 플랫폼으로 만들고 여러 시나리오를 활성화하기 위해 .NET Core를 만들었습니다. .NET 프레임워크와 .NET Core는 많은 구성 요소를 공유하며 코드를 교환할 수 있습니다. .NET 프레임워크와 .NET Core는 많은 구성 요소를 공유하며 코드를 교환할 수 있습니다. (Microsoft는 선택할 수 있는 [방법을 안내](https://docs.microsoft.com/en-us/dotnet/standard/choosing-core-framework-server)합니다.)

{% hint style="info" %}
프레임워크 지원은 항상 엔진에 알려진 파일 확장자에 의해 결정됩니다. 예를 들어, 엔진은 **\*.cshtml** 파일을 스캔하지 않고 연결된 **\*.cshtml.cs** 파일을 스캔합니다.
{% endhint %}
