# Snyk을 워크플로우에 통합하는 방법

이 문서는 Snyk이 Github 기반 워크플로우에 통합하는 방법을 제공합니다.

## 1단계: 환경 설정

1.  [Snyk CLI](https://docs.snyk.io/snyk-cli)를 실행하여 goof 저장소에서 git clone 명령을 실행합니다.

    ```
       git clone https://github.com/snyk/goof.git
    ```
2.  새로운 branch를 생성하고 이 branch에 취약점을 추가한 다음 변경 사항을 Github에 Pull Request로 다시 병합합니다.

    ```
       git branch add_vulns
       git checkout add_vulns
    ```

## 2단계: 오픈 소스 디펜던시 추가

복제된 goof 애플리케이션에서 **package.json** 매니페스트 파일을 검토하여 나열된 디펜던시를 확인합니다.

![](../../../.gitbook/assets/dependencies.png)

{% hint style="info" %}
이러한 디펜던시는 추가 간접 의존성을 가질 수도 있습니다.
{% endhint %}

디펜던시를 추가하려면 다음과 같이 진행합니다.

* 디펜던시 목록 맨아래의 **tinymce 4.1.0** 라이브러리를 추가합니다.

```
   {
   "name": "goof",
   ...
   }
   "dependencies" {
    ...
   "typeorm": "^0.2.24",
   "tinymce": "4.1.0"
   },
   ...
```

{% hint style="info" %}
Tip: 이전 디펜던시 뒤에 쉼표를 추가해야 합니다.
{% endhint %}

*   Node 애플리케이션에 대한 [lock file](https://docs.npmjs.com/files/package-lock.json)을 생성합니다.

    ```
    npm install --package-lock
    ```

{% hint style="info" %}
Tip: 이 파일이 이미 있는 경우 rm package-lock.json을 실행하여 제거합니다.
{% endhint %}

## 3단계: 변경 사항 commit 및 검토

* 변경 사항을 로컬에서 commit하고 로컬 git 저장소에서 변경 상태를 확인한 다음 로컬 git에 변경 사항을 추가하고 commit합니다.

```
   git status
   git add package*
   git commit -m "adding tinymce v4.1.0"
```

* 로컬 코드 변경 사항을 Github에 commit하고 파일과 기록을 Github의 업스트림 git 저장소로 전송합니다.

```
   git push --set-upstream origin add_vulns
```

```
GitHub has received your changes on your **add\_vulns** branch.
```

* Github에서 **Compare & pull request**을 클릭하여 **add\_vulns** branch를 **master** branch와 비교하고 pull request를 생성합니다.

![](../../../.gitbook/assets/click-compare.png)

## 4단계: Snyk은 pull request 검사 테스트

Snyk은 병합 프로세스에서 취약점 및 라이선스 검사에 대한 pull request를 자동으로 테스트합니다.

![](<../../../.gitbook/assets/snyk\_vuln\_lic\_check (1).png>)

PR 워크플로우가 완료되면 Snyk 프로젝트에 설정된 취약점과 라이선스 정책을 검증합니다. 정책에 따라 검사를 통과하거나 실패합니다. 해당 내용은 Gihtub에 표시됩니다.

이를 통해 보안 게이트를 설정하고 pull requests가 새로운 취약점 또는 라이선스 정책을 충족하지 않는 새로운 오픈소스 라이브러리를 소스 코드 기준에 추가하는 것을 방지할 수 있습니다.

PR 확인에 대한 자세한 내용은 [GitHub integration](../../../features/integrations/git-repository-scm-integrations/github-integration.md)문서를 참조하십시오.
