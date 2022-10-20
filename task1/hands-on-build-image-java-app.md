Docker is based on Linux OS kernel
Images are created using distributions of Linux.

# BUILDING DOCKER IMAGES: Hands-on for Java Devs

Dockerfile is a text file, a set of commands to build a Docker image.

## Simple Alpine Image
Alpine is a very light Linux OS

- First create a simple Dockerfile
put those two lines inside a file named exactly as :
Dockerfile

FROM alpine
CMD ["ls"]

This means, use alpine linux image, the image is downloaded from Docker hub like Github and give ls command to list folder in the alpine image

- Now, build image using build command:

    docker build -t myimage .

This command builds the image using Dockerfile with/without using any parameters or arguments

The image created is based on alpine Linux and executes a list command on the root folder of the container.


- list images
docker images

- run the created image using the image id
docker run --name myosimage imageid

- delete the container
docker rm container name or id

- delete the image
docker rmi imageid


## Simple Java App
# version 1
Go to Hello app folder
there is a Dockerfile and a Hello.java file
- first compile the java file using

javac Hello.java

- after compilation you will have Hello.class in addition to other files

- now first inspect and review the Dockerfile, then build the image

FROM openjdk:15.0.1
COPY ./Hello.class /
CMD ["java", "Hello"]

- then build the image and run

docker build -t yourdockerhubusername/myjavaapp:1 .
docker run --name myjavaapp1 imageid

# version 2
Go to Hello app folder
there is a Dockerfile and a Hello.java file

- now first inspect and review the Dockerfile, then build the image

FROM openjdk:17  
COPY . /app  
WORKDIR /app  
RUN javac Hello.java  
CMD ["java", "Hello"]  

- then build the image and run

docker build -t yourdockerhubusername/myjavaapp:2 .
docker run --name myjavaapp2 imageid


# PUSHING YOUR IMAGES TO YOUR DOCKER HUB REPO

Now we have 2 different versions of Java App, let's push them to our repo.


    docker push yourdockerhubusername/myjavaapp:1
    docker psuh yourdockerhubusername/myjavaapp:2
     



