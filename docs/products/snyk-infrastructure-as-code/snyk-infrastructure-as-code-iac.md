# Snyk Infrastructure as Code (IaC) 시작하기

ㅇㅁㄹGet started with Snyk IaC to inspect, find and fix issues in configuration files for Terraform or Kubernetes (including Helm) environments. For more information, see [Scan Kubernetes configuration files](broken-reference) and [Scan Terraform files](broken-reference).

{% hint style="info" %}
This article describes a process using the Snyk.io UI. For details of using IaC with the Snyk CLI, see [Broken link](broken-reference "mention").
{% endhint %}

## **Prerequisites**

Ensure you have:

* A Snyk account (go to [https://snyk.io/](https://snyk.io) and sign up - see [Create a Snyk account](https://docs.snyk.io/getting-started/getting-started-snyk-products) for details).
*
* An existing Kubernetes or Terraform environment to work in.Integrated your Git repository as for other Snyk products - see [Git repository (SCM) integrations](broken-reference) for more details.Integrated your Git repository as for other Snyk products - see [Git repository (SCM) integrations](broken-reference) for more details.For more details, see:



*
*

## Stage 1: Import projects



1.
2.
3.
4.
5.
6.

## Stage 2: View configuration file issues



Select **Projects**, then click on the imported project entry, to see information for scanned configuration files, including the number of high, medium and low severity issues found. For example:View results for configuration files in imported projects.View results for configuration files in imported projects.

![](../../.gitbook/assets/getting-started-snyk-iac-1.png)

(Issues are sorted into project types: Helm, Kubernetes and Terraform.)

Click on a project to see more information and details of the issues in a configuration file:

![](../../.gitbook/assets/getting-started-snyk-iac-2.png)

{% hint style="info" %}
If you encounter any errors during import, see [Importing projects](https://support.snyk.io/hc/en-us/sections/360000923478-Importing-projects) FAQs.
{% endhint %}

## Stage 3: View and fix config files

Act on the recommendations produced by Snyk IaC.

1.
2.
3.
4.

## For more information

See [Infrastructure as Code](https://docs.snyk.io/snyk-infrastructure-as-code).
