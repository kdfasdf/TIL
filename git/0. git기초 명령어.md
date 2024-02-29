### 원격 저장소 연결 및 삭제
```
git add init                                      # 깃 저장소 생성
git remote add [원격 저장소 이름] [원격 저장소 URL] # 원격 저장소 연결, 하나만 연결할 경우 저장소 이름은 보통 origin으로 많이 쓴다
git remote -v                                     # 연결된 원격 저장소들을 이름과 주소를 함께 나열한다
git remote remove [원격 저장소 이름]               # 선택된 이름의 원격 저장소 연결을 끊음
git remote rename [기존이름] [변경할 이름]         # 원격 저장소의 이름을 변경
```

### 원격 저장소에 업로드
```
git add [올릴 폴더 혹은 파일 명(전부 올리려면 .)] # 파일 인덱스(staging area)에 올리기
git commit -m "커밋 내용"                       # 로컬 저장소에 올리기
git push origin main                           # 원격 저장소에 올리기(깃의 기본 브랜치 명이 master에서 main으로 바뀜)
```
