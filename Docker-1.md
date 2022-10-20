# Hands-on Docker-02 : Docker Container Basic Operations

Purpose of the this hands-on training is to give Java Dev students the knowledge of basic operations on Docker containers.

## Learning Outcomes

At the end of the this hands-on training, students will be able to;

- list the help about the Docker commands.

- list the running and stopped Docker containers.

- understand the properties of Docker containers.

- start, stop, and remove Docker containers.
  
- understand running interactive mode 

- understand difference between an image and a container


## Basic Container Commands of Docker


  - Check whether the docker is up and running by using the following command.

```bash
  docker version
```

- Run either `docker` or `docker help` to see the help docs about docker commands.

```bash
docker help | less
```

- Run `docker COMMAND --help` to see more information about specific command.

```bash
docker run --help | less
```



- Run `hello-world` as a first image and container. To pull and run hello-world official image, use the following command.

```bash
docker run hello-world
```

- Show the list of all containers available on Docker machine and understand container properties.
- To see the `running containers`;  

```bash
docker ps
```

- To see the `running and exited/stopped containers`;  

```bash
docker ps -a
```

- Download and run `ubuntu` container.

```bash
docker run -it ubuntu bash
```


- Display the os name on the container for the current user.

```bash
uname -a
```

- Display the shell name on the container for the current user.

```bash
echo $0
```


- Run the second `ubuntu` os with interactive shell open and name container as `backend` and show that this `ubuntu` container is different from the previous one.

```bash
docker run -i -t --name backend ubuntu
```

- Exit the `ubuntu` container and return to user shell.

```bash
exit # to stop the process
```

- Show the list of all containers again and understand the second `ubuntu` containers' properties and how the names of containers are given.

```bash
docker ps -a
```

- Connect to the interactive shell of running `ubuntuiki` container, check if docker is installed and `exit` afterwards.

```bash
docker start backend && docker attach backend
docker version
```

- explain that docker is not installed inside the container

- Show that `backend` container has stopped by listing all containers.

```bash
docker ps -a
```

- Show that we can get more information about `backend` container by using `docker inspect` command and see the properties.

```bash
docker inspect backend | less
# Cikmak icin q veya crtl c'ya basin
```

- Delete the first container using its `ID`.

```bash
docker stop ContainerID && rm ContainerID
```

- Delete the second container using its name.

```bash
docker rm backend
```

- Or you can use `prune` command as well

```bash
docker container prune
```

- Show that both of containers are not listed anymore.

```bash
docker ps -a
```

- See if there are images 

docker images
docker image ls

- Get more detail on one of the images using inspect

docker image inspect imageID

Let us try some popular images

  docker pull rancher/cowsay
  docker run imageID merhaba!

- use a web server as a container

  docker pull nginx:alpine
  docker run -d -p hostport:containerport imageID

- play supermario

  docker run -d -p 8600:8080 pengbai/docker-supermario

- run a container with a command output

  docker run alpine uname
  docker run alpine ls

Let's pull a Mysql Database and run it as a container

  docker pull mysql:latest
  docker container run --detach --name mydb -e MYSQL_ROOT_PASSWORD=java-dev mysql:latest

- see logs 

  docker logs containerID


Remove containers and images

- Stop runnings containers

  docker ps
  docker stop

- remove containers

  docker ps -a
  docker rm 

- remove images

  docker image ls
  docker rmi imageID

  