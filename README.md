# Docker best practise 

<img src="remotecre.png">

## access docker engine from WEbUI  using portainer 

```
docker run -d --name ashuwebui -v /var/run/docker.sock:/var/run/docker.sock -p 9000:9000 portainer/portainer 
```

# image registry 

<img src="reg.png">

## type of image registry 

<img src="regt.png">

## Dockerfile 

```
[ec2-user@ip-172-31-6-16 project-html-website]$ cat  Dockerfile 
FROM nginx
MAINTAINER  ashutoshh@linux.com
WORKDIR  /usr/share/nginx/html/
COPY . . 
EXPOSE 80

```

## .dockerignore file 

```
[ec2-user@ip-172-31-6-16 project-html-website]$ cat .dockerignore 
Dockerfile
.dockerignore
.git
*.md
LICENSE

```

## building 
```
[ec2-user@ip-172-31-6-16 project-html-website]$ docker build  -t  ciscoweb:httpv1  . 
Sending build context to Docker daemon  833.5kB
Step 1/5 : FROM nginx
latest: Pulling from library/nginx
6ec7b7d162b2: Pull complete 
cb420a90068e: Pull complete 
2766c0bf2b07: Pull complete 
e05167b6a99d: Pull complete 
70ac9d795e79: Pull complete 
Digest: sha256:4cf620a5c81390ee209398ecc18e5fb9dd0f5155cd82adcbae532fec94006fb9
Status: Downloaded newer image for nginx:latest
 ---> ae2feff98a0c
Step 2/5 : MAINTAINER  ashutoshh@linux.com
 ---> Running in 81cf7f4ddc22
Removing intermediate container 81cf7f4ddc22
 ---> 8d723d43fca8
Step 3/5 : WORKDIR  /usr/share/nginx/html/
 ---> Running in 97e2e2180ecc
Removing intermediate container 97e2e2180ecc
 ---> ce9a3c934299
Step 4/5 : COPY . .
 ---> cca736bb5959
Step 5/5 : EXPOSE 80
 ---> Running in 101d9c66f93a
Removing intermediate container 101d9c66f93a
 ---> abffbd642bc9
Successfully built abffbd642bc9
Successfully tagged ciscoweb:httpv1

```


## image name reality 

<img src="imgname.png">

## Pushing image to docker hub 

## loging to docker hub 

```
[ec2-user@ip-172-31-6-16 project-html-website]$ docker  login  
Login with your Docker ID to push and pull images from Docker Hub. If you don't have a Docker ID, head over to https://hub.docker.com to create one.
Username: dockerashu
Password: 
WARNING! Your password will be stored unencrypted in /home/ec2-user/.docker/config.json.
Configure a credential helper to remove this warning. See
https://docs.docker.com/engine/reference/commandline/login/#credentials-store

Login Succeeded

```
## pushing image on docker hub 

```
[ec2-user@ip-172-31-6-16 project-html-website]$ docker  tag  ciscoweb:httpv1   dockerashu/ciscoweb:httpv1 
[ec2-user@ip-172-31-6-16 project-html-website]$ docker push dockerashu/ciscoweb:httpv1 
The push refers to repository [docker.io/dockerashu/ciscoweb]
f5b390952830: Pushed 
4eaf0ea085df: Mounted from library/nginx 
2c7498eef94a: Mounted from library/nginx 
7d2b207c2679: Mounted from library/nginx 
5c4e5adc71a8: Mounted from library/nginx 
87c8a1d8f54f: Mounted from library/nginx 
httpv1: digest: sha256:79bf0bdcaec740853881f33d3a41214470315d7a1ee72c218468bf6b4fafd218 size: 1572

```

# Docker networking 

## default docker bridge 

```
[ec2-user@ip-172-31-6-16 ~]$ ifconfig  docker0
docker0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 172.17.0.1  netmask 255.255.0.0  broadcast 172.17.255.255
        inet6 fe80::42:6cff:fedb:162  prefixlen 64  scopeid 0x20<link>
        ether 02:42:6c:db:01:62  txqueuelen 0  (Ethernet)
        RX packets 9961  bytes 5572858 (5.3 MiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 9354  bytes 1327543 (1.2 MiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
        
   ```
   
   
   ## docker0 bridge
   
   <img src="docker0.png">
   
   ## checking ip of container 
   
   ```
   docker inspect x1
   ===
         "Networks": {
                "bridge": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": null,
                    "NetworkID": "49019c7e83f0ceff32e925d99bb088fc2d857f609d25b05ba119997cbe062812",
                    "EndpointID": "c002e27d6a0aeea09903069adc13adab9a0a6ca00c9c1e7a995e96fb835fd693",
                    "Gateway": "172.17.0.1",
                    "IPAddress": "172.17.0.2",
                    "IPPrefixLen": 16,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "MacAddress": "02:42:ac:11:00:02",
                    "DriverOpts": null
                }
            }
        }

```

## NAT 

<img src="nat.png">

