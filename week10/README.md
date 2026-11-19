# 10 주차 
- 구조 
guestbook/
├── app.py, Dockerfile, compose.yaml ...
└── k8s/
├── deployment.yaml 
└── service.yaml 

## git revert 
- 과거 커밋 기록을 삭제 하지 않고 변경사항을 취소 
```
    A -> B -> C (HEAD)
```
-  B의 변경사항을 취소하고 싶을떄 
```
    git revert B 
```
- 결과 
```
    A -> B -> C -> D (HEAD)
                   ^
                   |
        " B의 변경을 취소한 커밋 "
```
    - B 와 C는 남아있고 B의 변경사항을 되돌리는 D가 추가

## git reset 
- 커밋 기록의 기준점을 과거로 되돌리는것 
```
git reset --soft
    - HEAD로 이동하되, 변경사항은 스테이지 영역에 유지

git reset --hard
    - HEAD로 이동하되, 작업 파일까지 대상 커밋 상태로 변경 
```
*git revert- 잘못 작성한 내용을 취소한 기록을 새로 남기는 것*
