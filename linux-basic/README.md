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
    
- 패키지 매니저 ex) apt
    ```
    
    ```
    
- 텍스트 에디터 ex) nano
    ```
    
    ```
    