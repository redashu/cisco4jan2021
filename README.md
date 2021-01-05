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
