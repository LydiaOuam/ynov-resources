# The HumansBestFriend app 

A simple distributed application running across multiple Docker containers.

# Content : 
1. [Requirement](#requirement)
2. [Getting started](#getting-started)
3. [Tasks](#tasks)
4. [Create a registry](#create-a-registry)
5. [Tag the images](#tag-the-images)
6. [Push the images](#push-the-images)
7. [Create the docker compose file](#create-the-docker-compose-file)
8. [Create the network](#create-the-network)
9. [Run the docker compose](#run-the-docker-compose)

## Requirement


- The project is done inside a linux virtual machine.
- First we forked the project from the professor's git, then we clone it into the virtual machine. Since we just modify inside and push or pull if needed.

## Getting started


This solution uses Python, Node.js, .NET, with Redis for messaging and Postgres for storage.

## Tasks

### Create a docker compose build

We create a file called docker-compose.build.yml : this file was created and you can just finded by clicking on this [link](https://github.com/LydiaOuam/ynov-resources/blob/main/2023/m2/dataeng/humans-best-friend/docker-compose.build.yml). 
After that run the file using this command : 
```shell
    docker-compose -f docker-compose.build.yml up
```
Then you can check the creation of the images uding this command : 
```shell
    docker images
```
### Create a registry

Create a registry container uding this command : 
```shell
    docker run -d -p 5000:5000 --restart always --name registry registry:2
```
### Tag the images

Then we tagged all the images with localhost:5000 so we can push the to the private registry : 
```shell
    docker tag db localhost:5000/db
    docker tag result localhost:5000/result
    docker tag vote localhost:5000/vote  
    docker tag redis localhost:5000/redis
    docker tag worker localhost:5000/worker
    docker tag seed localhost:5000/seed-data  
```
But before this we renamed the postgres image uding this command : ```docker tag postgres db```

### Push the images
```shell
    docker push db localhost:5000/db
    docker push result localhost:5000/result
    docker push vote localhost:5000/vote  
    docker push redis localhost:5000/redis
    docker push worker localhost:5000/worker
    docker push seed localhost:5000/seed-data  
```

We can verify the existence of the images in the registry : 
```curl localhost:5000/v2/_catalog```


### Create the docker compose file

We created the docker compose file by respecting all the requirements that were indicated in the task, you can see the docker compose [here](https://github.com/LydiaOuam/ynov-resources/blob/main/2023/m2/dataeng/humans-best-friend/compose.yml).

### Create the network
 

Create a network called : `humansbestfriend-network`
```docker create network humansbestfriend-network ```

### Run the docker compose

Run the docker compose file using this command : 
``` docker-compose up ```
