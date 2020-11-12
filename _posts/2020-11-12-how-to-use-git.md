---
published: true
layout: post
author: me
title: 깃 사용법
category: git
---
# How_To_Use_Git

How to use git

### 들어가기에 앞서

<○○○> 사용자가 적어줘야할 부분<br>
(○○○) 생략 가능한 부분

### 1. Git Init (Create Local Git Repository)
깃 초기화 설정
이미 했다면 안해도 됨.
```
$ cd <path_that_you_want_to_clone>
$ git init
$ git config --global user.name <username>
$ git config --global user.email <useremail>
$ git config --global --list
```

### 1-1. Authentication failed 에러
1. gitlab -> profile -> password에서 패스워드 설정
2. windows 검색에서 자격 증명 관리자
3. gitlab 항목 찾아서 그 내용을 자신의 ID와 설정한 패스워드로 바꿈
4. 재시도 (아래 링크 참고)

### 2. Clone Project
프로젝트 복사하기
```
$ cd <path_that_you_want_to_clone>
$ git remote add origin <git_project_ssh(http)_address>
$ git remote -v
$ git clone origin
```
remote add origin:
origin 변수에 git 프로젝트 주소를 저장하여 번거로움을 줄임.

### 3. Pull
프로젝트 시작 전 다른 팀원이 수정한 내용 내려받기
```
위치 확인
cd로 바탕화면-> ipdl 폴더로 들어가기 
$ git pull origin <branch_name>
```

### 4. Add, Commit, Push
자료 수정 후 커밋
```
$ git add --all
$ git commit -m "message"
$ git push origin <branch_name>
```
커밋 메시지에는 작업한 내용 요약 작성

### etc1. Branch
브랜치 리스트 확인
```
$ git branch
```
브랜치 생성
```
$ git branch <branch_name>
```
브랜치로 이동
```
$ git checkout <branch_name>
```
생성과 동시에 이동
```
$ git checkout -b <branch_name>
```

### etc2. Merge
```
$ git checkout <dest_branch>
$ git merge <src_branch>
```

### etc3. Fetch
원격 저장소의 브랜치들을 가져옴.
```
$ git fetch origin
```

### etc4. Add, Commit 취소
#### 1. Add 취소
```
$ git reset HEAD (file_name) 
```
파일 이름을 비워두면 add한 파일 전체를 취소
#### 2. Commit 취소
staged 상태 & 워킹 디렉토리 보존
```
$ git reset --soft HEAD^
```
unstaged 상태 & 워킹 디렉토리 보존
```
$ git reset (--mixed) HEAD^
```
unstaged 상태 & 워킹 디렉토리 삭제
```
$ git reset --hard HEAD^
```
Commit 메시지 변경
```
$ git commit --amend
```


## Windows에서 clone 시 Authentication failed 에러 해결

[링크](https://d2fault.github.io/2020/01/15/20200115-resolve-authentication-failure-on-git-clone/)

## GitLab 연동하기

[링크](https://tkddlf4209.blog.me/220737393340)

## GitLab with Android Studio

[링크](http://blog.naver.com/tkddlf4209/220714074459)
