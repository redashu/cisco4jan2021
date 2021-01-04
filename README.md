# Getting started with Docker & containers

## app history 

<img src="apph.png">

## Build process of container with host kernel

<img src="kernel.png">

## vm vs container provides

<img src="cre.png">

# Container by Docker & mirantis

<img src="infod.png">

## Docker installation 

<img src="dockerinstall.png">


## Docker Desktop for Mac 

[docker desktop] ('https://hub.docker.com/editions/community/docker-ce-desktop-mac')


# INstalling Docker in Linux server 

```
[ec2-user@ip-172-31-15-194 ~]$ sudo yum  install  docker 
Failed to set locale, defaulting to C
Loaded plugins: extras_suggestions, langpacks, priorities, update-motd
amzn2-core                                                         | 3.7 kB  00:00:00     
Resolving Dependencies
--> Running transaction check
---> Package docker.x86_64 0:19.03.13ce-1.amzn2 will be installed
--> Processing Dependency: runc >= 1.0.0 for package: docker-19.03.13ce-1.amzn2.x86_64
--> Processing Dependency: containerd >= 1.3.2 for package: docker-19.03.13ce-1.amzn2.x86_64
--> Processing Dependency: pigz for package: docker-19.03.13ce-1.amzn2.x86_64
--> Processing Dependency: libcgroup for package: docker-19.03.13ce-1.amzn2.x86_64
--> Running transaction check

```

## checking installation 

```
[ec2-user@ip-172-31-15-194 ~]$ docker  version 
Client:
 Version:           19.03.13-ce
 API version:       1.40
 Go version:        go1.13.15
 Git commit:        4484c46
 Built:             Mon Oct 12 18:51:20 2020
 OS/Arch:           linux/amd64
 Experimental:      false
Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?
```

## starting docker engine 

```
[ec2-user@ip-172-31-15-194 ~]$ sudo systemctl start docker 
[ec2-user@ip-172-31-15-194 ~]$ sudo systemctl enable  docker 
Created symlink from /etc/systemd/system/multi-user.target.wants/docker.service to /usr/lib/systemd/system/docker.service.

```

## starting 

```
[ec2-user@ip-172-31-15-194 ~]$ sudo systemctl status  docker 
● docker.service - Docker Application Container Engine
   Loaded: loaded (/usr/lib/systemd/system/docker.service; enabled; vendor preset: disabled)
   Active: active (running) since Mon 2021-01-04 06:08:12 UTC; 52s ago
     Docs: https://docs.docker.com
 Main PID: 3958 (dockerd)
   CGroup: /system.slice/docker.ser
   
 ```
 
 ## Connecting to Docker engine 
 
 ```
 [ec2-user@ip-172-31-15-194 ~]$ docker version 
Client:
 Version:           19.03.13-ce
 API version:       1.40
 Go version:        go1.13.15
 Git commit:        4484c46
 Built:             Mon Oct 12 18:51:20 2020
 OS/Arch:           linux/amd64
 Experimental:      false
Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get http://%2Fvar%2Frun%2Fdocker.sock/v1.40/version: dial unix /var/run/docker.sock: connect: permission denied

```

## adding non root user to Docker group 

```
[ec2-user@ip-172-31-15-194 ~]$ sudo usermod -a -G docker ec2-user 
[ec2-user@ip-172-31-15-194 ~]$ logout
Connection to 35.154.0.70 closed.
❯ ssh -i Downloads/cisco.pem ec2-user@35.154.0.70
Last login: Mon Jan  4 05:39:02 2021 from 103.22.142.170


```

## now checking 

```
ec2-user@ip-172-31-15-194 ~]$ docker version 
Client:
 Version:           19.03.13-ce
 API version:       1.40
 Go version:        go1.13.15
 Git commit:        4484c46
 Built:             Mon Oct 12 18:51:20 2020
 OS/Arch:           linux/amd64
 Experimental:      false

Server:
 Engine:
  Version:          19.03.13-ce
  API version:      1.40 (minimum version 1.12)
  Go version:       go1.13.15
  Git commit:       4484c46
  Built:            Mon Oct 12 18:51:50 2020
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          1.4.1
  GitCommit:        c623d1b36f09f8ef6536a057bd658b3aa8632828
 runc:
  Version:          1.0.0-rc92
  GitCommit:        ff819c7e9184c13b7c2607fe6c30ae19403a7aff
 docker-init:
  Version:          0.19.0
  GitCommit:        de40ad0

```

## searching images on docker hub 

```
17  docker  images
   18  docker search python 
   19  docker search  java
   20  history 
   21  docker search  dockerashu
   22  docker search  ashutoshh 
   
   ```
   
   
## pulling docker images from docker hub 

```
 25  docker pull java 
   26  docker pull  python 
   27  docker pull  tomcat 
   28  history 
[ec2-user@ip-172-31-15-194 ~]$ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
tomcat              latest              feba8d001e3f        2 weeks ago         649MB
python              latest              d1eef6fb8dbe        2 weeks ago         885MB
java                latest              d23bdf5b1b1b        3 years ago         643MB

```
## Docker internal configuration 

```
[ec2-user@ip-172-31-15-194 ~]$ cd /var/lib/docker/
[ec2-user@ip-172-31-15-194 docker]$ ls
ls: cannot open directory .: Permission denied
[ec2-user@ip-172-31-15-194 docker]$ sudo -i
[root@ip-172-31-15-194 ~]# cd /var/lib/docker/
[root@ip-172-31-15-194 docker]# ls
builder  buildkit  containers  image  network  overlay2  plugins  runtimes  swarm  tmp  trust  volumes
[root@ip-172-31-15-194 docker]# 

```
## Docker client options 

<img src="dcli.png">

# first container 

```
[ec2-user@ip-172-31-15-194 ~]$ docker   run  --name ashuc1  alpine:latest  ping fb.com 
PING fb.com (157.240.16.35): 56 data bytes
64 bytes from 157.240.16.35: seq=0 ttl=49 time=1.156 ms
64 bytes from 157.240.16.35: seq=1 ttl=49 time=1.153 ms
64 bytes from 157.240.16.35: seq=2 ttl=49 time=1.845 ms
64 bytes from 157.240.16.35: seq=3 ttl=49 time=1.263 ms
64 bytes from 157.240.16.35: seq=4 ttl=49 time=1.198 ms
64 bytes from 157.240.16.35: seq=5 ttl=49 time=1.141 ms
64 bytes from 157.240.16.35: seq=6 ttl=49 time=1.237 ms
64 bytes from 157.240.16.35: seq=7 ttl=49 time=1.289 ms
64 bytes from 157.240.16.35: seq=8 ttl=49 time=1.144 ms
64 bytes from 157.240.16.35: seq=9 ttl=49 time=1.190 ms
64 bytes from 157.240.16.35: seq=10 ttl=49 time=1.197 ms
64 bytes from 157.240.16.35: seq=11 ttl=49 time=1.176 ms
64 bytes from 157.240.16.35: seq=12 ttl=49 time=1.240 ms
64 bytes from 157.240.16.35: seq=13 ttl=49 time=1.174 ms
64 bytes from 157.240.16.35: seq=14 ttl=49 time=1.275 ms
^C
--- fb.com ping statistics ---
15 packets transmitted, 15 packets received, 0% packet loss
round-trip min/avg/max = 1.141/1.245/1.845 ms

```
## checking container status

```
[ec2-user@ip-172-31-15-194 ~]$ docker   ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
[ec2-user@ip-172-31-15-194 ~]$ 
[ec2-user@ip-172-31-15-194 ~]$ docker   ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                          PORTS               NAMES
0396a2d549ed        alpine:latest       "ping fb.com"       2 minutes ago       Exited (0) About a minute ago                       ashuc1


```
