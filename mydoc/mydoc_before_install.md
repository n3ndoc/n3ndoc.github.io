---
title: 설치 전 준비
keywords: "features, capabilities, scalability, multichannel output, dita, hats, comparison, benefits"
last_updated: "November 30, 2016"
summary: "이 문서는 WIZEYE소프트웨어를 사용할 수 있도록 프로그램을 설치하는 방법을 설명합니다."
published: true
sidebar: mydoc_sidebar
permalink: /mydoc_before_install/
---


## 시스템 요구사항 및 권장사항


구분 | 최소 요구사항 | 권장사항
:--------:|:-----------:|:-----------:
**OS** | CentOS7(64bit, Kernel 3.10이상) / *OS 버전확인 :uname -r |
**프로세서** | 1core 이상 | 2core 이상
**메모리(RAM)** | 2GB 이상  | 32GB 이상
**디스크** | 25GB 이상 | 40GB 이상

\* *최소요구사항에서는 WIZEYE가 정상 설치는 되나 일부 기능이 정상적으로 동작 하지 않을 수 있다.*


## 사전 준비 사항  

### NETWORK 환경 설정

```css
1. cd /etc/sysconfig/network-scripts
2. ls
3. ifcfg-[interface name]
4. service network restart
```

1\. Ethernet Interface가 있는 디렉토리로 이동한다.  
2\. Ethernet Interface파일이 존재 하는지 확인한다.  
3\. vi 편집기를 통해 Ethernet Interface파일을 열어 다음 항목들을 네트워크 환경에 맞도록 설정한다.

```
BOOTPROTO=static
IPV6=no
IPADDR=127.0.0.1
NETMASK=255.0.0.0
NETWORK=127.0.0.0
GATEWAY=172.16.0.1
DNS1=168.0.0.1
DNS2=8.8.8.8
ONBOOT=yes
```

4\. 설정한 정보가 적용되도록 network 서비스를 재 시작 한다.


### 임시 방화벽 해제  

원활한 설치를 위해 방화벽을 일시적으로 내린다

```css
1. systemctl stop firewalld
```
1\. 방화벽 서비스를 중지 한다.  

설치가 완료되면 다시 방화벽을 올리고,사용하는 포트들에 대해서만 방화벽을 열어 준다.


### 시스템 시간 동기화
WIZEYE 모든 시스템에 대한 시간을 동기화 한다.

```css
1. date
2. yum install ntp or ntpdatetime.apple.com
```
1. 각 시스템의 시간 정보를 확인 한다.
2. 다른 시스템과 시간 정보가 맞지 않을 경우 동기화 한다.

  \* *시스템 간 시간 동기화가 이루어 지지 않을 경우Data 처리가 정상적이지 않을 수 있습니다.*


### Preinstall

wizeyepackage를 설치하기 전에 기본적으로 설치해야 하는 프로그램이 있다.  
필요한 프로그램은 다음과 같다.

```css
1. yum update
2. yum install perl
3. yum install net-tools
4. yum install wget
5. yum install libcgroup
6. yum install zip
7. yum install unzip
8. yum install java-1.7.0-openjdk-devel
9. type java
10. yum install ntp or ntpdatetime.apple.com
```

1.설치되어 있는 모든 패키지의 업데이트 정보를 확인하고 업데이트를 실행한다.
  \* *업데이트는 도커 엔지 설치 이전에 실행한다.*
2.Perl을 설치한다.
3.net-tools를 설치한다.
4.wget를 설치한다. (rpm을 다운로드 하기 위해 필요하다.)
5.libcgroup을 설치한다. (docker 1.8.3을 설치하기 위해 필요하다.)
6.zip을설치한다. (파일을 압축하기위해필요하다.)
7.unzip을설치한다. (압축풀기를실행하기위해필요하다.)
8.JDK 1.7.0 버전을 설치한다.
9.JAVA HOME PATH를 확인한다.

[이미지]

10.9번에서 조회한 JAVA HOME PATH를환경변수로설정한다.

[이미지]

  \* *9번과 10번 항목은 반드시 JAVA 설치 후 진행한다.*