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


## Example 2 

```
❯ cat docker-compose.yml
version: "3.8"
services:
 ashuwebapp1:  # name of service first 
  image: alpine
  container_name: ashuc1
  command: ping google.com

 ashunginxapp1:  #  name of service second 
  image: nginx
  container_name: ashuc2
  ports:
   - "1199:80"
   
 ```
 
 ## compose related commands
 
 ```
 2979  docker  context  ls
 2980  docker-compose up  -d 
 2981  docker-compose ps
 2982  docker-compose logs 
 2983  ls
 2984  mv docker-compose.yml  ashu.yml
 2985  docker-compose ps
 2986  docker-compose -f  ashu.yml  ps 
 2987  docker-compose -f  ashu.yml  logs
 2988  history
 2989  ls
 2990  mv ashu.yml docker-compose.yml
 2991  docker-compose ps
 2992  docker-compose -v
 2993  docker-compose ps
 2994  docker-compose stop 
 2995  docker-compose ps
 2996  docker-compose start
 2997  history
 2998  docker-compose ps
 2999  docker-compose kill
 3000  docker context  ls
 3001  ls
 3002  docker-compose up -d
 3003  docker-compose -v
 3004  ls
 3005  docker-compose down 
 3006  history
 3007  ls
 3008  which docker-compose 
 3009  ls
 3010  vim  docker-compose.yml
 3011  cat docker-compose.yml
 3012  docker-compose up  -d
 3013  docker-compose ps
 3014  docker-compose kill  ashuwebapp1
 3015  docker-compose ps
 3016  docker-compose start
 3017  docker-compose ps
 3018  docker-compose  logs  ashuwebapp1
 3019  cat docker-compose.yml
 3020  docker-compose  logs  ashunginxapp1
 3021  history
 3022  cat  docker-compose.yml
 3023  docker-compose down
 
 ```
 
 ## docker cheet 
 
 [link] ('https://devhints.io/docker-compose')
 
 ## 
 
 docker-compose up --build  -d
 
 
# Container Orchestration Tools 

<img src="orch.png">

## GOogle history with k8s

<img src="k8shit.png">

## just overview of k8s & client architecture 

<img src="k8sL1.png">

## k8s master componet explain 

<img src="mastercomp.png">

## Minion node 

<img src="minion.png">

## system binary 

<img src="bin.png">

# K8s cluster deployment 

<img src="minikube.png">

## Installing minikube 

[minikube] ('https://minikube.sigs.k8s.io/docs/start/')

## Installing minikube on Mac 

```
❯ curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-darwin-amd64
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 54.8M  100 54.8M    0     0  6726k      0  0:00:08  0:00:08 --:--:-- 7957k
❯ sudo install minikube-darwin-amd64 /usr/local/bin/minikube
Password:
❯ minikube version
minikube version: v1.16.0
commit: 9f1e482427589ff8451c4723b6ba53bb9742fbb1

```

## deploy k8s cluster

```
❯ minikube start --driver=docker
😄  minikube v1.16.0 on Darwin 11.1
✨  Using the docker driver based on user configuration
👍  Starting control plane node minikube in cluster minikube
🚜  Pulling base image ...
🔥  Creating docker container (CPUs=2, Memory=1987MB) ...
🐳  Preparing Kubernetes v1.20.0 on Docker 20.10.0 ...
    ▪ Generating certificates and keys ...
    ▪ Booting up control plane ...
    ▪ Configuring RBAC rules ...
🔎  Verifying Kubernetes components...
🌟  Enabled addons: storage-provisioner, default-storageclass
🏄  Done! kubectl is now configured to use "minikube" cluster and "default" namespace by default

```

## Installation options

<img src="methodinstall.png">

## Installing kubectl on Mac

```
❯ curl -LO "https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/darwin/amd64/kubectl"
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 44.0M  100 44.0M    0     0  5528k      0  0:00:08  0:00:08 --:--:-- 5747k
❯ chmod +x ./kubectl
❯ sudo mv ./kubectl /usr/local/bin/kubectl
Password:
❯ 
❯ kubectl version --client
Client Version: version.Info{Major:"1", Minor:"20", GitVersion:"v1.20.1", GitCommit:"c4d752765b3bbac2237bf87cf0b1c2e307844666", GitTreeState:"clean", BuildDate:"2020-12-18T12:09:25Z", GoVersion:"go1.15.5", Compiler:"gc", Platform:"darwin/amd64"}

```

## link of kubectl 

[install]  ('https://kubernetes.io/docs/tasks/tools/install-kubectl/')


## checking connection 

====

```
❯ minikube status
minikube
type: Control Plane
host: Running
kubelet: Running
apiserver: Running
kubeconfig: Configured
timeToStop: Nonexistent

❯ kubectl  cluster-info
Kubernetes control plane is running at https://127.0.0.1:32780
KubeDNS is running at https://127.0.0.1:32780/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy

To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.
❯ 
❯ 
❯ kubectl  version
Client Version: version.Info{Major:"1", Minor:"20", GitVersion:"v1.20.1", GitCommit:"c4d752765b3bbac2237bf87cf0b1c2e307844666", GitTreeState:"clean", BuildDate:"2020-12-18T12:09:25Z", GoVersion:"go1.15.5", Compiler:"gc", Platform:"darwin/amd64"}
Server Version: version.Info{Major:"1", Minor:"20", GitVersion:"v1.20.0", GitCommit:"af46c47ce925f4c4ad5cc8d1fca46c7b77d13b38", GitTreeState:"clean", BuildDate:"2020-12-08T17:51:19Z", GoVersion:"go1.15.5", Compiler:"gc", Platform:"linux/amd64"}
❯ kubectl  get  nodes
NAME       STATUS   ROLES                  AGE    VERSION
minikube   Ready    control-plane,master   132m   v1.20.0

```
