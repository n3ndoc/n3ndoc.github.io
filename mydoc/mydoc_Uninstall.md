---
title: Uninstall
sidebar: mydoc_sidebar
permalink: /mydoc_Uninstall/
---

## Docker를 포함한 WIZEYE 전체 제거

Docker를 포함한 전체 WIZEYE Container를 삭제하는 프로세스는 다음과 같다.

~~~css
1. yum list installed | grep docker
2. yum –y remove [검색된 docker engine이름]
3. rm –rf /var/lib/docker
4. rm –rf/hdd /ss1 /ss2
~~~

1. 설치된 docker-engine의 이름을 확인한다.
2. 해당 docker-engine을 삭제 한다
3. 2번 명령은docker의 이미지,볼륨,Configulation파일들까지 삭제하는 것은 아니며, 모든 파일들까지 삭제 하기 위해 해당 명령을 입력한다.
4. WIZEYE 설치 시 생성한 모든 Directory를 삭제한다.



> **[주의]**  
> 
> WIZEYE 설치 시 생성한 Directory는 설치 시 다운로드 받은 **“configure_run_docker_compose.sh”**파일의 설정 정보에 따라 다를 수 있으므로 반드시 정확한 경로를 확인 후 삭제한다



## WIZEYE Container 제거
특정 WIZEYE Container를 삭제하는 프로세스는 다음과 같다.

~~~css
1. dockerps -a
2. dockerrm –f [삭제하고자 하는 Container ID]
3. dockerps -a
4. Docker images
5. docker rmi -f  [삭제하고자 하는 image ID]
6. Docker images
~~~


1. 삭제 하고자 하는 Container의 ID 정보를 확인한다. .
2. Container ID에 해당하는 Container를 삭제 한다.
3. Container 목록에서 삭제한 Container가 제거 되었는지 확인한다.
4. 2번 명령은 해당 Container의이미지파일까지 삭제한 것은 아니며,이미지 파일까지 삭제 하기 위해 삭제할 이미지 ID 정보를 확인한다.
5. Image ID에 해당하는 Image 파일을 삭제 한다.
6. Container Image목록에서 삭제한 Image 파일이 제거 되었는지 확인한다.  


> **[Tip] 삭제한 Container 다시 설치하기**  
>  
>
> 1. “docker-compose.yml” 파일이 저장된 경로로 이동 한다.(find / -name “docker-compose.yml”로 해당 파일이 저장된 경로 확인)  
> 2. docker-compose up –d  
> 3. dockerps –a :해당 Container가 생성되었는지 확인한다.  








