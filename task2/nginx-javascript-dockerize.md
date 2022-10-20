A Web App to Dockerize


Pull and Test Nginx 
- Nginx is a popular, fast web server
- Use Docker hub to pull nginx:alpine
    
    docker pull nginx:alpine

- Run nginx as a container

    docker run imageid

- Check web server in the browser

    http://localhost

Prepare Javascript app folder
- clone repo and put source files in a folder

    git clone https://github.com/mefekax/javascript-projects.git

- Prepare the app to work manually by copying source files into nginx folder

Create Dockerfile in app folder

'''
FROM nginx:alpine
COPY . /usr/share/nginx/html/
'''


Build image

    docker build -t javascript-app .





