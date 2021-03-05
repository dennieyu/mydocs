GIT
=====

## 1. 최초 설정

### 사용자 정보
```
git config --global user.name ""
git config --global user.email ""
```

## 2. 저장소 관리

### 기존 디렉토리를 저장소로 만들기
```
git init
```

### 원격지 저장소 생성 및 브랜치 생성
```
git remote add origin https://github.com/id/project.git
git push -u origin master
```
- `origin`: 원격지 저장소명
- `master`: 브랜치명

### 원격지 저장소 확인
```
git remote
```

### 기존 저장소를 복제
```
git clone master https://github.com/id/project.git
git log
```

## 3. 파일 버전 관리

### 소스 추가 및 커밋
```
git add -A 
git add README.md
git add .
git commit -m "first commit"
```

### 상태 확인
```
git status
```

### 원격지 브랜치에서 가져오기
```
git pull origin <branch_name>
```

### 원격지 브랜치에 반영하기
```
git push origin <branch_name>
```

### 수정된 브랜치를 원격지에 반영
```
git push origin -u <new_name>
```
- `-u` 옵션은 현재 브랜치를 자동으로 origin이라는 원격지 저장소의 master 브랜치에 연결. 연결 후 `git push`, `git pull` 단축 명령어 사용 가능함.

## 4. 브랜치 관리

### 브랜치 전환
```
git checkout -b <branch_name>
```
- `-b` 옵션을 넣으면 브랜치 작성과 체크아웃을 한꺼번에 실행함.

### 브랜치 리스트 동기화
```
git fetch -p
```
### 원격지 브랜치 삭제 (방법 #1)
```
git push origin --delete <old_name>
```

### 원격지 브랜치 삭제 (방법 #2)
```
git branch -d <old_name>
git push origin <old_name>
```

### 로컬에서 브랜치 삭제 (merge하지 않은 커밋이 있으면 삭제 불가)
```
git branch -d <old_name>
```

### 로컬에서 브랜치 삭제 (대문자 -D 옵션은 강제 삭제)
```
git branch -D <old_name>
```

### 로컬에서 브랜치명 수정
```
git branch -m <new_name>
```

### 브랜치 리스트 확인
```
git branch -a
```
