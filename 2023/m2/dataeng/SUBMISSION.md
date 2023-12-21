# The HumansBestFriend app 

A simple distributed application running across multiple Docker containers.

# Content : 
1. [Requirement](#Requirement)
2. [Getting started](#gettingstarted)
3. [Tasks](#tasks)
4. [Create a registry](#registry)
    - [Create a docker compose build](#Create a docker compose build)
    - [Fonctionnalité 2](#fonctionnalite-2)
4. [Contributions](#contributions)


## Requirement
 <a name="Requirement"></a>

- The project is done inside a linux virtual machine.
- First we forked the project from the professor's git, then we clone it into the virtual machine. Since we just modify inside and push or pull if needed.

## Getting started
 <a name="gettingstarted"></a>


This solution uses Python, Node.js, .NET, with Redis for messaging and Postgres for storage.

## Tasks
 <a name="tasks"></a>
### Create a docker compose build

We create a file called docker-compose.build.yml : this file was created and you can just finded by clicking on this [link](https://github.com/LydiaOuam/ynov-resources/blob/main/2023/m2/dataeng/docker-compose.build.yml). 
After that run the file using this command : 
```shell
    docker-compose -f docker-compose.build.yml up
```
Then you can check the creation of the images uding this command : 
```shell
    docker images
```
### Create a registry
 <a name="registry"></a>

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
 <a name="pull"></a>



### Create the docker compose file : 
We created the docker compose file by respecting all the requirements that were indicated in the task, you can see the docker compose [here](https://github.com/LydiaOuam/ynov-resources/blob/main/2023/m2/dataeng/compose.yml).

### Create the network : 

Create a network called : `humansbestfriend-network`
```docker create network humansbestfriend-network ```

### Run the docker compose
Run the docker compose file using this command : 
``` docker-compose up ```


# Submission

- You need to submit your own public github repository with the required files (`Dockerfile`, `compose.yml`, `docker-compose.build.yml` etc....).
- You need to write a complete, clean README like a pdf rendering (summary, table of content, sections, images etc...)
- The work need to be done inside a virtual machine that run docker engine.
- You need to submit a complete and clean pdf file that demonstrate your work. This take a great part of your mark so please do it carefully.
- The deployment need to be done inside a network called `humansbestfriend-network`
- Dont forget to showcase that the containers can talk to each other using their ips and DNS names. A simple ping is enough.
- The submission readme file need to be called `SUBMISSION.md`
- The README should contain step by step guide to run your app. This target a developer visitor for example.
- The moodle is `HumansBestFriend`. You need to submit before 18AM today.
