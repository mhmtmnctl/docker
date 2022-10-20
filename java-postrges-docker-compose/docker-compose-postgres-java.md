# Dcoker Compose Activity: Hands-on For Java Devs

## Learning Outcomes

At the end of the this hands-on training, students will be able to;

- explain what Docker Compose is.

- explain what the `docker-compose.yml` is.


## Docker Compose sample application

In this Java Spring Boot applicaiton there is the backend of a Blog.
Blog uses Postgresql Database

This application can be run using Docker in 2 ways. One with step by step, other is using docker compose.

To start, use IntelliJ to open the app main folder.
then use the Terminal panel at the bottom of IntelliJ screen.

### Manually
```
docker network create blog-network
docker run --name postgres-db -e POSTGRES_DB=blogdemo --network blog-network -e POSTGRES_PASSWORD=lmnop -v db-data:/var/lib/postgresql/data -p 5432:5432 -d postgres
docker build -t blog-backend .
docker run --name blog-backend-app -p 8080:8080 -network blog-network -e POSTGRES_HOST=db -e POSTGRES_DB=blogdemo -e POSTGRES_PASSWORD=lmnop -d blog-backend
```
```
docker stop postgres-db blog-backend-app
docker rm postgres-db blog-backend-app
docker network rm blog-network

```
```
curl -X POST "http://localhost:8080/blogs"  -H  "Content-Type: application/json" -d "hello"
curl localhost:8080/blogs
curl localhost:8080/stop
docker rm blog-backend app

```
### Automated using docker-compose
```
docker-compose up
docker-compose down
```


use terminal 

    curl localhost:8080/actuator/health
    curl localhost:8080/blogs
    curl -X POST "http://localhost:8080/blogs"  -H  "Content-Type: application/json" -d "hello"

use a web browser

    localhost:8080/actuator/health
    localhost:8080/blogs


### Conclusion

In this activity we used docker compose to run an application with 2 tiers, backend and database.