GIT
=====

### 초기 설정
```
git config --global user.name ""
git config --global user.email ""
```

### 소스 추가 및 커밋
```
git init
git add -A 
git add README.md
git add .
git commit -m "first commit"
```

### 원격 리포지토리 생성 및 브랜치 생성
```
git remote add origin https://github.com/id/project.git
git push -u origin master (origin: 원격 리포지토리, master: 브랜치명)
```

### 브랜치 복제
```
git clone master https://github.com/id/project.git
git log
```

### 브랜치 변경
```
git checkout -b branch01
git checkout -b branch01 origin/branch
```

### 상태 확인
```
git status
```

### 원격 브랜치에서 가져오기
```
git pull origin <branch_name>
```

### 원격 브랜치에 반영하기
```
git push origin <branch_name>
```

### 로컬에서 브랜치 삭제
```
git branch -D <old_name>
```

### 원격 브랜치 삭제
```
git push origin --delete <old_name>
```

### 로컬에서 브랜치명 수정
```
git branch -m <new_name>
```

### 수정된 브랜치를 원격에 반영
```
git push origin -u <new_name>
```

### 브랜치 리스트 동기화
```
git fetch -p
```

### 브랜치 리스트 확인
```
git branch -a
```

### 원격 리포지토리 확인
```
git remote
```

