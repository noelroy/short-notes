# Docker
This is a short note I created while learning docker.

## What is container?
 - Layers of images
 - A way to package applications with dependencies and configurations.
 - Container is a running environment for the image.
 - Containers can be stored in :
   - Public repositories (Docker Hub)
   - Private repositories (AWS ECR)

## Why Docker?
 - Application can be installed using a single cmd
 - Multiple versions can be run as all of them run in isolated env

## Docker v/s Virtual Machine
Docker virtualizes Application layer alone. VM virtualizes OS Kernal and Application layer
Docker advantages
- Hence docker images are smaller in size
- It's faster to start

## Basic Commands

List active containers
```sh
docker ps
```
List all containers
```sh
docker ps -a
```
List all images
```sh
docker images
```

## Running Docker Image

Pull an image
```sh
docker pull ${image_name}
```
Pull and Run
```sh
docker run -d ${image_name}:${tag}
# -d = dettach
# --name ${name} = give container a name
# -p6000:6379 = port binding - host_port:container_port
# -e ${env_var_name} ${env_var_value} = add an env variable
# --network ${some-network} = attach a network
# -v ${host_folder}:${container_folder} = attach a volume 
```
Start a container
```sh
docker start ${container_name/id}
```
Stop a container
```sh
docker stop ${container_name/id}
```
## Debugging
Get container logs
```sh
docker logs ${container_name/id}
```
Get a terminal in the container
```sh
docker exec -it ${container_name/id} /bin/bash
or
docker exec -it ${container_name/id} sh
```
## Docker Networks
An isolated network where docker containers can communicate with each other using container names.
List all networks
```sh
docker network ls
```
Create a network
```sh
docker create network ${network_name}
```

## Docker Compose
A structured way to contain normal docker commands.
Docker compose takes care of creating a common network
Example :
```yml
version:'3'
services:
    mongodb:
        image: mongo
    mongo-express:
        image: mongo-express
        ports:
            - 8081:8081
        environment:
            - ME_CONFIG_MONGODB_SERVER=mongodb
```
To up a docker compose
```sh
docker-compose -f ${filename} up
# -f = filename
# -d = to start in detached mode
```
To down a docker compose
```sh
docker-compose -f ${filename} down
# -f = filename
# -d = to start in detached mode
```

## Docker File
Blueprint for creating docker images.
Docker file has to be named `Dockerfile` always.
```Dockerfile
# Use the official image as a parent image.
FROM node:current-slim

# set environmental variables
ENV MONGO_DB_USERNAME=admin\
    MONGO_DB_PWD=admin

# Set the working directory.
WORKDIR /usr/src/app

# Copy the file from your host to your current location.
COPY package.json .

# Run the command inside your image filesystem.
RUN npm install

# Run the specified command within the container.
CMD [ "npm", "start" ]

```
Docker build command
```sh
# Two parameters are used : image tag and dockerfile location 
docker build -t ${image_name}:${image_tag} .
# -t = specify tag
```
Its preferred to keep all env variables in the docker-compose file. If its kept inside docker file, we have to build the image each time we make a change to it.

## Private Repository (AWS-ECR)

Image Naming in Docker registeries - `registryDomain/imageName:tag`

Steps to push an image to the local repository

#### Create a repository
In AWS each image has separate repositories. The repository will contain different tags of the same repository.

#### Login to the private repository (docker login)
For AWS, they provide a command that uses docker login in the background.  For this AWS client needs to be installed and credentials configured

#### Tag our image - We have to tag out images 
We have to tag our image so that docker knows that the image has to be pushed to the private repo that we created
```sh
docker tag ${app-name}:${tag} ${registryDomain}/${imageName}:${tag}
```

#### Push the docker image to private repository
```sh
docker push ${registryDomain}/${imageName}:${tag}
```


## Docker Volumes
- For data persistence
- When a container is restarted or removed, all its data is lost.
- With volumes we are mounting a folder in host file system to the docker virtual file system

3 Volume types
- Host Volumes : we decide the host folder to be mounted. Eg: docker run -v /home/mount/data:/var/lib/mysql/data
- Anonymous Volumes : docker automatically creates a host folder and mounts it. Eg: docker run -v /var/lib/mysql/data
- Named volumes : docker created the host folder, but we can refer it using a name. Eg: docker run -v name:/var/lib/mysql/data

Defining volumes in docker compose
```yml
version:'3'
services:
    mongodb:
        image: mongo
        volumes:
        - db-data:/var/lib/mysql/data
volumes:
    db-data:
        driver: local
```

#### Docker volume location
Windows : C:\ProgramData\docker\volumes
Linux/Mac : /var/lib/docker/volumes

## Sample Projects
- [ToDo Node App](https://github.com/noelroy/docker-node-app#demo-node-app---developing-with-docker)