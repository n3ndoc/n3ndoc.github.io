---
title: Collector 설치
keywords: release notes, announcements, what's new, new features
last_updated: March 20, 2016
summary: "Version 5.0 of the Documentation theme for Jekyll changes some fundamental ways the theme works to provide product-specific sidebars, intended to accommodate a site where multiple products are grouped together on the same site rather than generated out as separate outputs."
sidebar: mydoc_sidebar
permalink: /mydoc_collector/
---

## 설치 전 준비

### DATA 동기화 및 라이선스 확인

Collector를 설치하기 전에 실행해야 하는 사항은 다음과 같다.

1.[WIZEYE Builder]에 접속하여, 사이트를 생성해야 한다.
* Collector 설정에서 생성한 사이트의 [라이선스 키] 정보가필요하다.*

2.[WUF]에 접속하여 [Sync To DP]를 실행한다.
* Collector 설치 전 [Sync To DP]는 필수 이다.

[이미지]

### Host Collector Preinstall

Host Collector를 설치하기 전에 기본적으로 설치해야 하는 프로그램은 다음과 같다.

```css
1. yum update
2. yum install net-tools
3. yum install wget
4. yum install zip
5. yum install unzip
```

### JVM Collector Preinstall

JVM Collector를 설치하기 전에 기본적으로 설치해야 하는 프로그램은 다음과 같다.

```css
1. yum update
2. yum install net-tools
3. yum install wget
4. yum install zip
5. yum install unzip
6. yum install java-1.7.0-openjdk-devel
7. type java
8. export JAVA_HOME=[JAVA HOME PATH]
```

## HostCollector 설치
### HostCollector다운 로드 및 압축 풀기

HostCollector를 설치하는 방법은 다음과 같다.

```css
1. mkdir Collector
2. cd Collector/
3. wget https://yum.dockerproject.org/repo/main/centos/7/Packages/docker-engine-1.8.3-1.el7.centos.x86_64.rpm
4. unzip n3n-host-agent-1.0.12.zip –d n3n-host-1.0.12
```

1. Host Collector가 설치되는 디렉터리를 생성한다.
2. Collector 디렉터리로 이동한다.
3. Host Collector 파일을 다운로드 한다.
4. “n3n-host-agent-1.0.12.zip” 파일을 “n3n-host-1.0.12”폴더에 푼다.



### HostCollector 설정 변경

HostCollector를 설정하는 방법은 다음과 같다.
```css
1. cd n3n-host-1.0.12/
2. ls
3. cd conf
4. ls
5. vi host_monitor.config
```
1. “n3n-host-1.0.12” 디렉터리로 이동한다.
2. 디렉터리 내 파일 및 디렉토리를 확인 한다.
3. conf 디렉터리로 이동한다.
4. 디렉터리 내에 파일을 확인한다. (host_monitor.config 파일이 있다.)
5. vi 편집기로 “host_monitor.config”의Licensekey, PostURL, HealthcheckRequired의 정보를 환경에 맞도록 변경한다.

~~~~
{
        "authorization" : {
                "licensekey" :"ca164c0e2e90923e3664f80d43b35f7314e06c788931dec19381196735dc2b01"
        },
        "authentication" : {
                "PostURL"    : "http://172.16.10.45:8090/kafka.php?SrcType=HostMonitoring",
                "Userid"     : "n3ncollect",
                "Password"   : "welcome"
        },
        "CollectionInterval" : 60,
        "PostTo"             : "URL",
        "industrytype"       : "itsm",
        "DaemonModeInLinux"  : "Yes",
        "FileMode"           : "Overwrite",
        "HealthCheckRequired" : "No",
        "HealthCheckURL"     : "http://localhost:9000/agentmanager/Host",
        "HealthInterval"     : 60,
        "DebugLogLevel"      : "CRITICAL"
}
~~~~

- Builder에서생성된라이선스키를입력한다.
- n3n-dp-nginx의 IP, Port정보를입력한다
- HealthCheckRequired는 “No”를 입력한다.

### HostCollector 실행하기

```css
1. n3n-host-1.0.12/bin/
2. ls
3. python host-monitor.py
4. ps ax | grep python
```
1. “n3n-host-1.0.12/bin/” 디렉터리로 이동한다.
2. 디렉터리 내에 파일을 확인한다.(host-monitor.py파일이 있다.)
3. HostCollector를 실행한다.
4. HostCollector가 정상적으로 실행 되었는지 확인한다.

## JVMCollector 설치

### JVMCollector다운 로드 및 압축 풀기
JVMCollector를 설치하는 방법은 다음과 같다.

```css
1. cd Collector/
2. wget https://www.dropbox.com/s/p6by7xvcyiw6nzz/n3n-1.0.12.zip 
3. python host-monitor.py
4. ps ax | grep python
```

1. Collector 디렉터리로 이동한다.
2. JVM Collector 파일을 다운로드 한다.
3. “n3n-1.0.12.zip ” 파일을 “n3n-jvm-1.0.12”폴더에 푼다.


### JVMCollector설정 변경
JVMCollector를 설정하는 방법은 다음과 같다.

```css
1. cd n3n-jvm-1.0.12/
2. ls
3. cd conf
4. ls
5. vi Agent.properties
```

1. “n3n-host-1.0.12” 디렉터리로 이동한다.
2. 디렉터리 내 파일 및 디렉토리를확인한다.
3. conf 디렉터리로 이동한다.
4. 디렉터리 내에 파일을 확인한다. (Agent.properties파일이 있다.)
5. vi 편집기로 “Agent.properties의 Licensekey, applicationID, ssl, messageFeed의 정보를 환경에 맞도록 변경한다.

~~~~
n3n.licenseKey = ca164c0e2e90923e3664f80d43b35f7314e06c788931dec19381196735dc2b01
n3n.collectionInterval = 60
n3n.applicationID = N3NSTORE
n3n.ssl = false
n3n.messageFeed = C
~~~~

- Builder에서생성된라이선스 키를입력한다.
- 앱 이름을 입력한다.
- ssl를사용하지않을경우“False”로설정한다.

### Agent 설정 변경 및 n3n-agent-1.0.12.jar업데이트

```css
1. cd /n3n-jvm-1.0.12/
2. ls
3. unzipn3n-agent-1.0.12.jar
4. vi GlobalAgent.properties
5. zip -u n3n-agent-1.0.12GlobalAgent.properties
```

1. “n3n-jvm-1.0.12” 디렉터리로 이동한다.
2. 디렉터리 내에 파일을 확인한다. (n3n-agent-1.0.12.jar파일이 있다.)
3. “n3n-agent-1.0.12.jar”파일 압축 풀기를 실행한다.
4. vi 편집기로 “GlobalAgent.properties”내 n3n.hostName을Collector의IP:Port또는Domin정보(ex. - 127.0.0.1:8090 or datacollector.n3nwizeye.com)를환경에맞도록변경한다.
5. “n3n-agent-1.0.12.jar”압축파일의  GlobalAgent.properties파일을 업데이트 한다.

JVM Collector를 테스트하기 위해서는 다음과 같이 실행한다.

```css
1. wget http://apache.tt.co.kr/tomcat/tomcat-8/v8.0.32/bin/apache-tomcat-8.0.32.tar.gz 
2. gzip -dapache-tomcat-8.0.32.tar.gz
3. tar xvfapache-tomcat-8.0.32.tar
4. vi catalina.sh
```

1. tomcat을 다운로드 한다.
2. “apache-tomcat-8.0.32”파일 압축풀기를 실행한다.
3. “apache-tomcat-8.0.32” 파일을 설치한다.
4. vi 편집기에서catalina.sh의 스크립트에 위의 **[Agent 설정 변경 및 n3n-agent-1.0.12.jar 업데이트]**에서 업데이트한 **“n3n-agent-1.0.12.jar”**파일의 경로를 입력한다.  
`JAVA_OPTS="$JAVA_OPTS -javaagent:/home/collector/n3n-jvm-1.0.12/n3n-agent-1.0.12.jar"`

## Collector 설정

Collector를 설치한 후DP와의 연동을 위해Spark 스크립트를 설정한다.
설정이 완료되면 [WUF]에 접속하여 [Sync From DP]를 실행한다.

### Spark 스크립트 변경

Spark 스크립트를 설정하는 방법은 다음과 같다.

```css
1. cd /hdd/data/spark
2. vi submit_analytic_job.sh
3. vi submit_correlation_job.sh
4. /root/exec_correlation_spark_job.sh
```

1. /hdd/data/spark디렉터리로 이동한다. (해당 경로는 환경에 따라 다를 수 있으며,정확한 경로는 configure_run_docker_compose.sh파일에 설정된 경로를 확인해야 한다.)
2. vi 편집기로submit_analytic_job.sh를 아래와 같이 수정한다.

~~~
/data/spark/bin/spark-submit \
        --deploy-mode client \
        --driver-cores 2 \
        --driver-memory 2G \
        --executor-memory 2G \
        --driver-class-path /data/spark/apps/n3n-analytic-1.0-jar-with-dependencies.jar \
        --class com.n3n.itsm.analytic.RawEventsProcess \
        /data/spark/apps/n3n-analytic-1.0.jar $*
~~~

`class com.n3n.itsm.analytic.RawEventsBizNowProcess를 class com.n3n.itsm.analytic.RawEventsProcess로 변경한다.`

 3.vi 편집기로submit_correlation_job.sh를 아래와 같이 수정한다.
- JVM Collector와 Host Collect와 연동을 위해 jvmEvents와 hostEvents Topic을 추가 한다.(위 설정 정보는 Collector와 관련된 Topic으로,필요한 경우 추가 한다.)

~~~~
corr_class=com.n3n.itsm.event.client.Client
fori in `ps -ef|grep ${corr_class}|grep -v grep|awk '{print $2}'` ; do
kill ${i}
done
/data/spark/bin/spark-submit \
        --deploy-mode client \
        --driver-cores 2 \
        --driver-memory 3G \
        --executor-memory 3G \
        --driver-class-path /data/spark/apps/n3n-correlation-1.0-jar-with-dependencies.jar \
        --class ${corr_class} \
        /data/spark/apps/n3n-correlation-1.0.jar jvmEventshostEventslogEvents
~~~~


4.수정사항이 반영되도록 스크립트를 실행한다.

```css
1. crontab -l
2. /root/exec_correlation_spark_job.sh
```
 
1. Crontab스케쥴 정보를 조회한다.
2. /root/exec_correlation_spark_job.sh는 1시간 마다 실행되므로,수동으로 실행해준다.( /root/exec_analytic_spark_job.sh는 2분 마다 실행되므로 수동으로 실행 하지 않는다.)





















































