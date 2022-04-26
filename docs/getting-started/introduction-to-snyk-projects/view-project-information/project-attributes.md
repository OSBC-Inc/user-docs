# 프로젝트 속성

프로젝트 속성은 추가 메타데이터(값)를 프로젝트에 추가할 수 있는 정적 필드입니다. 속성에는 선택할 수 있는 미리 정의된 값 목록이 있습니다. 속성에서 값을 할당 및 제거할 수 있으며 프로젝트를 그룹화하고 우선 순위를 지정하고 필터링하는데 사용할 수 있습니다.

## 사용 가능한 속성 및 값

### **Lifecycle stage**

* Production
* Development
* Sandbox

### **Business criticality**

* Critical
* High
* Medium
* Low

### **Environment**

* Frontend
* Backend
* Internal
* External
* Mobile
* SaaS
* Hosted
* Distributed

속성에서 값을 할당 및 제거하는 기능은 [API](https://snyk.docs.apiary.io/#reference/projects/project-attributes) 및 [CLI](broken-reference)에서 사용할 수 있습니다. 값으로 프로젝트를 필터링하는 기능은 [API](https://snyk.docs.apiary.io/#reference/projects/project-attributes)에서도 사용할 수 있습니다 .

## **속성에 값 할당**

1. 프로젝트 페이지에서 값을 할당하려는 속성 아래의 "+" 아이콘을 클릭합니다.
2. 목록에서 값을 선택합니다.

![](../../../.gitbook/assets/gs1.png)

속성에 값을 할당하면 프로젝트 목록 페이지에 나타납니다. 각 속성에는 여러 값이 할당될 수 있으며 여러 속성에 값을 할당할 수 있습니다.

![](../../../.gitbook/assets/gs2.png)

## **속성에서 값 제거**

1. 값을 제거할 속성을 선택합니다.
2. 값에서 "x" 아이콘을 클릭합니다.

![](../../../.gitbook/assets/gs3.png)

속성에서 값이 제거되었습니다.

![](../../../.gitbook/assets/gs4.png)

## **프로젝트 목록 페이지에서 값 필터링**

1. 프로젝트 목록 페이지 왼쪽에서 프로젝트를 필터링할 값을 선택합니다.
2. 단일 속성에서 여러 값으로 필터링하면 필터에서 하나 이상의 값이 할당된 프로젝트가 나타납니다.
3. 여러 속성으로 필터링하면 필터에서 두 속성의 값이 모두 할당된 프로젝트가 나타납니다.

![](../../../.gitbook/assets/gs5.png)
