# labels를 사용하여 Dockerfile과 이미지를 자동으로 연결

Snyk allows you to manually or automatically link from a Dockerfile to all container images built from it. You can use this to understand the security impact on your running applications, and understand which images can be better secured, or need to be rebuilt, when taking action and updating the Dockerfile base image.

## 연결된 이미지 보기

This information appears in the **LINKED IMAGES** section of the details for a project:

![](../../../.gitbook/assets/mceclip3.png)

You can get automatic links between imported images (via container registry integration) to existing Dockerfile projects. This is done by checking whether the OCI label in the image matches the path of a Dockerfile that exists in the org in Snyk.

## 작동 방식

At the point of import (or re-test), the image is analysed, scanned for vulnerabilities and image labels are also retrieved from image manifest. Snyk then checks whether:

* Image labels defining dockerfile location exist:
  * `org.opencontainers.image.source` - URL to the project repo (mandatory)
  * `io.snyk.containers.image.dockerfile` - path to Dockerfile, e.g.: "/Dockerfile-prod" (optional)
* Dockerfile project exists in the same org, with a matching repo (and path or /Dockerfile) from the image labels

If the above applies, Snyk automatically creates a link between the image and dockerfile projects.

## 연결 자동 업데이트/제거

Links are automatically updated if the Dockerfile labels are updated and are targeting new location. This can happen at the time of retest or when a recurring test runs.

Links are removed if either the image project or Dockerfile project are deleted, if the Dockerfile labels are updated so that they target Dockerfile location without an existing project in Snyk, or if the Dockerfile labels are removed.

## 중개된 SCM 통합으로 연결

For a link to be created, Snyk needs to be able to map the Dockerfile repository URL to the right SCM org source. For brokered integrations this is a bit more complex, as this URL is not available by default.

To create automatic links between container images to Dockerfiles stored in brokered SCMs, enter the URL in the integration page settings:

![](../../../.gitbook/assets/mceclip0-4-.png)

Once available, Snyk can use that for linking generation.
