# 빌드 및 저장소로 푸시

## AWS CodeCommit에 빌드 및 푸시

이제 애플리케이션을 AWS CodeCommit 저장소와 Amazon Elastic Container Repository에 푸시할 준비가 되었습니다.

다음은 애플리케이션 리포지토리의 새 오리진을 CodeCommit unicorn-store로 설정하고, CodeCommit에 필요한 자격 증명 도우미를 구성하고, 소스 코드를 리포지토리에 푸시합니다. CodeBuild가 이 리포지토리에서 직접 애플리케이션을 빌드하므로 이 단계는 자동화된 파이프라인에 필요합니다.

```bash
cd ~/environment/modernization-workshop/
git remote set-url origin https://git-codecommit.us-west-2.amazonaws.com/v1/repos/modernization-workshop
git config --global credential.helper '!aws codecommit credential-helper $@'
git config --global credential.UseHttpPath true
git push origin master
```

{% hint style="info" %}
성공하면 아래와 유사한 메시지가 표시됩니다.
{% endhint %}

```
Counting objects: 9525, done.
Compressing objects: 100% (5900/5900), done.
Writing objects: 100% (9525/9525), 33.75 MiB | 2.65 MiB/s, done.
Total 9525 (delta 3240), reused 9525 (delta 3240)
remote: processing 
To https://git-codecommit.us-west-2.amazonaws.com/v1/repos/modernization-workshop
 * [new branch]      master -> master
```

## ECR(Amazon Elastic Container Repository)로 푸시

이제 코드를 컴파일하고 패키징할 차례입니다. 아래 코드를 복사하여 Cloud9의 터미널 창에 붙여넣습니다.

```bash
cd ~/environment/modernization-workshop/app
docker build -t modernization-workshop .
docker tag modernization-workshop:latest $(aws ecr describe-repositories --repository-name modernization-workshop --query=repositories[0].repositoryUri --output=text):latest
eval $(aws ecr get-login --no-include-email)
docker push $(aws ecr describe-repositories --repository-name modernization-workshop --query=repositories[0].repositoryUri --output=text):latest
```

화면을 보면 터미널에 애니메이션을 적용하는 도커 이미지 빌드 프로세스가 표시되어야 합니다.

{% hint style="info" %}
성공하면 아래와 같은 메시지가 표시되어야 합니다.
{% endhint %}

```
The push refers to repository [1234567891011.dkr.ecr.us-west-2.amazonaws.com/modernization-workshop]
8d2f7b95f78d: Pushed 
82852e5eaa9d: Pushed 
9df07df94e41: Pushed 
aa90bcce39de: Pushed 
d9ff549177a9: Pushed 
latest: digest: sha256:4229b5fe142f6d321ef2ce16ff22070e410272ee140e7eec51540a823dcd315a size: 1369
```
