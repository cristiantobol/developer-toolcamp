# Introduction to Docker

* [What is Docker?](#what)
* [Why Docker?](#why)
* [How Docker works](#how-docker-works)
* [What is a container?](#container)
* [What is an image?](#image)
* [Running a hello world docker container](#hello-world-docker)
* [Choosing a Mongo image](#choosing-an-image)
* [Running the Docker container](#running)
* [Stopping the Docker container](#stopping)
* [Restarting the Docker container](#restarting)
* [Using Docker Compose to create a Mongo database for the RestApi](#compose)
* [Building the image](#building)
* [Starting the Docker container](#starting)
* [Useful Docker commands](#useful)
* [Further reading](#further)

## Session Objective
This session will give an introduction to Docker. We will use Docker to run the MongoDB which is used in the Rest API application.  

<a name="what"></a>
## What is Docker?

> Docker unlocks the potential of your organization by giving developers and IT the freedom to build, manage and secure business-critical applications without the fear of technology or infrastructure lock-in.

Docker is computer software that allows you to run applications in containers.  Similar to the concept of running a server as a virtual machine.  However, the process of using and running docker applictions is fast, lightweight and takes seconds to spin up fully functioning applications and services.  

<a name="why"></a>
## Why Docker?

Docker is well suited to a DevOps strategy, allowing you to deploy self-contained applictions and then tear them down just a quickly when their job is done.  Because the process can be scripted, complex scenarios can be easily deployed and torn down when their job is done.

One such scenario could be a Continuous Integration pipeline.  The test process could involve spinning up a docker container, deploying the app to the container, running the tests against the app in the container.  When tests pass successfully, the container is torn down and the app deployed.

<a name="how-docker-works"></a>
## How Docker Works

<img src="./resources/session_docker_architecture.svg" alt="Docker architecture" />
Docker uses a client server architecture.  The Docker Client talks to the Docker daemon.  The client and the daemon could be on the same physical system, or they could be remote.

The Docker daemon listens for client requests and manages images, containers, networks, and volumes.  The daemon can also communicate with other Docker daemons.

The Docker client is the main way that users communicate with the Docker daemon using the [Docker client API](https://docs.docker.com/engine/reference/commandline/cli/).

A Docker Registry stores Docker images.  Docker Hub is a registry.  However, you can run your own Docker registry. An enterprise might use something like [Nexus](https://www.sonatype.com/products-overview) to run their own registry.

<a name="container"></a>
## What is a container?

> A container is a standard unit of software that packages up code and all its dependencies so the application runs quickly and reliably from one computing environment to another. A Docker container image is a lightweight, standalone, executable package of software that includes everything needed to run an application: code, runtime, system tools, system libraries and settings.

<a name="image"></a>
## What is an image?
To create a Docker container, an image is used.  This image can be a standard image available from [Docker Hub](https://hub.docker.com).  Or it can be custom image created using a `Dockerfile`.

> An image is essentially a snapshot of a container and a container is a running instance of an image.

<a name="hello-world-docker"></a>
## Running a hello world docker container
To run a simple Hello World Docker image, at the terminal run
```
$ docker run hello-world
```
This will download the `hello-world` image from Docker and run the container.  You should see a message output like this:
```
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
d1725b59e92d: Pull complete 
Digest: sha256:0add3ace90ecb4adbf7777e9aacf18357296e799f81cabc9fde470971e499788
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.
```

<a name="choosing-an-image"></a>
## Choosing a Mongo image

We could create our own Mongo image, but it is far better to use the official images from the Docker Hub.  They are well maintained and comprehensive.  They will also save us a huge amount of time.

Take a look at the MongoDB page on Docker Hub:
https://hub.docker.com/_/mongo/
  
<a name="running"></a>
## Running the Docker container
At the terminal, type the following command, which will download the image from Docker and start the container:
```
$ docker run --name Rest-Api -p 27017:27017 -v /data/db:/data/db -d mongo
```

Let's break down what this command does:  
`--name Rest-Api` sets the name of the docker container to Rest-Api  
`-p 27017:27017` maps the external port of the Docker container to the internal port  of the container.  This is the standard port for Mongo connectivity  
`-v /data/db` sets the host machines volume used for storing the Mongo data  
`-d` runs the container as a daemon  
`mongo` the name of the image to use. If no version is requested, the latest is used  

<a name="stopping"></a>
## Stopping the Docker container
Stopping the docker container is straight forward:
```
$ docker stop <container name>
```
<a name="restarting"></a>
## Restarting a Docker container
If you have named your Docker container using the ```--name``` switch as we did above, then you can restart your Docker container using the name:
```
$ docker start Rest-Api
```

<a name="deleting"></a>
## deleting a Docker container
Before we build and run our container using Docker compose, we will need to delete the existing Rest-Api container that we created on the command line above.
```
$ docker rm Rest-Api
```

<a name="exercise"></a>
## Using Docker Compose to create a Mongo database for the RestApi
Docker Compose allows you to spin up multiple containers with one command.  This is useful when chaining together multiple commands with multiple Docker containers.

1. Open the `developer-toolcamp-rest-api` project in VSCode.
2. In the terminal, cd to the directory of the `developer-toolcamp-rest-api`
```
$ git checkout completed-all-endpoints
```
3. Using VSCode, create a new file called `docker-compose.yml` in the `developer-toolcamp-rest-api` project. Copy the following into the file:
```
version: "3"
services:
  mongo:
    image: mongo:latest
    container_name: Rest-Api
    ports:
      - "27017:27017"
    volumes:
      - ./data/db:/data/db
  mongo-seed:
    build: .
    links:
      - mongo
```
4. We are spinning up two containers.  The `mongo` container doesn't use a Dockerfile, as we are simply using the latest mongo image from Docker Hub.  The `mongo-seed` container is responsible for copying over the data and importing the data into Mongo.  You would think that this could be done in one container, but if you try that, the container will error and exit.  So we use two containers, but following the data import, the mongo-seed container will exit.
5. Create a new file called `Dockerfile`.  Copy the following into the file:
```
FROM mongo:latest

COPY ./importData.json /data/importData.json

CMD mongoimport --db RecipesDB --collection recipes --drop --file /data/importData.json --jsonArray
```

<a name="build"></a>
## Building the image
```
$ docker-compose build
```

<a name="starting"></a>
## Starting the Docker container
```
$ docker-compose up -d // -d for starting in the background as a daemon
```

<a name="useful"></a>
## Useful Docker commands

```$ docker ps``` - lists all of the containers that are running

```$ docker stop <containerId>``` - stop a container

```$ docker exec -it some-mongo bash``` - access the Docker container using a bash shell

```$ docker logs some-mongo``` - view the Docker container logs

```$ docker rm <containerName>``` - deletes the container

<a name="further"></a>
## Further reading
[The MongoDB page on the Docker website](https://docs.docker.com/samples/library/mongo/)  

Take a look at the Docker website for [self paced training](https://training.play-with-docker.com)  

There are various courses on Udemy. Take a look at [Docker Mastery: The Complete Toolset From a Docker Captain](https://ibm-learning.udemy.com/docker-mastery/)  

Also, Safari Books Online have various books and videos [Docker: Dockerization with Docker - Build, ship, and scale your containers with ease using Docker](https://www.safaribooksonline.com/learning-paths/learning-path-docker/9781788997355/)  

