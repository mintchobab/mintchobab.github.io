---
title: Git 명령어

categories:
  - Git
tags:
  - [Git]

toc: true
toc_sticky: true

date: 2021-09-30
last_modified_at: 2021-09-30
---


### help

  - 명령어의 모음을 볼 수 있다.---
    ```
    git help
    ```
  <br>

  - 사용할 수 있는 git 명령어들의 전체 리스트 확인---
    - 많은 내용이 나오기 떄문에 도중에 리스트 보기를 멈추고 싶으면 'q'를 누르면 된다.

    ```
    git help -a
    ```

  <br>
  
  - 특정 명령어의 자세한 내용 보기 (메뉴얼 페이지로 연결)
    ```
    git help [명령어 이름]

    ex) git help commit
    ```


<br>


### config

Git을 설치한 후에 사용환경을 설정하고 확인하는 명령어들이다.
<br>
설정은 최초 1회만 하면 되고, 설정한 내용은 Git을 업그레이드 해도 유지 된다.

  - zzz
    ```
    git config
    ```

  <br>

  - 설정된 정보들의 리스트를 보여준다.
    ```
    git config --list
    ```

  <br>

  - 특정 key에 대해 어떤 값을 사용하는지 확인할 수 있다.
    ```
    git config [key]

    ex) git config user.name
    ```

  <br>

  - 사용자의 이름과 이메일 주소를 설정한다.
    ```
    git config --global user.name "MyName"
    git config --global user.email "MyEmail@example.com"
    ```

<br>

### 저장소 만들기




