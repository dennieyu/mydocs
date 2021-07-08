TOOL
=====

개발 환경 툴

Flyway
=====

- [**(출처) Flyway 로 Java 에서 DB schema, seed 관리하기/강남언니 공식 블로그**](https://blog.gangnamunni.com/post/introducing-flyway)

- DB schema 를 코드로 관리한다는 것

   - 목표
      - 현재 DB schema 를 코드로 옮긴다
      - 앞으로 DB schema 변경을 코드로 관리한다
      - 배포 시에 Flyway 를 이용해 DB migration 을 수행한다
      - local 환경 작업을 위한 seed 를 코드로 관리한다

   - 작업
      - Flyway 설치 및 설정
      - 현재 DB schema 를 기준으로 migration 파일 생성
      - seed 파일 생성

Docker compose
=====

- [**(출처) Docker Compose 로 local 개발 환경 쉽게 관리하기/강남언니 공식 블로그**](https://blog.gangnamunni.com/post/docker-compose-for-local-env)
      
- Docker Compose 는 간단하게 여러 Docker application 들을 어떻게 실행할지 정의하고 실행할 수 있는 툴이다.

- 예제

```
# docker-compose.yml

version: '3'

services:
  database:
    image: mysql:5.7.27
    ports:
      - 43306:3306
    environment:
      MYSQL_ROOT_PASSWORD: password
    command: [ '--character-set-server=utf8mb4', '--collation-server=utf8mb4_unicode_ci' ]
	redis:
    image: redis:5.0.5
    ports:
      - 46379:6379
  influxdb:
    image: influxdb
    ports:
      - 48086:8086
```

- 장점
   - 띄우고 내리는 등의 행위가 편하다
   - Docker 환경이 파일로 관리된다
   - 협업 하는 모두가 명령어 하나로 쉽게 같은 환경을 사용할 수 있게 된다

