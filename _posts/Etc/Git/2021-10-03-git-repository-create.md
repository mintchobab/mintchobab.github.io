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

Repository를 만드는 방법은 2가지가 있다.

  1. 아직 버전관리를 하지 않는 로컬 디렉토리 하나를 선택해서 Git 저장소를 적용하는 방법
  2. 다른 어딘가에서 Git 저장소를 Clone 하는 방법

<br>
Repository를 만들기 위해서는 git 명령어를 사용할 수도 있고 github를 이용해서 만들 수도 있다.
아래명령어들을 순서대로 진행해보자

<br>

### 로컬 저장소 만들기

기존 프로젝트의 폴더 위치를 이동하거나 새로운 폴더를 하나 생성한다. 폴더를 생성하기 위해서는 마우스 우클릭을 통해 직접 생성을 해도 되고 명령어를 이용해서 생성해도 된다.
- 현재 위치에 폴더 생성
    ```
    mkdir [생성할 폴더 이름]

    ex) mkdir TestFolder
    ```


폴더 생성이 완료됐다면 해당 폴더로 이동한다.
  <br>

  - 폴더 이동
    ```
    cd [폴더명1/폴더명2/폴더명3]

    ex) cd C:/Users/User/Desktop/TestFolder
    ```

  <br>

git init 명령어를 사용하여 해당 폴더를 로컬 Repository로 만든다.
  - git init
    ```
    git init
    ```






    

