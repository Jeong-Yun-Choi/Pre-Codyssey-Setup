# 프로젝트 개요
해당 프로젝트는 코디세이 2기 입학연수과정에서 진행되는 첫 번째 미션인 <내 컴퓨터에 개발자용 '작업실' 꾸미기>에 대한 것으로 본격적인 개발에 앞서 개발 환경을 구축하고 준비하는 과정을 담고 있습니다. 다음과 같이 크게 세 가지 도구에 대해서 다루게 됩니다.
 - 리눅스 CLI(Command Line Interface) : 터미널(Terminal)
 - 도커(Docker) : 컨테이너(Container)
 - 깃/깃헙(Git/GitHub) : 버전 관리 및 협업툴
 
 본 과제의 목표는 다음과 같습니다.
 1. 절대 경로 vs 상대 경로
 2. 파일 권한의 의미, 권한 표기법의 규칙
 3. 기존 Dockerfile 기반 커스텀 이미지 생성
 4. 포트 매핑이 필요한 이유
 5. Docker 볼륨(데이터 영속성)
 6. Git(로컬 버전관리) vs GitHub(원격 협업 플랫폼)의 역할

 # 목차

[1) 실행환경](#1-실행환경)

[2) 수행 항목 체크리스트](#2-수행-항목-체크리스트)

[3) 터미널 조작 및 권한 실습](#3-터미널-조작-및-권한-실습)

&nbsp;&nbsp;&nbsp;&nbsp; [3-1) 터미널 조작](#3-1-터미널-조작)

&nbsp;&nbsp;&nbsp;&nbsp; [3-2) 권한 실습](#3-2-권한-실습)

[4) Docker 실습](#4-docker-실습)

&nbsp;&nbsp;&nbsp;&nbsp;[4-1) Docker 설치 및 기본 점검](#4-1-docker-설치-및-기본-점검)

&nbsp;&nbsp;&nbsp;&nbsp;[4-2) Docker 기본 운영 명령 수행](#4-2-docker-기본-운영-명령-수행)

&nbsp;&nbsp;&nbsp;&nbsp;[4-3) 컨테이너 실행 실습](#4-3-컨테이너-실행-실습)

&nbsp;&nbsp;&nbsp;&nbsp;[4-4) 기존 Dockerfile 기반 커스텀 이미지 제작](#4-4-기존-dockerfile-기반-커스텀-이미지-제작)

&nbsp;&nbsp;&nbsp;&nbsp;[4-5) 포트 매핑 및 접속](#4-5-포트-매핑-및-접속)

&nbsp;&nbsp;&nbsp;&nbsp;[4-6) Docker 볼륨 영속성 검증](#4-6-docker-볼륨-영속성-검증)

[5) Git 설정 및 GitHub 연동](#5-git-설정-및-github-연동)

[6) 트러블슈팅](#6-트러블슈팅)

[7) 검증방법](#7-검증방법)

## 1) [실행환경](#실행환경-검증)
- **OS :  macOS 15.7.7**

- **SHELL : bash 5.9 x86_64**

- **Terminal : Apple_Terminal 455.1**

- **Docker : 28.5.2 build ecc6942**

- **Git : 2.53.0**

## 2) 수행 항목 체크리스트
- [ ] 터미널 기본 조작 및 폴더 구성

- [ ] 권한 변경 실습

- [ ] Docker 설치/점검

- [ ] hello-world 실행

- [ ] Dockerfile 빌드/실행

- [ ] 포트 매핑 접속

- [ ] 바인드 마운트 반영

- [ ] 볼륨 영속성 검증

- [X] Git 초기 설정

- [X] VSCode GitHub 연동

## 3) 터미널 조작 및 권한 실습
### 3-1) 터미널 조작

**- 현재 위치를 확인하는 명령어**
```bash
pwd
```
**&#9654; 수행 로그**
```bash
jeongyun.choi****** ~ % pwd
/Users/jeongyun.choi******
```
**- 숨김 파일을 포함한 목록 확인하는 명령어**
```bash
ls -la
```
`-l`: 상세히 보기, `-a`: 숨김파일까지 모두 표시

**&#9654; 수행 로그**
```bash
jeongyun.choi****** ~ % ls -la # 숨김파일 포함 목록 확인
total 64
drwxr-x---+ 25 jeongyun.choi******  jeongyun.choi******    800  8  3 16:17 .
drwxr-xr-x   6 root                 admin                  192  8  3 09:10 ..
-r--------   1 jeongyun.choi******  jeongyun.choi******      8  8  3 09:10 .CFUserTextEncoding
drwxr-xr-x   5 jeongyun.choi******  jeongyun.choi******   160  8  3 10:53 .docker
-rw-r--r--@  1 jeongyun.choi****** jeongyun.choi******  10244  8  3 14:05 .DS_Store
-rw-r--r--   1 jeongyun.choi******  jeongyun.choi******     91  8  3 10:11 .gitconfig
-rw-------   1 jeongyun.choi  jeongyun.choi     20  8  3 13:22 .lesshst
drwxr-xr-x  10 jeongyun.choi******  jeongyun.choi******    320  8  3 10:53 .orbstack
drwxr-xr-x   3 jeongyun.choi******  jeongyun.choi******     96  8  3 10:53 .ssh
drwx------+ 14 jeongyun.choi******  jeongyun.choi******    448  8  3 16:11 .Trash
drwxr-xr-x   5 jeongyun.choi******  jeongyun.choi******    160  8  3 10:33 .vscode
-rw-r--r--   1 jeongyun.choi******  jeongyun.choi******    154  8  3 10:53 .zprofile
-rw-------   1 jeongyun.choi******  jeongyun.choi******    540  8  3 16:17 .bash_history
drwx------  15 jeongyun.choi******  jeongyun.choi******    480  8  3 16:17 .bash_sessions
drwx------+  5 jeongyun.choi******  jeongyun.choi******    160  8  3 16:11 Desktop
drwx------+  3 jeongyun.choi******  jeongyun.choi******     96  8  3 09:10 Documents
drwx------+  6 jeongyun.choi******  jeongyun.choi******    192  8  3 14:06 Downloads
drwx------@ 82 jeongyun.choi******  jeongyun.choi******   2624  8  3 14:21 Library
drwx------   3 jeongyun.choi******  jeongyun.choi******     96  8  3 09:10 Movies
drwx------+  3 jeongyun.choi******  jeongyun.choi******     96  8  3 09:10 Music
drwx------   4 jeongyun.choi******  jeongyun.choi******    160  8  3 10:53 OrbStack
drwx------+  4 jeongyun.choi******  jeongyun.choi******    128  8  3 09:10 Pictures
drwxr-xr-x   5 jeongyun.choi******  jeongyun.choi******    160  8  3 16:11 projects
drwxr-xr-x+  4 jeongyun.choi******  jeongyun.choi******    128  8  3 09:10 Public
drwxr-xr-x   2 jeongyun.choi******  jeongyun.choi******     64  8  3 11:52 test
```
#### 이동
**- 특정한 디렉토리로 이동하는 명령어**
```bash
cd 경로
```
&#8251; 이동하고자 하는 디렉토리가 현재 위치에 있지 않은 경우, 현재 위치에서 해당 디렉토리까지의 전체 경로가 표현되어야만 이동할 수 있다.

**&#9654; 수행 로그**
```bash
jeongyun.choi****** ~ % cd projects # 이동하고자 하는 디렉토리가 현재 위치에 바로 있는 경우
jeongyun.choi****** projects % 

jeongyun.choi****** ~ % cd test/intest/inintest # 이동하고자 하는 디렉토리가 현재 위치에 바로 있지 않은 경우
jeongyun.choi****** inintest % pwd                    
/Users/jeongyun.choi*******/test/intest/inintest
```
`~` : 홈 디렉토리, `/` : 루트 디렉토리
<br>
<br>

&#8251; 파일과 디렉토리의 이름을 변경하는 명령어는 mv로 동일하다. 경로를 변경하지 않으면 이름을 변경하는 명령어로 작동한다.

**- 파일 및 디렉토리를 이동시키는 명령어**
```bash
mv 파일명(디렉토리명).파일형식 이동시킬 경로
```

**- 파일 및 디렉토리의 이름을 변경하는 명령어**
```bash
mv 파일명(디렉토리명).파일형식 변경할 파일명(디렉토리명)
```
#### 생성

**- 파일을 생성하는 명령어**

**- 디렉토리를 생성하는 명령어**

#### 복사

#### 삭제

#### 파일 내용 확인

#### 빈 파일 생성

### 3-2) 권한 실습



## 4) Docker 실습
### 4-1) Docker 설치 및 기본 점검

**- Docker 설치 확인 및 버전 확인하는 명령어**
```bash
docker --version
```
**&#9654; 수행 로그**
```bash
jeongyun.choi****** ~ % docker --version
Docker version 28.5.2, build ecc6942
```
**- docker 데몬 동작 여부 확인하는 명령어**
```bash
docker info
```
&#8251; `Server:` 뒤에 다음과 같이 출력결과가 나온다면 데몬이 정상적으로 동작하고 있음을 알 수 있다.
```bash
Server:
 Containers: 0
  Running: 0
  Paused: 0
  Stopped: 0
 Images: 0
 Server Version: 28.5.2
```
**&#9654; 수행 로그**

```bash
jeongyun.choi******~ % docker info
Client:
 Version:    28.5.2
 Context:    orbstack
 Debug Mode: false
 Plugins:
  buildx: Docker Buildx (Docker Inc.)
    Version:  v0.29.1
    Path:     /Users/jeongyun.choi******/.docker/cli-plugins/docker-buildx
  compose: Docker Compose (Docker Inc.)
    Version:  v2.40.3
    Path:     /Users/jeongyun.choi******/.docker/cli-plugins/docker-compose

Server:
 Containers: 0
  Running: 0
  Paused: 0
  Stopped: 0
 Images: 0
 Server Version: 28.5.2
 Storage Driver: overlay2
  Backing Filesystem: btrfs
  Supports d_type: true
  Using metacopy: false
  Native Overlay Diff: true
  userxattr: false
 Logging Driver: json-file
 Cgroup Driver: cgroupfs
 Cgroup Version: 2
 Plugins:
  Volume: local
  Network: bridge host ipvlan macvlan null overlay
  Log: awslogs fluentd gcplogs gelf journald json-file local splunk syslog
 CDI spec directories:
  /etc/cdi
  /var/run/cdi
 Swarm: inactive
 Runtimes: io.containerd.runc.v2 runc
 Default Runtime: runc
 Init Binary: docker-init
 containerd version: 1c4457e00facac03ce1d75f7b6777a7a851e5c41
 runc version: d842d7719497cc3b774fd71620278ac9e17710e0
 init version: de40ad0
 Security Options:
  seccomp
   Profile: builtin
  cgroupns
 Kernel Version: 6.17.8-orbstack-00308-g8f9c941121b1
 Operating System: OrbStack
 OSType: linux
 Architecture: x86_64
 CPUs: 6
 Total Memory: 15.67GiB
 Name: orbstack
 ID: 713b2d7a-8952-4054-931f-879b6d592dde
 Docker Root Dir: /var/lib/docker
 Debug Mode: false
 Experimental: false
 Insecure Registries:
  ::1/128
  127.0.0.0/8
 Live Restore Enabled: false
 Product License: Community Engine
 Default Address Pools:
   Base: 192.168.97.0/24, Size: 24
   Base: 192.168.107.0/24, Size: 24
   Base: 192.168.117.0/24, Size: 24
   Base: 192.168.147.0/24, Size: 24
   Base: 192.168.148.0/24, Size: 24
   Base: 192.168.155.0/24, Size: 24
   Base: 192.168.156.0/24, Size: 24
   Base: 192.168.158.0/24, Size: 24
   Base: 192.168.163.0/24, Size: 24
   Base: 192.168.164.0/24, Size: 24
   Base: 192.168.165.0/24, Size: 24
   Base: 192.168.166.0/24, Size: 24
   Base: 192.168.167.0/24, Size: 24
   Base: 192.168.171.0/24, Size: 24
   Base: 192.168.172.0/24, Size: 24
   Base: 192.168.181.0/24, Size: 24
   Base: 192.168.183.0/24, Size: 24
   Base: 192.168.186.0/24, Size: 24
   Base: 192.168.207.0/24, Size: 24
   Base: 192.168.214.0/24, Size: 24
   Base: 192.168.215.0/24, Size: 24
   Base: 192.168.216.0/24, Size: 24
   Base: 192.168.223.0/24, Size: 24
   Base: 192.168.227.0/24, Size: 24
   Base: 192.168.228.0/24, Size: 24
   Base: 192.168.229.0/24, Size: 24
   Base: 192.168.237.0/24, Size: 24
   Base: 192.168.239.0/24, Size: 24
   Base: 192.168.242.0/24, Size: 24
   Base: 192.168.247.0/24, Size: 24
   Base: fd07:b51a:cc66:d000::/56, Size: 64

WARNING: DOCKER_INSECURE_NO_IPTABLES_RAW is set
```
&#8251; 만약 orbstack이 완전히 종료된 상태이거나 정상적으로 동작하고 있지 않다면 다음과 같은 문구가 뜨게 된다.
```bash
Server:
Cannot connect to the Docker daemon at unix:///Users/jeongyun.choi******/.orbstack/run/docker.sock. Is the docker daemon running?
```
**&#9654; 수행 로그**
```bash
jeongyun.choi****** ~ % docker info
Client:
 Version:    28.5.2
 Context:    orbstack
 Debug Mode: false
 Plugins:
  buildx: Docker Buildx (Docker Inc.)
    Version:  v0.29.1
    Path:     /Users/jeongyun.choi******/.docker/cli-plugins/docker-buildx
  compose: Docker Compose (Docker Inc.)
    Version:  v2.40.3
    Path:     /Users/jeongyun.choi******/.docker/cli-plugins/docker-compose

Server:
Cannot connect to the Docker daemon at unix:///Users/jeongyun.choi******/.orbstack/run/docker.sock. Is the docker daemon running?
```

**- 간단하게 데몬 동작 여부를 확인할 수 있는 명령어**
```bash
docker ps
```
**&#9654; 수행 로그**

```bash
jeongyun.choi****** ~ % docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```
<br>
<br>

**- 정상적으로 동작하고 있지 않을 때**

**&#9654; 수행 로그**
```bash
jeongyun.choi******* ~ % docker ps
Cannot connect to the Docker daemon at unix:///Users/jeongyun.choi******/.orbstack/run/docker.sock. Is the docker daemon running?
```
### 4-2) Docker 기본 운영 명령 수행
**- 다운로드된 이미지를 확인하는 명령어**

```bash
docker images
```
**&#9654; 수행 로그**
```bash
jeongyun.choi****** ~ % docker images
REPOSITORY   TAG       IMAGE ID   CREATED   SIZE
```
현재는 docker를 처음 실행한 상태이기 때문에 이미지 목록에는 아무것도 뜨지 않는다.

### 4-3) 컨테이너 실행 실습
### 4-4) 기존 Dockerfile 기반 커스텀 이미지 제작
### 4-5) 포트 매핑 및 접속
### 4-6) Docker 볼륨 영속성 검증
## 5) Git 설정 및 GitHub 연동
### 5-1) GitHub 계정 연동하기
**- 계정 연동 시 사용되는 명령어**
```bash
git config --global user.email "이메일주소"
git config --global user.name "사용자이름(username)"
```
**&#9654; 수행 로그**
```bash
jeongyun.choi******** ~ % git config --global user.name "Jeong-Yun-Choi" # GitHub 가입 시 사용한 사용자이름(username)
jeongyun.choi******** ~ % git config --global user.email "******@******" # GitHub 가입 시 사용한 이메일 주소
```
### 5-2) 기본 브랜치 설정하기
**- 기본 브랜치 설정 시 사용되는 명령어**
```bash
git config --global init.defaultBranch main
```
**&#9654; 수행 로그**
```bash
jeongyun.choi******* projects-setup % git config --global init.defaultBranch main
main
```
### 5-3) 로컬저장소에 Git 초기화하기
```bash
jeongyun.choi********~ % pwd # 현재 위치 확인
/Users/jeongyun.choi******

jeongyun.choi ~ % cd projects-setup # 로컬저장소로 사용할 디렉토리로 이동
jeongyun.choi******** projects-setup % 
```
**- Git 초기화시 사용되는 명령어**
```bash
git init
```
**&#9654; 수행 로그**
```bash
jeongyun.choi******** projects-setup % git init
/Users/jeongyun.choi******/projects-setup/.git/ 안의 빈 깃 저장소를 다시 초기화했습니다
```
### 5-4) 로컬저장소와 원격저장소 연결하기
**- 두 저장소를 연결하는 명령어**

```bash
git remote add origin 해당 레포지토리 주소(원격저장소 주소)
```
**&#9654; 수행 로그**

```bash
jeongyun.choi******** projects-setup % git remote -v
origin	https://github.com/Jeong-Yun-Choi/Pre-Codyssey-Setup.git (fetch)
origin	https://github.com/Jeong-Yun-Choi/Pre-Codyssey-Setup.git (push)
```
### 5-5) 원격저장소와 로컬저장소의 연동 확인하기
**- 두 저장소의 연동 확인하는 명령어**
```bash
git config --list
```
**&#9654; 수행 로그**

```bash
jeongyun.choi******** projects-setup % git config --list
credential.helper=osxkeychain
user.email=*********@********
user.name=Jeong-Yun-Choi
init.defaultbranch=main
core.repositoryformatversion=0
core.filemode=true
core.bare=false
core.logallrefupdates=true
core.ignorecase=true
core.precomposeunicode=true
remote.origin.url=https://github.com/Jeong-Yun-Choi/Pre-Codyssey-Setup.git
remote.origin.fetch=+refs/heads/*:refs/remotes/origin/*
```
### 5-6) VSCode와 GitHub 계정 연동 확인하기
![vscode_github_connect](./screenshot/github_vscode_connect.png)

## 6) 트러블슈팅

## 7) 검증방법
### 실행환경-검증
**- OS를 확인하는 명령어**
```bash
sw_vers
```
**&#9654; 수행 로그**
```bash
jeongyun.choi******* ~ % sw_vers
ProductName:		macOS
ProductVersion:		15.7.7
BuildVersion:		24G720
```

<br>
<br>

**- SHELL의 이름과 버전을 확인하는 명령어**
```bash
echo $SHELL # 쉘의 종류
bash --version # 쉘의 버전
```
**&#9654; 수행 로그**
```bash
jeongyun.choi****** ~ % echo $SHELL # 쉘의 종류
/bin/bash
jeongyun.choi****** ~ % bash --version # 쉘의 버전
bash 5.9 (x86_64-apple-darwin24.0)
```
<br>
<br>

**- 터미널의 이름과 버전을 확인하는 명령어**
```bash
echo $TERM_PROGRAM # 터미널명
echo $TERM_PROGRAM_VERSION # 터미널 버전 확인
```

**&#9654; 수행 로그**
```bash
jeongyun.choi******* ~ % echo $TERM_PROGRAM
Apple_Terminal
jeongyun.choi*******~ % echo $TERM_PROGRAM_VERSION
455.1
```
<br>
<br>

**- Docker 버전을 확인하는 명령어**
```bash
docker --version
```
**&#9654; 수행 로그**
```bash
jeongyun.choi****** ~ % docker --version
Docker version 28.5.2, build ecc6942
```
<br>
<br>

**- Git의 버전을 확인하는 명령어**
```bash
git --version
```
**&#9654; 수행 로그**
```bash
jeongyun.choi******* projects % git --version
git version 2.53.0
```