---
title: 설치
keywords: questions, troubleshooting, contact, support
last_updated: March 20, 2016
summary: "WIZEYE package는 Docker를 이용하여 설치를 진행한다. Docker는 리눅스 컨테이너(LXC) 기반의 가상화 엔진으로 응용프로그램의 배포를 자동화한다."
sidebar: mydoc_sidebar
permalink: /mydoc_install/
---


## Docker 설치

### 설치
WIZEYE package를 정상적으로 설치하기 위해서는 docker-engine-1.8.3 버전을 설치해야 한다.
docker-engine-1.8.3 버전을설치하는 방법은 2가지가 있다.

 * Yum 설치  
 
 * rpm 설치  

----


1.yum 설치 과정으로 repository를 추가하여 설치한다.  

`cat >/etc/yum.repos.d/docker.repo<<-EOF`  
`[dockerrepo]`  
`name=Docker Repository`  
`baseurl=https://yum.dockerproject.org/repo/main/centos/7`  
`enabled=1`  
`gpgcheck=1`  
`gpgkey=https://yum.dockerproject.org/gpg`  
`EOF`  

* 도커 저장소를 구성하고 정보를 입력한다.  

`sudoyum install -y docker-engine-1.8.3`

* docker-engine-1.8.3를 설치한다.  


2.rpm을 다운로드 하여 설치한다.

wget [https://yum.dockerproject.org/repo/main/centos/7/Packages/docker-engine-1.8.3-1.el7.centos.x86_64.rpm](http://)

* docker-engine-1.8.3-1.el7.centos.x86_64.rpm을 다운한다.  

`rpm –Uvh docker-engine-1.8.3-1.el7.centos.x86_64.rpm`

* rpm을 설치한다.


### 실행 및 확인

Docker를 실행하고 정상적으로 설치되었는지를 확인한다.

```css
1. sudo service docker start
2. sudo docker run hello-world
3. dockerps -a
4. docker-v
```

1. 도커를 실행한다.
2. 테스트 이미지(hello-world)를 실행하여 제대로 설치되었는지를 확인하다.
    * 테스트 이미지가 정상 작동하면 아래와 같이 출력된다.

[이미지]
   * 테스트 이미지(hello-world) 과정을 실행하지 않으면 도커 실행이 이뤄지지 않을 수 있다.  

3. 도커가 정상적으로 작동하는 것을 확인한다.
[이미지]

4. 도커 버전을 확인한다. (1.8.3)

### 설정
Docker 서비스가 자동으로 실행할 수 있도록 설정한다.

```css
1. sudo chkconfigdocker on
```

1. 시스템을 재 부팅 시에도 Docker 서비스가 자동 실행된다.



## Docker-Compose

### 실행

다음의 명령을 실행한다.

```css
1. curl -L https://github.com/docker/compose/releases/download/1.4.2/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose  
2. chmod +x /usr/local/bin/docker-compose
```

1. 지정한 경로(/usr/local/bin)에 docker-compose가 다운로드 된다.  
2. docker-compose의 권한을 설정한다. 

### 확인
docker-compose정보를 확인한다.

```css
1. docker-compose -v
```

1. docker-compose 버전을 확인한다. (1.4.2)


## 스크립트 다운로드 및 실행
스크립트를 다운로드 받아 실행한다.

1. 아티팩토리에서스크립트를 다운로드 한다.  
wget [http://artifactory.dev.n3n.io:8081/artifactory/ext-release-local/release-candidate/n3n-docker/1.0/configure_run_docker_compose.sh](http://)

2. 권한을 설정한다.  
`chmod 700 configure_run_docker_compose.sh`

3. docker-compose를 실행한다.  
`./configure_run_docker_compose.sh`
  
 * 발급받은 Docker Hub 계정 정보를 입력하면 설치가 진행된다.  

===========  Login to Docker Hub ======================  
Please enter Docker Hub Username :  
Please enter Docker Hub Password :  
Logging in to Docker Hub Account ..... Login successful  
========================================================  
 * Docker Hub 계정 정보는 N3N에 문의 한다.



## 설치 확인
WIZEYE package가 설치되어 서비스가 정상적으로 실행되는지는 프로세스 및 웹 접속으로 확인한다.

### 프로세스 확인
프로세스 확인 방법은 다음과 같습니다.


```css
1. dockerps -a
```

1. WIZEYE container구성 및 서비스 상태를 확인한다.

[이미지]

- WIZEYE Container는 총 14개이며,ws(WIZEYEServer), wuf(WIZEYE UI Framework), wuf-builder, wuf-proxy, mongodb, mysql, redmine, Cassandra, zookeeper, Nginx, spark, service, neo4j, kafka으로 구성된다.



### 방화벽 설정

보안을 위해 WIZYE에서 사용하는 포트들에 대해 방화벽을 열어 주어야 한다.

```css
1. systemctl start firewalld  
2-a. firewall-cmd --zone=public --permanent --add-port=4243/tcp(4243 포트 오픈 예제)  
2-b. firewall-cmd --zone=public --permanent --add-port=4990-4999/tcp(4990-4999 포트 오픈 예제)  
3. firewall-cmd --zone=public --permanent --list-ports  
```

1. 원활한 설치를 위해 일시적으로 내렸던 방화벽을 다시 올린다.
2. 방화벽을 열어줄 포트를 추가한다.이때,특정 범위의 포트를 열어 주고자 하는 경우는 b와 같은 방법을 사용한다.
3. 방화벽이 열린 포트 목록을 조회 한다.

  * WIZEYE 구축환경에 따라 사용하는 포트들은 다를 수 있으며,방화벽을 열어 줄 포트들도 다를 수 있다.
  * WIZEYE에서 기본적으로사용하는 포트는(27017, 1337, 1335, 8080, 1336, 9000, 80, 3306, 3000, 7474, 7000, 9042, 9160, 2181, 9092, 443, 4040, 6066, 7077, 8888, 8081, 8082, 4234, 7001-7006, 7012-7016)이 있다.

### 웹 접속 확인

1. WIZEYEUI Framework 확인
 - http://xxx.xx.xx.xxx:8080으로 접속한다.
 - 정상적으로 실행하고 있으면 아래의 웹으로 접속한다.

[이미지]


2. WIZEYEBuilder확인

- [http://xxx.xx.xx.xxx:9000](http://)으로 접속한다.
- 정상적으로 실행하고 있으면 아래의 웹으로 접속한다.


[이미지]






















