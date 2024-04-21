# Environment variable
##### 원작자: 문광일 PM
##### 링크: [KOROMOON][koromoonlink]
[koromoonlink]: https://koromoon.blogspot.com/2018/02/blog-post_19.html "Go koromoon"
##### 작성자: 김평일 대리
##### 작성일자: 2024년 4월 17일

<br>
<br>

## (1) 동작 범위에 따른 환경 변수

크게 세 가지 관점으로 나눌 수 있음.

<br>1. 로컬 환경 변수<br>
현재 세션에서만 동작하는 환경 변수임.<br>

<br>2. 사용자 환경 변수<br>
특정 사용자에 대해서만 정의된 환경 변수로 로컬 터미널 세션 또는 원격 로그인 세션을 사용하여 로그인할 때마다 로드되며 관련파일은 특정 사용자의 홈 디렉토리에 존재하는 파일로 아래와 같음.<br>
`.bashrc`<br>
`.bash_profile`<br>
`.bash_login` <br>
`.profile`<br>

<br>3. 시스템 전체 환경 변수<br>
해당 시스템에 존재하는 모든 사용자가 사용할 수 있는 환경 변수로 시스템 전원이 켜져 있고 모든 사용자가 로컬 또는 원격으로 로그인할 때마다 로드되며 관련 파일은 아래와 같음.<br>
`/etc/environment`<br>
`/etc/profile`<br>
`/etc/profile.d/`<br>
`/etc/bash.bashrc`<br>

<br>
<br>

## (2) 환경 변수 구성 파일

**`.bashrc`**<br>
특정 사용자가 새로운 로컬 세션을 생성할 때마다 로드되는 파일로 별칭(alias)과 bash 가 실행될 때 실행되는 함수 등으로 구성됨.<br>
이 파일은 전역적인 설정 파일인 /etc/bashrc 이 수행된 다음 바로 수행됨.<br>
모든 사용자에게 영향을 주는 /etc/bashrc 와는 달리 ~/.bashrc 는 오직 bash 를 실행하는 그 사용자에게만 영향을 줌.<br>


**`.bash_profile`**<br>
특정 사용자의 원격 로그인 파일로 이 파일에 있는 환경 변수는 사용자가 원격 로그인 세션이 이루어질 시에 호출됨.<br>
이 파일이 존재하지 않으면 시스템은 .bash_login 이나 .profile 파일을 검색함.<br>
이 파일은 전역적인 설정 파일인 /etc/profile 이 수행된다음 바로 수행됨.<br>
모든 사용자에게 영향을 주는 /etc/profile 과는 달리 ~/.bash_profile 는 오직 bash 를 실행하는 그 사용자에게만 영향을 줌.<br>


**`/etc/environment`**<br>
전반적인 시스템을 제어하는 파일로 필요한 환경 변수를 작성하거나 편집 또는 제거함.<br>
이 파일에서 만든 환경 변수는 로컬 및 원격으로 접속한 모든 사용자가 액세스할 수 있음.<br>


**`/etc/bash.bashrc`**<br>
시스템 전체의 bashrc 파일로 모든 사용자가 로컬 터미널 세션을 열 때마다 로드됨.<br>
이 파일에서 만든 환경 변수는 모든 사용자가 액세스할 수 있지만 로컬 터미널 세션에서만 가능함.<br>


**`/etc/profile`**<br>
시스템 전체의 profile 파일로 모든 사용자가 원격 로그인 세션이 이루어질 시에 호출됨.<br>
이 파일에서 만든 환경 변수는 모든 사용자가 액세스할 수 있지만 원격 로그인 세션에서만 가능함.<br>


파일 내용을 수정 후에 재부팅/재실행 없이 즉시 적용하고자 한다면 아래 명령어와 같이 입력함.<br>
&ensp;**`source [파일 이름]`** <br>

<br>
<br>

## (3) 로컬 환경 변수 설정

<br>1. 가변적인 변수명을 사용하여 설정
</br><div align="center">![image](https://github.com/ICTIS-Cert-System-Project/ICTIS-Cert-System/assets/165347210/c734c58a-a716-49ca-8436-a9e380c44b7c)</div>

기본 형식 : <ins>[가변적인 변수명]</ins>=<ins>[환경변수값]</ins><br>

<br>2. export 명령어를 이용하여 환경 변수를 설정
</br><div align="center">![image](https://github.com/ICTIS-Cert-System-Project/ICTIS-Cert-System/assets/165347210/4174b764-baad-4c40-8b81-061c01eb724a)</div>

기본 형식 : export <ins>[변수명]</ins>=<ins>[환경변수값]</ins><br>

**주의사항! <ins>변수명과 데이터값 사이에 있는 '=' 과 띄워쓰기를 하면 '=' 을 데이터로 인식하는 오류가 나기 때문에 사용해서는 안됨.</ins>**<br>

<br>

입력한 환경 변수를 확인할 때는 `'echo [$변수명]'` 명령을 입력해서 확인함.<br>
로컬 환경 변수를 삭제할 때는 `'unset [가변적인 변수명]'` 입력하거나 `'env -i bash'` 명령을 입력함.<br>
참고로 그 후에 exit 명령어를 입력하면 모든 변수명이 복원되어서 다시 사용할 수 있음.<br>

아래는 export 명령어에 대한 추가 정보임.<br>
export<br>
환경변수 리스트를 보여줌<br>
`export [변수명]=[$변수명]:[환경변수값]`<br>
ex. `export PATH=$PATH:/home/koromoon/hack1/bin:/home/koromoon/hack2/bin`<br>

**변수명에 환경변수값을 추가함**<br>

<br>
<br>

## (4) 사용자 환경 변수 설정

<br>

`.bashrc` 이나 `.bash_profile` 파일 하단에 `'export [변수명]=[환경변수값]'` 명령줄을 추가한 후 `source [파일 이름]` 명령어를 입력하여 설정함.<br>
삭제할 때는 역으로 `'export [변수명]=[환경변수값]'` 명령줄을 삭제한 후 `source [파일 이름]` 명령어를 입력하여 설정함.<br>
`.bashrc` (특정 사용자가 새로운 로컬 세션으로 접근 시도시)<br>
`.bash_profile` (특정 사용자가 원격 로그인 세션으로 접근 시도시)<br>

<br>
<br>

## (5) 시스템 전체 환경 변수

<br>

`/etc/bash.bashrc` 이나 `/etc/profile` 파일 하단에 `'export [변수명]=[환경변수값]'` 명령줄을 추가한 후 source [파일 이름] 명령어를 입력하여 설정함.<br>
삭제할 때는 역으로 `'export [변수명]=[환경변수값]'` 명령줄을 삭제한 후 `source [파일 이름]` 명령어를 입력하여 설정함.<br>
`.bashrc` (모든 사용자가 새로운 로컬 세션으로 접근 시도시)<br>
`.bash_profile` (모든 사용자가 원격 로그인 세션으로 접근 시도시)<br>

<br>
<br>

## (6) 일반적으로 사용되는 환경변수 목록


</br>![image](https://github.com/ICTIS-Cert-System-Project/ICTIS-Cert-System/assets/165347210/b2037ce7-5a88-4456-a25f-0f73fa436dc8)</div>

<br>
<br>

## (7) 환경변수 확인 명령어

`set 명령어   : 로컬 환경변수 조회 명령어`<br>
`env 명령어   : 글로벌 환경변수 조회 명령어`<br>

<br>





