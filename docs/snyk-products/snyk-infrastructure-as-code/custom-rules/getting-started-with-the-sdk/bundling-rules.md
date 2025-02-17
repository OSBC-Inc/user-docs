# Rule 번들링

다음 명령어를 실행하여 custom rule bundle을 빌드할 수 있습니다.

```
snyk-iac-rules build
```

현재 폴더에 생성된 Rule보다 더 많은 Rule이 있는 경우 `--ignore` 옵션을 사용하여 production-ready bundle에 관련이 없는 폴더 및 파일을 제외하십시오. 옵션을 사용하여 진행하면 프로세스 속도를 높이고 생성된 bundle의 크기를 작게 유지할 수 있습니다.

#### 기본 진입점 재정의

**`deny`**와 다른 Rule(`allow`,`violation` 등)의 이름을 지정하도록 선택한 경우 다음과 같이 실행하여 재정의할 수 있습니다.

```
snyk-iac-rules build --entrypoint "<package name>/<function name>"
```

마지막으로 bundle의 압축을 풀지 않고도 다음을 실행하여 bundle의 내용을 확인할 수 있습니다.

```
tar -tf bundle.tar.gz
```

그러면 bundle에 포함된 모든 파일이 출력됩니다.

```
/data.json
/lib/main.rego
/rules/my_rule/main.rego
/policy.wasm
/.manifest
```

이제 새로 구축된 [custom bundle로 snyk iac test를 실행할 수 있습니다](../use-iac-custom-rules-with-cli/).
