# PostgreSQL
> The World's Most Advanced Open Source Relational Database

세계에서 가장 진보한 오픈 소스 관계형 데이터베이스

object-relational database management system 줄여서 **ORDBMS**

무료, 객체생성이 유연, 테이블 상속

## installation
로컬로 할 경우는 brew로 설치
```bash
$ brew install postgresql
```

도커로 할 경우는 공식 이미지가 존재 [https://hub.docker.com/_/postgres](https://hub.docker.com/_/postgres)

```bash
$ docker pull postgres
```

## Usage
결국 도커로 사용하니 컨테이너 생성 방법
```bash
# 단순 생성
$ docker run -d -p 5432:5432 --name postgres -e POSTGRES_PASSWORD=password postgres

# 데이터 유지를 위해 volume
$ docker volume create pgdata

# docker run 방법
$ docker run -d -p 외부접속포트:내부접속포트 --name 컨테이너이름 -it --rm -v pgdata:data경로 -e POSTGRES_PASSWORD=비밀번호 postgres 이미지

# docker run 예시
# default port는 5432
$ docker run -d -p 5432:5432 --name postgres -it --rm -v pgdata:/var/lib/postgresql/data postgres
```

컨테이너 bash
```bash
$ docker exec -it postgres bash
#  컨테이너에서 posgres 접속
root@d63115007011:/# psql -U postgres
...
postgres=#
```
