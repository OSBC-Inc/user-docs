# Ruby용 Private Gem Sources

## **개요**

{% hint style="info" %}
**Note**\
이 기능은 현재 기능 플래그 뒤에 있습니다. [지원 팀에 문의](https://support.snyk.io/hc/en-us/requests/new)하여 조직에서 사용할 수 있도록 하십시오.
{% endhint %}

개인 Gem이 호스팅되는 위치를 Snyk에 알려주는 구성을 추가할 수 있습니다. 이것은 일반적으로 Bundler 환경 변수로 추가하는 것과 동일한 정보입니다.

일단 구성되면 Snyk는 이 정보를 사용하여 Pull/Merge 요청을 생성할 때 Bundler가 잠금 파일을 재생성하기 위해 해당 dep에 도달할 수 있도록 허용하여 개인 종속성에 액세스합니다.

이 가이드는 Snyk UI 통합에만 해당되며 CLI는 추가 구성 없이 비공개 레지스트리가 있는 Ruby 프로젝트를 지원합니다.

## 구성

1. settings ![](../../../.gitbook/assets/cog\_icon.png) > **General**로 이동합니다.
2. `RubyGems Bundler environment variables`섹션 찾기(아래 참조)
3. 환경 변수 이름과 값을 추가하여 gem 소스에 대한 자격 증명을 정의합니다(일반적으로 개발자 컴퓨터 및/또는 CI 환경에서 설정한 값과 동일함). 예: 이름: `BUNDLE_GITHUB__COM`, 값: `abcd0123generatedtoken:x-oauth-basic`
4. 이제 테스트해 보세요. 비공개 레지스트리의 gem이 포함된 프로젝트에서 Pull/Merge Request을 열어 잠금 파일이 업데이트되고 Snyk Fix Pull Request에 포함되었는지 확인하세요.

![](../../../.gitbook/assets/94445628-8fdd3980-019f-11eb-816e-2c61c5b99c5c.png)

## 요구 사항

* 변수 값은 CGI로 이스케이프되어야 합니다.
* 보석 소스는 https URL을 사용해야 합니다. 예: \
  **지원됨**: `gem "privvy", git: "https://github.com/testexample/ruby-gem-for-private-source"` \
  **지원되지 않음:** `gem "privvy", git: "git@github.com:testexample/ruby-gem-for-private-source"`
* 보석 소스는 공개적으로 확인할 수 있어야 합니다(예: 방화벽 뒤에 있지 않아야 함).
* [Gem Sources 문서에 대한 공식 번들러 자격 증명](https://bundler.io/v1.16/bundle\_config.html#CREDENTIALS-FOR-GEM-SOURCES)에 따라 변수를 구성해야 합니다.
