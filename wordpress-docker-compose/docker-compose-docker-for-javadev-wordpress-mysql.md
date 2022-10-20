# Hands-on Docker-Compose : Compose and WordPress

- Purpose of the this hands-on  use Docker Compose to easily run WordPress in an isolated environment built with Docker containers. This hands-on demonstrates how to use Compose to set up and run WordPress. Before starting, make sure you have Compose installed.

## Learning Outcomes

At the end of this hands-on training, students will be able to;

- explain what Docker Compose is.

- explain what the `docker-compose.yml` is.

- build a `wordpress` and `MYSQL Database`  application running on Docker Compose.

## STEPS

## Building a WordPress application in an isolated environment built with Docker containers

- Create an empty project directory.
  
```bash
mkdir my_wordpress/
```

- Change into your project directory.

```bash
cd my_wordpress/
```
- Create a docker-compose.yml file that starts your WordPress blog and a separate MySQL instance with volume mounts for data persistence:

```yaml
version: "3.9"
    
services:
  db:
    image: mysql:5.7
    volumes:
      - db_data:/var/lib/mysql
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: somewordpress
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wordpress
      MYSQL_PASSWORD: wordpress
    
  wordpress:
    depends_on:
      - db
    image: wordpress:latest
    volumes:
      - wordpress_data:/var/www/html
    ports:
      - "8000:80"
    restart: always
    environment:
      WORDPRESS_DB_HOST: db:3306
      WORDPRESS_DB_USER: wordpress
      WORDPRESS_DB_PASSWORD: wordpress
      WORDPRESS_DB_NAME: wordpress
volumes:
  db_data: {}
  wordpress_data: {}
```

- The docker volumes ```db_data``` and ```wordpress_data``` persists updates made by WordPress to the database, as well as the installed themes and plugins.

- WordPress Multisite works only on ports ```80 and 443```.

## Building the project


- Now, run `docker-compose up -d` from your project directory.

```bash
docker-compose up -d
```

- This runs docker-compose up in detached mode, pulls the needed Docker images, and starts the `wordpress` and `MYSQL database` containers.


## Bringing up WordPress in a web browser

- At this point, WordPress should be running on port 8000 of your Docker Host, and you can complete the “famous five-minute installation” as a WordPress administrator.

- If you are using Docker Desktop for Mac or Docker Desktop for Windows, you can use http://localhost as the IP address, and open http://localhost:8000 in a web browser.


## Shutting down and cleanup

- The command docker-compose down removes the containers and default network, but preserves your WordPress database.

```bash
docker-compose down
```
- The command docker-compose down --volumes removes the containers, default network, and the WordPress database.

```bash
docker-compose down --volumes
```

- You can remove the images by

  docker rmi imageID