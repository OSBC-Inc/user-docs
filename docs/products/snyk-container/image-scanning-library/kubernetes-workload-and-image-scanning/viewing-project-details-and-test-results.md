# 프로젝트 세부 정보 및 테스트 결과 확인

모니터링하기 위해 가져온 모든 워크로드는 Kubernetes 아이콘이 표시된 프로젝트 페이지에 나타납니다.

![Kubernetes icon](../../../../.gitbook/assets/uuid-24e0b69a-01c3-9434-9dac-9b44864bd269-en.png)

워크로드 테스트 결과를 보고 작업하려면 다음과 같이 진행합니다.

* **Projects** 페이지로 이동하여 Kubernetes 프로젝트에 대해서만 필터링합니다.

![](../../../../.gitbook/assets/uuid-08d7978e-0c64-a8c2-c289-402534ebec42-en.png)

확인하려는 항목을 펼칩니다.

* 워크로드에 사용하는 개별 이미지 목록입니다.
* 각 이미지의 취약점 수를 요약합니다.

이미지 기록을 포함하여 이미지에 대한 취약점을 자세히 확인하려면 이미지 이름을 클릭합니다. 선택한 이미지에 대한 프로젝트 세부 정보 페이지가 나타납니다.

![](<../../../../.gitbook/assets/image (59) (2) (3) (3) (3) (3) (4) (5) (5) (5) (4) (7).png>)

* To view an aggregate list of the vulnerabilities in all of the images in the workload, along with details about the security posture of the workload configuration, click the workload link. The Project details page loads for the selected image similar to the following example:

![](../../../../.gitbook/assets/uuid-79e06589-b59c-4bad-30e4-56c0e15607e0-en.png)

Currently, we test the workload configuration for the following properties:

| **Snyk parameter**     | **Associated Kubernetes parameters**         | **Description**                                                                                                                                                                                                                                                                                                                     |
| ---------------------- | -------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| CPU and Memory limits  | Resources.limits.memory resources.limits.cpu | Limiting the expected CPU and Memory available to the container has operational as well as security benefits. In the context of security, this is about limiting the impact of potential denial of service attacks to affecting the app rather than the node and potentially the whole cluster.                                     |
| runAsNonRoot           | securityContext.runAsNonRoot                 | By default, containers can run as the root user. This property prevents that at the container runtime, meaning an attacker would only have limited permissions if they were to be able to execute a command in the context of the container.                                                                                        |
| readOnlyRootFilesystem | securityContext. readOnlyFilesystem          | By default the file system mounted for the container is writable. That means an attacker who compromises the container can also write to the disk, which makes certain kinds of attacks easier. If your containers are stateless then you don’t need a writable filesystem.                                                         |
| Capabilities           | securityContext.capabilities                 | At a low-level, Linux capabilities control what different processes in the container are allowed to do: from being able to write to the disk, to being able to communicate over the network. Dropping all capabilities and adding in those that are required is possible but requires understanding the list of capabilities first. |
