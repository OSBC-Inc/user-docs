# 인증되지 않은 액세스 또는 리소스가 존재하지 않습니다: Dockerhub

**문제 상황 설명**: Docker Hub에서 이미지를 가져올 때 '인증되지 않은 액세스 또는 리소스가 존재하지 않습니다.' 라는(_Unauthorized access or Resource does not exist)_ 오류와 함께 가져오기가 실패합니다.

![](../../../../.gitbook/assets/screen-shot-2021-04-28-at-2.13.11-am.png)

**해결 방법**: 그 이유는 Docker Hub 계정에서 이미지가 private이기 때문입니다. 이 문제를 해결하려면 **settings > Visibility settings** 섹션에서 이미지를 공개하십시오.

![](../../../../.gitbook/assets/screen-shot-2021-04-28-at-2.24.55-am.png)
