# PHP용 Snyk

하십시오.Snyk은 CLI 및 애플리케이션 UI(app.snyk.io)를 통해 취약점에 대한 보안 스캔을 제공합니다.

이 문서는 Snyk을 사용하여 PHP 프로젝트를 스캔하는 방법을 제공합니다.

## 특징

{% hint style="info" %}
**Note**\
요금제에 따라 기능을 사용하지 못할 수 있습니다.
{% endhint %}

| Package managers / Features         | <p>CLI</p><p>support</p> | <p>Git</p><p>support</p> | License scanning | Fixing | Runtime monitoring |
| ----------------------------------- | ------------------------ | ------------------------ | ---------------- | ------ | ------------------ |
| [Composer](https://getcomposer.org) | ✔︎                       | ✔︎                       | ✔︎               |        |                    |

## 작동 방식

트리를 구축한 후에는 [vulnerability database](https://snyk.io/vuln)를 사용하여 디펜던시 트리의 모든 패키지에서 취약점을 찾을 수 있습니다.

{% hint style="info" %}
**Note**\
디펜던시를 스캔하려면 먼저 관련 패키지 매니저를 설치했는지, 프로젝트에 지원되는 매니페스트 파일이 포함되어 있는지 확인해야 합니다.
{% endhint %}

Snyk이 트리를 분석하고 빌드하는 방법은 프로젝트의 언어 및 패키지 매니저와 프로젝트 위치에 따라 다릅니다. 자세한 내용은 다음 문서를 참조하십시오.

* [Snyk CLI tool for PHP projects](https://docs.snyk.io/snyk-open-source/language-and-package-manager-support/snyk-for-php)
* [Git services for PHP projects](snyk-for-php.md#git-services-for-php-projects)

## PHP 프로젝트에서 Snyk CLI 사용하기

Snyk이 트리를 분석하고 구축하는 방식은 프로젝트의 언어와 패키지 매니저에 따라 다릅니다.

디펜던시 트리를 구축하기 위해 Snyk은 디펜던시 및 해당 버전을 분석하기 위해 `composer.json` 과 `composer.lock` 파일을 분석합니다.

## **CLI parameters for PHP**

### 전제 조건

* Snyk CLI를 사용하기 전에 관련 패키지 매니저를 설치하세요.테스트 진행 이전에 Snyk에서 지원하는 관련 매니페스트 파일을 포함합니다.
* 테스트 진행 이전에 Snyk에서 지원하는 관련 매니페스트 파일을 포함합니다.
* [Snyk CLI](../../../features/snyk-cli/install-the-snyk-cli/)를 설치하고 인증하여 로컬 환경에서 프로젝트 분석을 시작합니다.

### **Parameters**

Snyk을 실행할때 PHP 전용 파라미터가 없습니다.

CLI에 대한 자세한 내용은 [Getting started with the CLI](../../../features/snyk-cli/guides-for-our-cli/getting-started-with-the-cli.md)를 참조하십시오.

## PHP 프로젝트를 위한 Git Services

PHP 프로젝트는 Snyk에서 지원하는 모든 Git Services에서 가져올 수 있습니다. 가져오기가 완료되면 Snyk은 지원하는 매니페스트 파일을 기반으로 프로젝트를 분석합니다.

가져올 프로젝트를 선택하면 다음 매니페스트 파일을 기반으로 디펜던시 트리를 빌드합니다.

* composer.json
* composer.lock

## **Git settings for PHP**

기본적으로 Snyk은 프로덕션 디펜던시를 스캔합니다. Snyk UI에서 취약점 스캔에 개발 디펜던시(`require_dev`)를 포함 여부를 구성할 수 있습니다.

### 언어 기본 설정 업데이트

1. 정에 로그인하고 관리할 관련 그룹 및 조직으로 이동합니다.
2. 설정 클릭 ![](../../../.gitbook/assets/cog\_icon.png)> **Languages**.
3. **Edit settings**를 클릭하고 **Scan dev dependencies**를 선택하여 특정 조직의 PHP 프로젝트에 대한 개발 및 프로덕션 디펜던시를 모두 포함하도록 설정합니다.
4. **Update settings**를 클릭합니다.

이 설정은 새로 가져온 모든 프로젝트에 적용되고 다시 테스트를 진행하면 모든 기존 프로젝트에 적용됩니다.

## PHP 프로젝트 문제 해결

## 오류 메시지

PHP 프로젝트로 작업할 때 다음 오류 메시지가 나타날 수 있습니다.

* composer.json or composer.lock not found in path
* Manifest file not found in path
* Lockfile missing packages property
* Lockfile or manifest file is not a valid JSON

## Support

이러한 문제나 다른 문제가 발생하는 경우 해당 파일을 [support@snyk.io](mailto:support@snyk.io)로 보내 주시면 도와드리겠습니다.

* `composer.json`
* `composer.lock`
