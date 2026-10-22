# 6주차 
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

