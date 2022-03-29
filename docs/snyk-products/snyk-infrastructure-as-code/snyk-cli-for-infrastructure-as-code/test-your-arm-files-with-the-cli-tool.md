# CLI를 이용하여 ARM 파일 테스트

Snyk Infrastructure as Code를 사용하면 CLI에서 직접 구성 파일을 테스트할 수 있습니다.

ARM(Azure Resource Manager)에서 Snyk Infrastructure as Code는 json 형식 파일 스캔을 지원합니다. Bicep CLI를 사용하여 구성 파일을 JSON으로 변환함으로써 Bicep 형식 파일을 스캔할 수도 있습니다.

## 지정된 json 파일에 대한 Issue 테스트

다음 Snyk CLI 명령을 입력합니다.

```
snyk iac test deploy.json
```

다음과 같이 파일 이름을 차례로 추가하여 여러 파일을 지정할 수도 있습니다.

```
snyk iac test file-1.json file-2.json
```

## 지정된 bicep 파일 테스트

우선 [Bicep CLI](https://docs.microsoft.com/en-us/azure/azure-resource-manager/bicep/install)가 설치되어 있는지 확인합니다.

Bicep CLI를 설치한 후 bicep 파일이 들어 있는 디렉토리로 **이동**하고 다음을 입력하여 관련 bicep 파일을 json으로 **변환**합니다.

```
az bicep build -f deploy.bicep
```

새로 생성된 JSON 파일은 다른 파일과 같은 방법으로 스캔할 수 있습니다. 다음 Snyk CLI 명령을 사용합니다.

```
snyk iac test deploy.json
```
