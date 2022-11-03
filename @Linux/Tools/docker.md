#migrate to root user  
`docker run -v /:/mnt --rm -it alpine chroot /mnt sh`

#docker man:
```
docker run \ #run container or id
-v /path/from/mount/:/path/to/mount \ #mounted path
--name container_name \ #contaner name
-d \  #daemon 
-it \ #interactive terminal
--rm \ #remove containers from ps
-p 8080:80 #ports to map to:from
```

`docker container inspect container_name` #docker shows config
#docker show all processes
`docker ps -a`
`docker run container_name or id`
`docker stop container_name or id`

#docker_crear list of stoped containers
`docker container prune`

#docker_config 

```
FROM python:alpine

WORKDIR /app

RUN pip install pymongo

COPY . .

CMD ["python", "main.py"]
```
`docker images` #shows docker local containers
#build_docker_container
`docker build . -t my-docker-container:4.1.3` #or:latest #create_docker_container

```
version: '3'

  

services:

app:

build: ./app

mongo:

image: mongo
```

```
FROM python:alpine

WORKDIR /app

RUN pip install pymongo

COPY . .

CMD ["python", "main.py"]
```
`docker compose up -d` #docker_as_daemon
`docker compose up -d --build` #docker_rebuild 