---
title: "[Git] Repository 만들기"

categories:
  - Git
tags:
  - [Git]

toc: true
toc_sticky: true

date: 2021-10-03
last_modified_at: 2021-10-03
---


## Git Repository

Repository란 프로젝트에 사용될 파일이나 폴더를 저장해 두는 곳이다.<br>

Local Repository와 Remote Repository로 나눌 수 있다.<br>
- Local Repository (로컬 저장소) : 내 PC에 파일이 저장되는 개인 저장소 
- Remote Repository (원격 저장소) : 파일이 서버에서 관리되며 여러 사람이 함께 사용하기 위한 저장소

<br>

![local and remote](/assets/images/git/local.png)


<br><br>

## Repository 만들기
<br>

Repository를 만드는 방법은 2가지가 있다.

  1. 아직 버전관리를 하지 않는 로컬 디렉토리 하나를 선택해서 Git 저장소를 적용하는 방법
  2. 다른 어딘가에서 Git 저장소를 Clone 하는 방법

<br>

### 디렉토리를 Git 저장소로 만들기
<br>

먼저 로컬 저장소로 사용하기 위한 디렉토리를 하나 생성한다. 윈도우 환경에서 원하는 경로에 마우스 우클릭을 통해 새로운 디렉토리를 생성해도 되고, 아래와 같이 `mkdir` 명령어를 통해 디렉토리를 생성해도 된다.
명령어를 사용해서 디렉토리를 생성하려면 아래의 cd 명령어를 통해 원하는 경로로 이동한 후 `mkdir` 명령어를 사용해야 한다.


- 현재 위치에 디렉토리 생성
    ```
    mkdir [생성할 디렉토리 이름]

    ex) mkdir TestFolder
    ```

<br>

디렉토리 생성이 완료됐다면 해당 디렉토리로 이동한다.
  <br>

  - 디렉토리 이동
    ```
    cd [디렉토리명1/디렉토리명2/디렉토리명3]

    ex) cd C:/Users/User/Desktop/TestFolder
    ```

<br>

생성된 디렉토리를 로컬 Repository로 만든다. `git init` 명령어를 사용하게 되면 .git이라는 하위 디렉토리가 생성된다.
  - git init
    ```
    git init
    ```

<br>

### 기존 저장소를 Clone하기

Clone 명령어를 사용하면 원격 서버에 있는 Repository를 복사해서 사용할 수 있다.
먼저 cd 명령어를 통해 Repository를 저장할 위치로 이동한 후 아래 명령어를 실행한다.
  - git clone
    ```
    git clone [url]

    ex) git clone https://github.com/libgit2/libgit2
    ```

<br>

여기까지 Repository를 만드는 방법에 대해서 알아보았다. 하지만 아직은 프로젝트의 파일들이 git에 의해 관리되는 상태가 아니다. 
다음 포스트에서 commit을 통해 레포지토리내의 파일의 추가, 삭제, 수정 등의 변경사항을 관리하는 방법에 대해서 알아보자.

<br>
<br>

## 자료 출처
> https://git-scm.com/book/ko/v2










    

