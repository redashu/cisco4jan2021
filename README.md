# Docker recap 

<img src="contrecap.png">

## creating and changing context 

```
❯ docker context create  remoteDE  --docker "host=tcp://52.66.251.242:2375"
remoteDE
Successfully created context "remoteDE"
❯ 
❯ docker  context  ls
NAME                TYPE                DESCRIPTION                               DOCKER ENDPOINT               KUBERNETES ENDPOINT   ORCHESTRATOR
default *           moby                Current DOCKER_HOST based configuration   unix:///var/run/docker.sock                         swarm
remoteDE            moby                                                          tcp://52.66.251.242:2375                            
❯ docker  context  use  remoteDE
remoteDE
❯ docker  context  ls
NAME                TYPE                DESCRIPTION                               DOCKER ENDPOINT               KUBERNETES ENDPOINT   ORCHESTRATOR
default             moby                Current DOCKER_HOST based configuration   unix:///var/run/docker.sock                         swarm
remoteDE *          moby                                                          tcp://52.66.251.242:2375                            


```

## Compose file versions

<img src="compose.png">

## compose file desing 

<img src="file.png">

## compose example 1 

```
❯ cat docker-compose.yml
version: "3.8"
services:
 ashuwebapp1:  # name of service first 
  image: alpine
  container_name: ashuc1
  command: ping google.com
  
```

## Deploy in remote De 

```
❯ docker-compose up  -d
Creating network "ashuapp11_default" with the default driver
Creating ashuc1 ... done
❯ docker-compose ps
 Name        Command       State   Ports
----------------------------------------
ashuc1   ping google.com   Up           
❯ docker-compose ps
 Name        Command       State   Ports
----------------------------------------
ashuc1   ping google.com   Up           
❯ docker-compose logs
Attaching to ashuc1
ashuc1         | PING google.com (216.58.203.142): 56 data bytes
ashuc1         | 64 bytes from 216.58.203.142: seq=0 ttl=110 time=1.941 ms
ashuc1         | 64 bytes from 216.58.203.142: seq=1 ttl=110 time=1.979 ms
ashuc1         | 64 bytes from 216.58.203.142: seq=2 ttl=110 time=1.985 ms
ashuc1         | 64 bytes from 216.58.203

```
