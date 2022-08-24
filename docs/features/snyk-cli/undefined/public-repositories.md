# 사용하기 전 public repositories 테스트

공개 Github, BitBucket 또는 GitLab 저장소를 테스트하려면 `snyk test`를 실행하고 저장소에 대한 GitHub URL을 포함하십시오.

`$ snyk test https://github.com/snyk/snyk`

다음 git URL 형식이 지원됩니다.

* `git://github.com/user/project.git#commit-ish`
* `https://github.com/user/project#commit-ish`
* `user/project#commit-ish`

이것은 Bitbucket 및 GitLab에서도 작동합니다.&#x20;

[snyk.io](https://snyk.io/test/)의 테스트 페이지를 통해 공개 npm 패키지 또는 Github 프로젝트를 테스트할 수도 있습니다.&#x20;

참고 항목

* [CLI 시작하기](../cli.md)
* [CLI reference](../cli-reference.md)
* [CLI에서 Snyk 오픈 소스 사용](cli-snyk.md)
* [CLI 테스트에 대한 severity threshold 설](set-severity-thresholds-for-cli-tests.md)정
* [사용하기 전 공용 npm 패키지 테스트](npm.md)
