# Docker course
To turn hyper v on
* search `turn windows features on or off`

## Setup nginx docker
* To pull nginx webserver and run it use following command
```bash
docker run --publish 80:80 nginx
```
* to run container in background use detach command
```bash
docker run --publish 80:80 --detach nginx
```
* to stop container
```bash
docker stop <<container_id>
```
* To start a stopped container
```bash
docker start <<container_id>
```
* To list running Containers
```bash
docker ps -a
```
or use
```bash
docker container ls -a
```
* To view logs of a detached container
```bash
docker container logs <<container_id>
```
* To view processes running in a detached container
```bash
docker container top <<container_id>
```
* To remove a docker container
```bash
docker container rm <<container_id>
```
* To forcefully remove a container
```bash
docker rm -f <<container_id> 
```
* To view the Utilization of the docker containers running in the docker Engine
```bash
docker stats
```
* To go back to a container or attach use the following
```bash
docker start -ai <<container_id>
```

* To get inside a shell in a container use the following
```bash
docker run -it <image_name> bash
```
* to run additional command in an existing container
```bash
docker run exec -it <container_name> bash
```

### Docker Networks
```bash
docker run --publish 80:80 --name <container_name> --detach nginx
```
To view used ports
```bash
docker port <<continer_name>
```
* TO view the Ip address of a docker container
```bash
docker container inspect --formart '{{ .NetworkSettings.IPAddress}}' <<container_name>
```
To view the network options on your docker Engine
```bash
docker network ls
```
docker network management commands
* show networks `docker network ls`
* inspect a network `docker network inspect`
* create a network `docker network create --driver`
* attach a network to container `docker network connect <container_id> <network_name>`
* detach a network from container `docker network disconnect <container_id> <network_name>`


* DNS naming in Docker
* a container can talk to another container on the same network using their container name or id
* eg a container can ping another container if they are on the same network using the container name and not the ip address
create a new network
```bash
docker network create <<new_network>
```
add a container to the new network
```bash
docker run -d --name emeka --network <<new_network> apline 
```
add another container
```bash
docker run -d --name another --network <<new_network> apline 
```
check network connectivity using ping
```bash
docker container exec -it emeka ping another
```
* in this case `emeka` and `another` are the container names

`Note`
* To delete a container after run
```bash
docker container run --rm -it centos:7 bash
```


## Docker Images
* To view images
```bash
docker images
```
* To see image history
```bash
docker image history <<image_name>>
```
* To inspect an image
```bash
docker image inspect <<image_name>>
```
* TO create an image tag
```bash
 docker tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]
```

### Build Docker image
To build a docker image create an image and save it as a Dockerfile
* You can use the Dockerfile in the docker image alpine folder.
* To build from that image, clone the repo and navigate to the folder 
and then run the following command
```bash
docker image build -t cusniginx .
```
 #### sample format to build an image and copy a file in the folder into that image
 
 ```Dockerfile
FROM nginx:lastest
# base image

WORKIR /usr/share/nginx/html
# change working directory 

COPY index.html index.html
# copy file without changing the name

```
* save the file as `Dcokerfile`
* To build run `docker image build `















































