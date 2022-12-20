# 설정

## 세션 관리자에 비밀번호 저장

다음 명령을 실행하여 `abc123`을 **고유한 토큰**으로 바꿉니다. 그러면 세션 매개변수 관리자에 토큰이 배치됩니다.

```
aws ssm put-parameter --name "snykAuthToken" --value "abc123" --type SecureString
```

## 애플리케이션 스캔 설정

`maven`이 애플리케이션을 빌드한 후 **Snyk**에 테스트를 삽입하려고 합니다. 가장 간단한 방법은 Mvn이 애플리케이션/종속성 트리를 구축한 후 **Snyk** 명령을 다운로드, 권한 부여 및 실행하는 명령을 삽입하는 것입니다.

`modules/snyk/Dockerfile`에서 이러한 작업을 수행하기 위해 다음 명령을 삽입했습니다.

`docker build`명령에 전달된 값에서 환경 변수를 설정합니다. 여기에는 **Snyk**용 토큰이 포함됩니다. **Snyk**은 환경 변수를 사용하여 토큰을 사용할 때 자동으로 감지합니다.

```
#~~~~~~~SNYK Variable~~~~~~~~~~~~
# Declare Snyktoken as a build-arg
ARG snyk_auth_token
# Set the SNYK_TOKEN environment variable
ENV SNYK_TOKEN=${snyk_auth_token}
#~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
```

**Snyk**을 다운로드하고 테스트를 실행하여 중간에서 높은 심각도 문제를 찾고 빌드가 성공하면 모니터링 및 보고를 위해 결과를 **Snyk**에 게시합니다. 새로운 취약점이 발견되면 알림을 받게 됩니다.

```
# package the application
RUN mvn package -Dmaven.test.skip=true

#~~~~~~~SNYK test~~~~~~~~~~~~
# download, configure and run snyk. Break build if vulns present, post results to `https://snyk.io/`
RUN curl -Lo ./snyk "https://github.com/snyk/snyk/releases/download/v1.210.0/snyk-linux"
RUN chmod -R +x ./snyk
#Auth set through environment variable
RUN ./snyk test --severity-threshold=medium
RUN ./snyk monitor
```

## Docker Scanning 설정

빌드 프로세스의 후반부에 도커 이미지가 생성됩니다. 취약점을 분석하고자 합니다. 우리는 이것을 `buildspec.yml`에서 할 것입니다. 먼저 `parameter store`에서 **Snyk** 토큰 `snykAuthToken`을 가져옵니다:

```
env:
  parameter-store:
    SNYK_AUTH_TOKEN: "snykAuthToken"
```

`prebuild` phase 단계에서 Snyk를 설치합니다.

```
phases:
  pre_build:
    commands:

      - PWDUTILS=$(pwd)
      - curl -Lo ./snyk "https://github.com/snyk/snyk/releases/download/v1.210.0/snyk-linux"
      - chmod -R +x ./snyk
```

`build` 단계에서 토큰을 **docker compose** 명령에 전달하여 이전에 애플리케이션을 테스트하기 위해 설정한 Dockerfile 코드에서 토큰을 검색합니다:

```
build:
    commands:
      - docker build --build-arg snyk_auth_token=$SNYK_AUTH_TOKEN -t $REPOSITORY_URI:latest .
```

다음으로 생성된 Docker 이미지를 테스트하기 위해 **Snyk** 인스턴스에 **권한**을 부여합니다. 통과하면 모니터링 및 보고를 위해 결과를 **Snyk**에 전달합니다.

```
build:
    commands:
      - $PWDUTILS/snyk auth $SNYK_AUTH_TOKEN
      - $PWDUTILS/snyk test --docker $REPOSITORY_URI:latest
      - $PWDUTILS/snyk monitor --docker $REPOSITORY_URI:latest
      - docker tag $REPOSITORY_URI:latest $REPOSITORY_URI:$IMAGE_TAG
```

터미널에서 다음 폴더로 **이동**합니다:

```
cd ~/environment/aws-modernization-workshop/
```

이 모듈을 시도하기위해 **Snyk** 버전을 빌드에 복사해 보겠습니다:

```
cp modules/snyk/Dockerfile modules/containerize-application/Dockerfile
cp modules/snyk/buildspec.yml buildspec.yml
```
