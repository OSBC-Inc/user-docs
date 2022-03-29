# CLI를 이용하여 Kustomize 파일 테스트

Kustomize 템플릿을 스캔하려면 Kubernetes 매니페스트 파일을 빌드한 후 Snyk CLI의 `iac test` 명령을 사용합니다.

```
kustomize build > kubernetes.yaml
snyk iac test kubernetes.yaml
```

Kustomize 템플릿에 따라 빌드 파라미터 뒤에 이름을 입력해야 할 수 있습니다.
