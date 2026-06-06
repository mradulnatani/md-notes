
## **Introduction**
- The issue: It works on my machine
- The solution: Containerize it
- Basically Docker is a tool which helps us to make containers, and these containers run applications inside them.
- Docker makes a OS independent environment and makes the system compatible for the libraries that are required

---

## **How did Docker came?**
There was a company names DotCloud which started facing the classic problem of "it works on my machine", so they decided to make a tool for building containers and they made it available in pycon in 2013 and in 2017 it became a CNCF tool.

---

## **Virtualization vs Containerization**

| Virtual Machines are used.                                                                                                   | Containerization tool like Docker, Podman, Containerd are used.                                                                                         |
| ---------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| uses Hypervisor: allocates resources from the system and runs the os on it. Vistual machines has there own operating system. | Docker engine uses the host operating system, do not require there own operating system. The system calls are made via the hosto operating system only. |
| Virtualization is heavy.                                                                                                     | Containers are light weight.                                                                                                                            |

---

## **Docker Architecture**
- Docker Engine: Application container engine, which runs all the applications.
- Docker Daemon: Background service to manage all the running applications. Dockerd runs containerd internally
- Docker CLI: Interface to interact.
- Docker Client: Connects APIs and communicates to docker engine and gives as a GUI view of our containers.

---
## **Docker Images and Containers**

```
docker ps (to see the running continers/processes)
docker images (to see the available docker images)
```

A Docker image is a read-only blueprint that contains the source code, libraries, dependencies, and runtime required to run an application, while **a Docker container is the live, runnable instance** created from that image. A docker image is written using a Dockerfile.

Docker file has instructions -> these instructions create image -> this image can be replicated in the form of containers.

Dockerfile -> image -> container
        (build)   (run)


```
docker pull hello-world
```
The docker pull command is used to pull a pre-defined image from the docker hub.

```
docker run hello-world
```
This command will run the container for the image.


- Adding env to the docker containers
```
docker run -e MYSQL_ROOT_PASSWORD=root mysql
```

- "Use -d to run the container in the background"

```
docker stop {container id}
docker start {container id}
```


---

## **How to write a Dockerfile?**

```
FROM {base_image_name:image_version}           #pulls base image

WORKDIR /app                                   #directory in the container                                                       where the application code will                                                  reside

COPY . .                                       #copy code from the current                                                       location to container's workdir

RUN apt-get update && apt-get install -y curl  #executes commands at image                                                       build time

CMD ["python","app.py"]                        #specifies the default command                                                    executed at container runtime

ENTRYPOINT                                     #similar to CMD but it cannot be                                                  overridden
```
- CMD can be override at the time of docker run command, but ENTRYPOINT cannot be overridden, both of these commands are used to inject commands in the running containers.


#### How to make a docker image from a Dockerfile?

```
docker build -t test-app . 
```

-t -> gives a tag or name to the docker image
 . -> give the context of the Dockerfile (location of the Dockerfile to      be used)

```
docker run test-app
```
- This will run the docker image as a container
- Everytime there is a change in the source code the Docker image should be updates using "docker build" command.

-> Port mapping
```
docker run -p 80:80 test-app 
```
- Host Port : Container Port
- -p : publish

-> How to get inside a docker container
```
docker exec -it {container id} bash
```
- -it : interactive terminal
- bash : shell name

---
## Docker Networking
Imagine your computer runs multiple docker containers and both the containers are isolated in nature, but if we want both of these containers to communicate we need a network for that.

-> Types of Docker networks
 1. Host (docker m/c and host m/c 's networks are same)
 2. Bridge (bridges the network between host and the container,               it is the default network for docker)
 3. User defined Bridge (custom bridge)
 4. None (completely isolated container)
 5. MACVLAN (network in which communication happens via 2 MAC                  addresses, used in docker swarm)
 6. IPVLAN  (used in docker swarm)
 7. Overlay (used in docker swarm)


```
docker network ls
```
- Shows all the available docker networks.

```
docker network create mynetwork -d bridge
```
- -d : drivers
- creates a bridge type network

-> How to give network to the containers?
```
	docker run -d --name mysql --network two-tier -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=devops mysql:latest
```
- To get information about the network:
```
docker network inspect two-tier 
```


---
## Docker Volumes and Storage
When we delete our docker containers the data which was not persistent in nature will we erased.
For saving our data after a crash we bind our data with our host machine which are called volumes.

```
docker volume ls
```
- Shows all the docker volumes that are currently available or are in existence.

```
docker volume create mysql-data
```
- A docker volume can be inspected using the "docker inspect {volume name}"
- binding of the container with the host path of the volume:
```
docker run -d --name mysql --network two-tier -v mysql-data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=devops mysql:latest
```

---

## Docker Compose
Docker compose is a config file that is a yaml/yml file