# CLI를 이용하여 ARM 파일 테스트 진행

Snyk Infrastructure as Code를 사용하면 CLI에서 직접 구성 파일을 테스트할 수 있습니다.

ARM(Azure Resource Manager)에서 Snyk Infrastructure as Code는 json 형식 검색을 지원합니다.

{% hint style="info" %}
Bicep CLI를 사용하여 구성 파일을 json으로 변환하여 bicep 형식을 검색할 수도 있습니다.
{% endhint %}

CLI는 다음과 같이 사용할 수 있습니다.

## 지정된 json 파일 테스트

CLI에서 다음과 같이 입력합니다.

```
snyk iac test deploy.json
```

파일이름을 추가하여 다음과 같이 여러 파일을 지정할 수 있습니다.

```
snyk iac test file-1.json file-2.json
```

## 지정된 bicep 파일 테스트

우선 [Bicep CLI](https://docs.microsoft.com/en-us/azure/azure-resource-manager/bicep/install)가 설치되어 있는지 확인합니다.

Bicep CLI를 설치한 후 bicep 파일이 들어 있는 디렉토리로 이동하고 다음을 입력하여 관련 bicep 파일을 json으로 변환합니다

```
az bicep build -f deploy.bicep
```

다른 파일과 마찬가지로 새로 만든 json 파일을 CLI에서 다음과 같이 입력하여 검색할 수 있습니다.

```
snyk iac test deploy.json
```
