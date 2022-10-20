# Docker for Java Devs: Sample Java archive to be deployed on Tomcat Server

This is the hands-on document on how to build a Java app, package and create as a Docker image and deploy it on a Tomcat Server.
Java app will be packed as WAR file and Tomcat will be used.
In this Java Spring Boot Initializer app, Spring Web and Spring Boot Actuator are used.
Actuator endpoint is going to be used as 
http://localhost:port/actuator/health
It returns results in Json format.


## Instructions

- Open the project folder (springboot2-6-3-war-java-17) in the IntelliJ Idea Project Tools Menu.
- While the main folder name is selected open the Terminal in the panel below.
- a bash or git bash terminal should open
- type in ls to view the files and folders
- they should look like :

..... Dockerfile
..... mvnw
..... mvnw.cmd
..... pom.xml
..... run-demo.bat
..... run-demo.sh
..... src

- now check the java version

```$ java --version
```
- you may see another version

java version "15.0.1" 2020-10-20
Java(TM) SE Runtime Environment (build 15.0.1+9-18)
Java HotSpot(TM) 64-Bit Server VM (build 15.0.1+9-18, mixed mode, sharing)

- note the version of Java in the application

- now build the Docker image

    docker build -t demoapp .

- list the images

    docker images 
    docker image ls


- and now run a container using the image we just created

    docker run -name mydemoapp -p 8080:8080 -d demoapp

- check the runnings containers

    docker ps

- test the application

    curl localhost:8080/actuator/health
    or put on a browser

- list the containers again

    docker ps

- execute a shell command and enter the container

    docker exec -t -i mydemoapp /bin/sh

- now we are inside the container which we ran from the image we created

- type some commands

    ls
    pwd
    java -version
    ls /usr/local/tomcat

- note that the development environment, all source, runtime etc are included in this container.

- now exit from the container

    exit

- stop the container

    docker stop mydemoapp

- see all containers

    docker ps -a

- remove the container

    docker rm mydemoapp

- remove the image

    docker rmi demoapp


## Outcome

Here we built a Java Application that will be served on Tomcat Server. 
We observed that the development environmet, dependencies, runtime and libraries are included inside the container we ran from the image.

