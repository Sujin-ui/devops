# 6주차
## 이미지 주소 
- GitHub Container Registry 이미지 경로 
	- ghcr.io/Sujin-ui/guestbook:v1
- 친구 이미지 실행한 결과
	-  ghcr.io/ericlair/guestbook:v1
``` 
docker run -d -p 8081:5000 --name friend_guestbook ghcr.io/[친구_계정명]/[이미지명]:[태그]
```
## 도커파일의 각줄이 하는일 
- 사용된 각 지시어의 역할과 의미 
``` 
FROM ghcr.io/ericlair/inhatc-devops-guestbook:v1
ENV APP_TITLE="방명록" THEME_COLOR="#7C9A82"
```
FROM ghcr.io/ericlair/inhatc-devops-guestbook:v1
- 새로 만들 이미지를 위한 베이스 이미지를 지정합니다 
외부저장소에 올려진 방명록 기본 실행 환경을 가져와 시작점으로 사용 

ENV APP_TITLE="방명록" THEME_COLOR="#7C9A82"
- 컨테이너 내부 애플리케이션에 사용할 환경변수의 기본값을 설정 
- 상단의 타이틀을 '방명록'지정후 메인 테마 색상을 지정 

## 빌드캐시가 동작한 로그 
- 동일한 Dockerfile로 이미지를 다시 빌드할 경우 도커는 이전에 빌드한 레이어 재사용
- 즉 속도 올림

``` 
$ docker build -f Dockerfile.custom -t guestbook:custom .

[+] Building 0.2s (6/6) FINISHED                                        docker:default
 => [internal] load build definition from Dockerfile.custom                       0.0s
 => => transferring dockerfile: 110B                                              0.0s
 => [internal] load .dockerignore                                                 0.0s
 => CACHED [1/2] FROM docker.io/library/guestbook:v1                              0.0s
 => CACHED [2/2] ENV APP_TITLE=방명록 THEME_COLOR=#7C9A82                         0.0s
 => exporting to image                                                            0.0s
 => => naming to docker.io/library/guestbook:custom  
```
	- 기존에 처리된 From 구문과 Env 레이어가 변경 ❌
	- 새로 빌드 안하고 캐시를 활용해 빠르게 빌드가 완료
## 설정 넣는 세가지 방법 및 차이점 요약 
| 구분 | 코드 내 하드코딩 | Dockerfile의 ENV | docker run -e 옵션 |
| ---|---|---|---|
|설정 시점 | 소스코드 작성시점 | 이미지 빌드시점 | 컨테이너 실행시점 |
|유연성 | 매우낮음 | 보통 | 매우높음 |
|우선순위|가장낮음 | 중간 | 가장높음 |

- 요약 
	- 환경변수 우선순위는 코드 기본값 < Dockerfile ENV < Docker run -e 순서입니다 
	- Dockerfile의 ENV는 기본설정값을 정의하기 적합
	- 

### Dockerfile 
- 이미지 빌드 방법을 코드로 정의하는 레시피 
	- RUN = 이미지 만들때 
	- CMD = 컨테이너 켤 때 
	- EXPOSE = 사용할 포트 정보 선언 
- 설정 우선 순위 
	- 코드기본값 < ENV < docker run -e 
	- 레이어 캐시 : 자주 바뀌는것 -> 뒤 

### 베포흐름 
- build -> tag -> push -> <타사용자> pull -> run 


