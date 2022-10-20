# A Javascript Web App: Hands-on for Java Devs

In this activity we are going to pull Nginx image, run it on port 80, enter the container, install git and pull a javascript web app repo into nginx default folder and then preview on browser.


* Pull and Test Nginx 
- Nginx is a popular, fast web server
- Use Docker hub to pull nginx:alpine
    
    docker pull nginx:alpine

- Run nginx as a container

    docker run -p 80:80 imageID

- Check web server in the browser

    http://localhost

- exit the Nginx process rerun the container in detached mode 

    docker run -d -p 80:80 imageID

* Enter the container 

- now let's enter the container

    docker exec -it imageID /bin/sh

- now, note that we are inside running container(a running machine with OS), browse to Nginx Web Server default location

    cd /usr/share/nginx/html

- list the files and folders and see the default html files of Nginx

    ls -la

* Install dependencies, requirements

- now let's install git command line tool
- first update packages of this Os which is Alpine, a distro of Linux

    apk update

- now install git

    apk add git

- check if git is installed

    git --version

- clone Javascript app repo and source files

    git clone https://github.com/mefekax/javascript-projects.git

- list the files and folders

    ls -la

- now, we have to copy the files of the javascript-projects/reviews into this Nginx folder

    cp javascript-projects/reviews/* .

- list the files and folders again and see the files were copied

    ls -la

* Preview Web Page 
- now, refresh and check the browser

    http://localhost

- in the container, under Nginx default folder, rename html file

    mv index.html index.old

- go check the browser again

    http://localhost




- In this activity we pulled a Nginx Web Server image
- We made it run on port 80
- entered the running container
- installed git
- pulled a javascript web app repo 
- made Nginx serve our web page

- Congratulations!

