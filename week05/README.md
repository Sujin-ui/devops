## Nginx 컨테이너 3개 실행 실습

### 접속 주소
- nginx1: http://localhost:8091
- nginx2: http://localhost:8092
- nginx3: http://localhost:8093

### curl 확인 결과
- nginx1: Welcome to nginx1
- nginx2: Welcome to nginx2
- nginx3: Welcome to nginx3

### 실행 화면
- nginx1: images/nginx1.png
- nginx2: images/nginx2.png
- nginx3: images/nginx3.png
- Docker 실행 목록: images/docker-ps.png

#5주차 Docker 

## 하이퍼바이저 vs 컨테이너 
### 하이퍼바이저 
``` 
┌────────하이퍼바이저 방식 ──────┐
│ 앱A │ 앱B │ 앱C │
│ Guest OS │ Guest OS │ Guest OS │
├──────────┴──────────┴──────────┤
│ 하이퍼바이저 (VMware) │
├────────────────────────────────┤
│ 호스트 OS (Windows) │
├────────────────────────────────┤
│ 하드웨어 │
└────────────────────────────────┘
무겁다 (VM마다 Guest OS 필요)
상대적으로 느린 시작
이미지 크기가 크다 (기가바이트 단위)
강한 격리

```
### 컨테이너 
```
┌────────── 컨테이너 방식 ──────────┐
│ 앱A │ 앱B │ 앱C │
├──────────┴───────────┴────────────┤
│ Docker 엔진 │
├───────────────────────────────────┤
│ 호스트 OS (커널 공유) │
├───────────────────────────────────┤
│ 하드웨어 │
└───────────────────────────────────┘
커널 공유
일반적으로 빠르게 시작
이미지 크기가 작다 (메가바이트 단위)
프로세스 수준으로 격리

```
- namespace 
	- 시야 격리 - "안 보이게 만들기"
		- 프로세스 
		- 네트워크 
		- 마운트 
	** 서로 연결이 안된게 ❌ 통신 ⭕ 훔쳐보기 ❌ **
- cgroup
	- 자원 사용량 제한 및 관리 - " 많이 못 쓰게 만들기 "
		- 메모리 cgroup
		- CPU chroup
- 커널 공유 
	- 컨테이너가 윈도우 맥 OS 커널을 직접 공우 하는것이 아님
### 이미지 Vs 컨테이너 
```

[이미지] ────실행────▶ ([컨테이너]
(붕어빵 틀) 		     (붕어빵)
- 읽기 전용              - 실행, 정지할 수 있는 인스턴스
- 실행 중 변경되지 않음	  - 쓰기 가능, 정지 후에도 파일은 유지, 컨테이너 삭제 시 쓰기 계층이 사라짐
- 1개 			         - N개 찍기 가능

[참고]
클래스(class) ───────▶ 객체(instance) 
```
### Registry 
- 레지스트리 = 이미지 창고 
```
[Docker Hub / ghcr.io] (이미지 저장소)
 │ 			     ▲
docker pl     docker push
 ▼  		     |
 [내 컴퓨터: 내가 만든 이미지]
   └ ── docker run ──▶ [컨테이너] 


```
### Registry 
docker run -d -p 8080:80 --name web nginx 
	# -d (detached) : 백그라운드 실행 
	# -p (publish)  : 포트연결 
	# --name	: 컨테이너 이름 지정 
	# nginx  	: 이미지 이름
docker ps     # 컨테이너 출력 
docker images # 이미지 확인 
docker logs <컨테이너 이름>    # 로그 보기 
docker stop <컨테이너 이름>    # 컨테이너 정지하기 
docker start <컨테이너 이름>   # 컨테이너 시작
docker restart <컨테이너 이름> # 컨테이너 재시작
docker rm -f <컨테이너 이름>   # 실행중이여도 삭제 
docker exec -it <컨테이너 이름> bash 
	# -it (interactive+tty)
	# bash 컨테이너 안에 실행할 명령 (셸)


