## 1. Basic Syntax Structure
A typical docker-compose.yml looks like this:

````yaml
version: "3.9"
services:
service_name:
image: image_name:tag
container_name: custom_name
build:
context: .
dockerfile: Dockerfile
ports:
- "HOST:CONTAINER"
volumes:
- "HOST_PATH:CONTAINER_PATH"
environment:
VAR_NAME: value
restart: always
depends_on:
- another_service

````
## 2. Explanation of Each Docker Compose Command

* version
#### Specifies Docker Compose file format version.
````yml
version: "3.9"
````


* image
#### Runs a container from a Docker Hub image.
````yml
image: nginx:latest
````

* build
#### This tells Docker to build a custom image using a Dockerfile.
````yml
build:
  context: .
  dockerfile: Dockerfile
````
context: folder where your Dockerfile exists

dockerfile: name of the Dockerfile

* container_name
#### Gives your container a readable name.
````yml
container_name: laravel_php
````

* ports
#### Maps container ports → your machine’s ports
````yml
ports:
  - "80:80"
````
Format:

HOST_PORT : CONTAINER_PORT

* volumes
#### Attaches your machine’s folders into the container.
````yml
volumes:
  - ./src:/var/www/html
````
This means:

Use my local folder src inside the container at /var/www/html

This is how Laravel code is shared with PHP & Nginx containers.


* environment
#### Sets environment variables inside the container.
````yml
environment:
  MYSQL_ROOT_PASSWORD: example
  MYSQL_DATABASE: test_database
````

* restart
#### What to do if container stops.
````yml
restart: always
restart: unless-stopped
restart: on-failure
````


* depends_on
#### Start one service before another.
````yml
depends_on:
  - db
````
Meaning:
Start db container before starting php.

### 3. Global Docker Commands You Will Use

* Start services:
````yml
docker-compose up -d
````

* Stop all services:
````yml
docker-compose down
````

* Rebuild (after changing Dockerfile):
````yml
docker-compose up --build -d
````

* View logs:
````yml
docker-compose logs -f
````

* Restart only one container:
````yml
docker-compose restart php
````