# 고급 Snyk Container CLI 사용

## 아카이브 테스트

로컬 Docker 데몬 또는 원격 레지스트리의 이미지를 테스트하는 것 외에도 Snyk은 Docker 또는 OCI 아카이브를 직접 테스트하거나 모니터링할 수 있습니다.

```
snyk container test docker-archive:archive.tar
snyk container test oci-archive:archive.tar
```

## 다중 플랫폼 이미지 테스트

일부 저장소는 필요한 운영체제 및 아키텍쳐에 따라 여러 다른 이미지를 가리키는 다중 매니페스트를 나타냅니다. Snyk CLI `container` 명령을 사용하여 특정 플랫폼에 대한 이미지를 명시적으로 테스트할 수 있습니다.

```
snyk container test --platform=linux/arm64 debian
```

`--platform` flag에는 다음 중 하나가 포함되어야 합니다.

* linux/amd64
* linux/arm64
* linux/riscv64
* linux/ppc64le
* linux/s390x
* linux/386
* linux/arm/v7
* linux/arm/v

## 원격 컨테이너 레지스트리에 인증

Docker가 설치되면 Snyk CLI `container` 명령은 미리 구성된 레지스트리 인증을 사용합니다. Docker를 사용하지 않는 경우 command를 통해 인증 정보를 전달할 수 있습니다.

* 다음 환경 변수를 사용합니다. `SNYK_REGISTRY_USERNAME` 및 `SNYK_REGISTRY_PASSWORD`
* 또는 다음과 같이 사용자 이름과 암호를 전달합니다.

```
snyk container test <repository>:<tag> --username= --password=
```

두 옵션이 모두 전달되는 경우 옵션이 환경 변수보다 우선 적용됩니다.

## 일반적인 추가 옵션

몇 가지 유용한 CLI 옵션은 다음과 같습니다.

| Option                       | Description                                                                                                                                      |
| ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| `--json`                     | 결과를 JSON 형식으로 인쇄하여 다른 도구와 통합하는 데 유용합니다.                                                                                                          |
| `--sarif`                    | 결과를 다른 도구와 통합하는 데 유용한 [SARIF](https://www.oasis-open.org/committees/tc\_home.php?wg\_abbrev=sarif) 형식으로 반환합니다. 이렇게 하려면 `--file`로도 테스트를 실행해야 합니다. |
| `--exclude-base-image-vulns` | 기본 이미지에 의해서만 도입된 취약점을 표시하지 않습니다. `snyk container test` 사용 시에만 사용할 수 있습니다.                                                                        |
| `--severity-threshold`       | 지정된 수준 이상의 취약점만 보고합니다.                                                                                                                           |
| `--app-vulns`                | Snyk을 사용하면 한 번의 스캔으로 컨테이너 이미지와 운영체제에서 애플리케이션 디펜던시의 취약점을 모두 감지할 수 있습니다.                                                                           |
| `--nested-jars-depth`        | `--app-vulns`를 사용할 경우 `--nested-jars-depth=n` 옵션을 사용하여 Snyk이 압축을 풀어야 하는 중첩된 jar의 수준을 설정합니다.                                                      |

더 많은 옵션은 Snyk CLI `container` [도움말](../../../features/snyk-cli/commands/container.md) 참조하거나 다음을 실행하여 도움말을 참고하십시오.

```
snyk container --help
```

## 추가 정보

* [컨테이너 보안을 위한 Snyk CLI](./)
* [Snyk Container CLI 결과 이해](understanding-snyk-container-cli-results.md)
