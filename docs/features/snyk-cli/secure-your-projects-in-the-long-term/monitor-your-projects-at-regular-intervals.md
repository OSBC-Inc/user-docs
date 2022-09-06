# 정기적으로 프로젝트 모니터링

`test` 명령과와 `@snyk/protect` [package](https://github.com/snyk/snyk/tree/master/packages/snyk-protect)(snyk `protect` command 대체)를 사용하면 알려진 취약점을 해결할 수 있습니다. 지속적으로 공개되는 새로운 취약점을 해결하려면 snyk 모니터를 사용하십시오.

배포하기 직전에 프로젝트 디렉토리에서 `snyk monitor`를 실행하십시오:

`cd ~/projects/myproject/`\
`snyk monitor`

그러면 현재 디펜던시의 스냅샷이 Snyk 대시보드로 전송되므로 Snyk는 해당 디펜던시에서 새로 공개된 취약점에 대해 또는 이전에 사용할 수 없었던 패치 또는 업그레이드 경로가 생성될 때 알려줄 수 있습니다. 동일한 프로젝트의 여러 스냅샷을 찍는 경우 Snyk는 최신 스냅샷에 대한 새로운 정보만 알려줍니다.

로그인하고 조직의 프로젝트 페이지([https://app.snyk.io/monitor/](https://app.snyk.io/org/nskim/projects))로 이동하여 프로젝트의 최신 스냅샷과 기록을 확인하세요.
