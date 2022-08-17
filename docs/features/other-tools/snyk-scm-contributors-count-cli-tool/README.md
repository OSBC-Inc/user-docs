# Tool: Snyk-SCM- Contributors-Count

## 이 Tool은 무엇을 합니까?

이 Tool은 다음 SCM에 대해 지난 90일 동안의 기여자 수 요약을 계산하고 출합니다:

* Azure Devops
* Bitbucket Cloud
* Bitbucket Server
* GitHub
* GitHub Enterprise
* GitLab
* GitLab Server

{% hint style="info" %}
명명 규칙과 관련하여 SCM 간에 약간의 차이가 있습니다. 예를 들어 GitHub의 "Orgs"는 Azure의 "Projects"이고 Bitbucket의 "Workspaces"일 수 있습니다. 이러한 차이점은 Tool이 각 SCM에 대해 허용하는 command에 반영됩니다.
{% endhint %}

## **How the SCM-Contributors-Count tool works**

The tool works in two modes: **Scoping usage prior to onboarding** and **Snyk License Consumption.**

* **Scoping usage prior to onboarding:** For users who want to onboard to Snyk and would like to get an estimate of the developer count across their SCMs.\
  In this mode, the tool fetches all the information directly from the SCMs, using the credentials provided by the user.
* **Snyk License Consumption (valid only for Bitbucket and Azure):** For users with an existing Snyk account, who want some clarity and details about their license consumption (number of contributors, names, email, and so on).\
  In this mode, the tool fetches the SCM-related projects monitored by Snyk and then matches those to the repos on the SCM and counts the contributors only for those repos/projects.

## Downloading the tool

Run the following:

```
npm i -g snyk-scm-contributors-count
```

You can also get the binaries from the [release page](https://github.com/snyk-tech-services/snyk-scm-contributors-count/releases).
