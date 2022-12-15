# CI/CD 결과 검토

## CI/CD 결과 보기

비밀을 추가하고 파이프라인에서 환경 변수를 구성했으므로 이제 결과를 검토할 수 있습니다. 작업의 마지막 실행을 선택하고 Snyk 스캔 결과를 살펴보겠습니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/screen-shot-2020-08-22-at-11.28.15-am.png)

## Snyk 스캔 결과

Snyk은 작업 구성에 따라 Synk 모니터 명령을 수행했습니다. Snyk에서는 애플리케이션의 취약점 및 라이선스 준수 여부를 테스트하거나 모니터링하도록 선택할 수 있습니다. 모니터링은 스캔 결과를 저장하고 새로운 취약성과 라이선스 문제에 대한 지속적인 모니터링을 수행합니다. Snyk 작업의 출력에서 저장된 결과의 URL을 볼 수 있습니다. Snyk UI를 사용하여 결과를 검토할 수도 있습니다. 이 작업은 나중에 Synk CI/CD 섹션에서 수행합니다.

이 GitHub 파이프라인에서는 Maven 빌드 프로세스와 병렬로 모니터를 수행하는 GitHub Snyk 작업을 추가했습니다. 결과가 Snyk 조직에 업로드되었습니다. 이 워크숍의 뒷부분에서 Snyk의 결과를 검토할 것입니다.

![](https://partner-workshop-assets.s3.us-east-2.amazonaws.com/screen-shot-2020-08-22-at-11.52.35-am.png)
