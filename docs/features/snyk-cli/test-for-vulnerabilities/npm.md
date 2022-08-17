# Test public npm packages before use

`synk test`를 사용하여 **공개 패키지를 설치하기 전에 자세히 조사하여** 알려진 취약성이 있는지 여부를 확인할 수 있습니다. 패키지 이름을 사용하여 패키지의 최신 버전을 테스트합니다.

`snyk test ionic@1.6.5`

다음을 사용하여 특정 버전 또는 범위를 제공할 수도 있습니다.`snyk test module[@semver-range]`

참고 항목 [Getting started with the CLI](../cli.md)
