# Most used Docker Commands
자주 사용하는 도커 커맨드

## Image
```bash
# Docker Hub 저장소에 로그인, 로그아웃
$ docker login
$ docker logout

# Docker Hub 저장소에서 이미지를 가져옴
$ docker pull [image:version]

# 모든 이미지 리스트
$ docker images

# 컨테이너를 생성하지만 시작하지는 않음
$ docker create [image]

# 이미지 빌드
$ docker build --tag [image-tag] --file [path]

# 이미지 삭제
$ docker rmi [image]

# 모든 이미지 삭제
$ docker rmi $(docker images -q)

# 모든 이미지 강제 삭제
$ docker rmi $(docker images -q) -f
```

## Container
```bash
# 실행 중인 컨테이너 리스트
$ docker ps

# 모든 컨테이너 리스트
$ docker ps -a

# 새 컨테이너 시작
$ docker run [options] [image:version]
# [options]
# -d: detach 백그라운드에서 시작
# -it [] []: 쉘 + 명령어
# --name [name]: 컨테이너 이름
# -p [host-port]:[docker-port]: 특정 포트 매핑
# -P 모든 포트 매핑
# --rm: 종료 후 제거

# 정지되어있는 컨테이너 시작
$ docker start [container]

# 컨테이너 안에서 커맨드 실행
$ docker exec [container] [command]

# 컨테이너 로그 확인
$ docker logs [container]

# 컨테이너 정지
$ docker stop [container]

# 컨테이너 삭제
$ docker rm [container]

# 모든 컨테이너 삭제
$ docker rm $(docker ps -aq)
```
