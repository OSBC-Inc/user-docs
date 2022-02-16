# CLI를 이용하여 Kustomize 파일 테스트 진행

Kuberenetes 매니페스트 파일을 작성한 다음 Snyk IaC CLI를 사용하여 Kustomize 템플릿을 스캔합니다.

```
kustomize build > kubernetes.yaml
snyk iac test kubernetes.yaml
```

Kustomize 템플릿에 따라 빌드 파라미터 뒤에 이름을 입력해야 할 수 있습니다.
