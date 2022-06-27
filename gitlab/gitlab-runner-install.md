## 오늘 찾아본 링크

[gitlab runner 설치 방법](https://sangchul.kr/101)

## 공부한 내용

### gitlab cicd runner

gitlab runner를 설치하는 방법에 대해 공부했다.

gitlab runner는 다양한 방법으로 설치할 수 있다. 나는 docker를 활용해서 설치를 했다.

docker 기반으로 설치를 하게되면 dind 기반으로 되어 다양한 컨테이너 이미지를 설치하여 다양한 환경에서 CI를 진행할 수 있다.

gitlab runner설치하는 방법은 다음과 같이 간단하다.

1. 도커 명령어로 컨테이너 실행하기

```
docker run --detach \
--name gitlab-runner \
--restart always \
--volume /var/run/docker.sock:/var/run/docker.sock \
gitlab/gitlab-runner:latest
```

2. 도커 컨테이너 내부로 들어간다.

```
docker container exec -it  gitlab-runner bash
```

3. 다음 명령어를 실행한다.

```
gitlab-runner register -n \
--url https://gitlab.com/ \
--registration-token [runner token] \
--description gitlab-runner \
--executor docker \
--tag-list "<tag>"
--docker-image docker:latest \
--docker-volumes /var/run/docker.sock:/var/run/docker.sock
```
