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
   
   
