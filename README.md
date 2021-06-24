## Spring Boot Docker Project

Used the following guide: https://spring.io/guides/gs/spring-boot-docker/
---

## Prerequisites

1. Install Docker Desktop 
2. Create an account at hub.docker.com
3. Create a Docker repository for this project: See "Setup Docker Repo" below

---

### Setup Docker Repo

Create Docker repository to match below settings in pom.xml

> ```<docker.image.prefix>dedjer</docker.image.prefix>```
> ```<repository>${docker.image.prefix}/${project.artifactId}</repository>```

Go to http://hub.docker.com

---

### Build and push to Docker Hub

> Create repository > lab-springboot-docker

Build project 

> mvn install dockerfile:build

Push image to Docker Hub

> docker push dedjer/lab-springboot-docker

---

### Try out your Docker image locally

Check that you have the image locally

> docker images

REPOSITORY                     TAG                 IMAGE ID            CREATED             SIZE
dedjer/lab-springboot-docker   latest              62cdd5aad631        5 minutes ago       125MB

Run your Docker image in a container and use port 5000 so you can view it in your browser

> docker run --name lab-docker -p 5000:8080 -t dedjer/lab-springboot-docker

Launch your browser to verify container is working.  You should see "Hello Docker World" if things worked.

> http://localhost:5000

Stop your Docker container

> CTRL-C

> docker stop lab-docker 

---

### Optional: Delete your container and image

Find your container id 

> docker ps -a

CONTAINER ID        IMAGE                          COMMAND                  CREATED             STATUS              PORTS                    NAMES
687f2a438c27        dedjer/lab-springboot-docker   "java -cp app:app/li…"   29 seconds ago      Up 27 seconds       0.0.0.0:5000->8080/tcp   lab-docker

Remove your container using the first 3 characters of the CONTAINER ID

> docker rm 687

Find your image id

> docker images

REPOSITORY                     TAG                 IMAGE ID            CREATED             SIZE
dedjer/lab-springboot-docker   latest              62cdd5aad631        5 minutes ago       125MB

Delete your image using the first 3 characters of the IMAGE ID

> docker rmi 62c

--- 

### Optional: Pull your Docker image from Docker hub

NOTE: This command can also be found on "Repositories" page at hub.docker.com 

> docker pull dedjer/lab-springboot-docker:latest

---

### Troubleshooting

Error during build: `denied: requested access to the resource is denied unauthorized: authentication required`

Solution: Make sure Docker Desktop is installed and you are logged into your Docker account