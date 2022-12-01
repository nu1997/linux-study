## 기본 쉘 명령어

- 매뉴얼 조회: man
    ```
    man ls
    ```
    - `/`로 검색

- 파일 목록/내용 조회 관련 명령어 ex) ls, cat, head, tail, less
    ```
    $ ls
    linux
    
    $ pwd
    /home/ubuntu

    $ cd /
    /$ ls
    bin  boot  dev  etc  home  lib  lib32  lib64  libx32  lost+found  media  mnt  opt  proc  root  run  sbin  snap  srv  sys  tmp  usr  var
    ```

- 검색/탐색 관련 명령어 ex) grep, find
  - grep
    ```
    /var/log$ grep "startup packages configure" dpkg.log
    2022-09-12 06:06:45 startup packages configure
    2022-09-12 06:08:22 startup packages configure
    2022-09-12 06:08:22 startup packages configure
    2022-09-12 06:08:30 startup packages configure
    2022-09-12 06:08:39 startup packages configure
    2022-09-12 06:08:41 startup packages configure
    2022-09-12 06:08:44 startup packages configure

    // pipeline 활용
    $ cat 123.txt | grep "boy"
    Don’t act so shy boy
    ```

  - find
    ```
    $ find == $ find /etc -print
    ```

- 압축/해체 관련 명령어 ex) tar, gzip/gunzip, zip/unizip
  - 못 보던 확장자의 압축 파일? ex) `gz`, `tar.bz`, `tar.gz`, ...
  - 압축하기 및 압축풀기

    ```
    $ ls -al > freeze.txt
    $ gzip freeze.txt 
    $ file freeze.txt.gz
    freeze.txt.gz: gzip compressed data, was "freeze.txt", last modified: Mon Nov 28 06:48:28 2022, from Unix, original size modulo 2^32 327

    $ gunzip freeze.txt.gz 
    $ file freeze.txt 
    freeze.txt: ASCII text
    ```
  - 리눅스는 확장자 개념이 없다. 따라서 확장자를 바꾸거나 이름을 변경하더라도 file type은 변하지 않는다.
  - `tar`: 파일을 연결하여 하나의 파일로 붙여준다.

- 시간 관련 명령어 ex) date, cal
    ```
    $date
    Mon Nov 28 07:24:34 UTC 2022
    $ date +%Y%m%d
    20221128
    $ cal -d 1997-02
      February 1997      
    Su Mo Tu We Th Fr Sa
                      1
    2  3  4  5  6  7  8
    9 10 11 12 13 14 15
    16 17 18 19 20 21 22
    23 24 25 26 27 28
    ```
    
- 기타 명령어 ex) echo, exit, history
    ```
    - 커맨드 기록
    $ history

    - 직전 커맨드
    $ !!

    - 쉘 종료
    $ exit
    
    - The echo command is used to display a line of text that is passed in as an argument.
    $ echo $PATH

    - which
    $ which ls
    ```

    
- 관리자 권한 실행 ex) sudo
  - 리눅스의 계정과 보안

    - 관리자 계정: root
      - 프로그램 설치 등에서 사용자 계정과 권한 다름

    - 사용자 계정: user - password
      - 관리자 권한으로 실행하기 위해 필요한 명령어: sudo

  ```
  $ sudo apt install hello
  $ hello
  Hello, world!
  ```
    
- 패키지 매니저 ex) apt(Ubuntu), yum(CentOS)
    ```
    apt list --installed
    apt install @@@
    ```
    
- 텍스트 에디터 ex) nano


### 실습
- 아이노드와 하드링크 
  - 아이노드 번호 확인
    ```
    $ ls -ali
    total 20
    258281 drwxrwxr-x 2 ubuntu ubuntu 4096 Nov 29 05:27 . 
    258157 drwxr-x--- 6 ubuntu ubuntu 4096 Nov 29 05:27 ..
    258304 -rw-rw-r-- 1 ubuntu ubuntu 1845 Nov 28 04:51 123.txt
    258306 -rw-rw-r-- 1 ubuntu ubuntu 1719 Nov 28 06:39 last.txt
    258275 -rw-rw-r-- 1 ubuntu ubuntu 1812 Nov 29 04:30 lov.txt
    ```
  - 링크 생성
    ```
    $ ln 123.txt fx.txt
    $ ln -s 123.txt s123.txt
    ```
  - 파일 상태 / 정보 조회
    ```
    $ stat fx.txt 
    * modify: change on contents
    * change: chagne on inode infos
    ```

### /etc/passwd
- 시스템에 등록된 유저 정보 목록
  ```
  root:x:0:0:root:/root:/bin/bash
  = id:pw:uid:gid:description:homedir:defaultshell
  ```

### 사용자 추가

```
$ sudo adduser ael
Adding user `ael' ...
Adding new group `ael' (1001) ...
Adding new user `ael' (1001) with group `ael' ...
Creating home directory `/home/ael' ...
Copying files from `/etc/skel' ...
New password: 
Retype new password:
passwd: password updated successfully
Changing the user information for ael
Enter the new value, or press ENTER for the default
        Full Name []: Test
        Room Number []: 123
        Work Phone []: 88888888
        Home Phone []: 97979797
        Other []: 24242424
Is the information correct? [Y/n] y

$ tail /etc/passwd
ael:x:1001:1001:Test,123,88888888,97979797,24242424:/home/ael:/bin/bash
```

### 사용자 삭제
```
$ sudo deluser ael --remove-home
```

### 그룹 + 사용자 등록 및 삭제
```
$ sudo addgroup animals
$ sudo addgroup fruits

$ sudo adduser pig --ingroup animals
$ sudo adduser dog --ingroup animals
...
```

### 권한 확인 및 수정
```
ubuntu$ su - pig
pig$ touch pig
pig$ ls -al
-rw-r--r-- 1 pig  animals    0 Dec  1 17:29 pig

chmod 644 pig
chmod g+w pig
...
```
홈 디렉토리 접근을 위해서는 기본적으로 사용자가 같은 그룹에 속해있어야 한다. (설정 변경 가능)