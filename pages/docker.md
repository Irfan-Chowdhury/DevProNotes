<div align='center'>

# Docker Related Commands
</div>


### 1. Docker Basic/Regular Commands

| **Command**      | **Description**            |
|------------------|----------------------------|
| `docker --version` | Show Docker version information. |
| `docker info`    | Display system-wide information about Docker. |
| `docker help`    | List all Docker commands or get help for a specific command. |
| `docker-compose build`                   | Build or rebuild services.               |
| `docker-compose stop`                    | Stop running containers.                 |
| `docker-compose start`                   | Start stopped services.                  |
| `docker-compose up`                      | Create and start containers.             |
| `docker-compose up -d`                   | Start containers in detached mode.       |
| `docker-compose down`                    | Stop and remove containers, networks, and volumes created by `up`. |
| `docker ps`                   | To Check Container Running.                  |
| `docker exec -it php-task bash`                   | Enter Container                  |
| `docker ps -a`                   | List All Containers (Including Stopped Ones)                  |
| `docker rm laravel_app`                   | Remove the Conflicting Container                  |
| `docker-compose up -d`                   | Restart Docker Compose                  |
| `docker stop $(docker ps -q)`                   | Stop All Running Containers                  |
---

### If the conflicting container is found, stop and remove it:

```bash
docker stop <container_id>
docker rm <container_id>
```

### If the already exists container name :

- Stop the Running Container
```bash
docker stop <container_name>
```
- Remove the Container
```bash
docker rm <container_name>
```
- Restart Docker Compose
```bash
docker-compose up -d
```
### Enter Container :

```bash
docker exec -it laravel-doc-app bash
```

### Run Server to Change the port on 0.0.0.0:

```bash
php artisan serve --host=0.0.0.0
```

### Exit Container :

```bash
exit
```

### Access Database :

- Let your port is look like that 
```bash
  phpmyadmin:
    image: phpmyadmin:latest
    ports:
      - 9003:80
```

- Now access to : http://localhost:9003





### 2. Container Management

| **Command**                             | **Description**                          |
|-----------------------------------------|------------------------------------------|
| `docker ps`                             | List running containers.                 |
| `docker ps -a`                          | List all containers (including stopped ones). |
| `docker start <container_name>`         | Start a stopped container.               |
| `docker stop <container_name>`          | Stop a running container.                |
| `docker restart <container_name>`       | Restart a container.                     |
| `docker rm <container_name>`            | Remove a container.                      |
| `docker exec -it <container_name> bash` | Access a container's shell interactively. |
| `docker logs <container_name>`          | View the logs of a container.            |
| `docker inspect <container_name>`       | Get detailed information about a container. |
| `docker top <container_name>`           | Display running processes inside a container. |
| `docker stats`                          | Display real-time resource usage statistics for containers. |
| `docker kill <container_name>`          | Force-stop a container.                  |

---

### 3. Image Management

| **Command**                           | **Description**                          |
|---------------------------------------|------------------------------------------|
| `docker images`                       | List all Docker images on the host.      |
| `docker pull <image_name>`            | Pull an image from a Docker registry (e.g., Docker Hub). |
| `docker build -t <image_name> .`      | Build a Docker image from a Dockerfile.  |
| `docker rmi <image_name>`             | Remove a Docker image.                   |
| `docker tag <image_id> <new_image_name>` | Tag an image with a new name or version. |
| `docker save -o <file_name>.tar <image>` | Save an image to a tar file.            |
| `docker load -i <file_name>.tar`      | Load an image from a tar file.           |

---

### 4. Network Management

| **Command**                              | **Description**                          |
|------------------------------------------|------------------------------------------|
| `docker network ls`                      | List all Docker networks.                |
| `docker network inspect <network_name>`  | Inspect a specific Docker network.       |
| `docker network create <network_name>`   | Create a new Docker network.             |
| `docker network connect <network_name> <container>` | Connect a container to a network. |
| `docker network disconnect <network_name> <container>` | Disconnect a container from a network. |
| `docker network rm <network_name>`       | Remove a Docker network.                 |

---

### 5. Volume Management

| **Command**                              | **Description**                          |
|------------------------------------------|------------------------------------------|
| `docker volume ls`                       | List all Docker volumes.                 |
| `docker volume create <volume_name>`     | Create a new volume.                     |
| `docker volume inspect <volume_name>`    | Inspect a specific volume.               |
| `docker volume rm <volume_name>`         | Remove a volume.                         |

---

### 6. System Cleanup

| **Command**                              | **Description**                          |
|------------------------------------------|------------------------------------------|
| `docker system df`                       | Show Docker disk usage information.      |
| `docker system prune`                    | Remove unused containers, networks, images, and volumes. |
| `docker image prune`                     | Remove dangling (unused) images.         |
| `docker container prune`                 | Remove all stopped containers.           |
| `docker volume prune`                    | Remove unused volumes.                   |
| `docker network prune`                   | Remove unused networks.                  |

---

### 7. Docker Compose

| **Command**                              | **Description**                          |
|------------------------------------------|------------------------------------------|
| `docker-compose up`                      | Create and start containers.             |
| `docker-compose up -d`                   | Start containers in detached mode.       |
| `docker-compose down`                    | Stop and remove containers, networks, and volumes created by `up`. |
| `docker-compose ps`                      | List containers managed by `docker-compose`. |
| `docker-compose logs`                    | View logs for all services in a Compose project. |
| `docker-compose build`                   | Build or rebuild services.               |
| `docker-compose stop`                    | Stop running containers.                 |
| `docker-compose start`                   | Start stopped services.                  |
| `docker-compose exec <service> bash`     | Open a shell inside a running container. |
| `docker-compose config`                  | Validate and view the Compose file.      |

---

### 8. Debugging & Troubleshooting

| **Command**                              | **Description**                          |
|------------------------------------------|------------------------------------------|
| `docker logs <container_name>`           | View logs for a container.               |
| `docker inspect <container_name>`        | Get detailed information about a container or image. |
| `docker events`                          | Monitor Docker events in real-time.      |
| `docker-compose logs -f`                 | Follow logs from containers in a Compose setup. |
| `docker-compose config`                  | Validate the `docker-compose.yml` file.  |

---

### 9. Exporting and Importing

| **Command**                              | **Description**                          |
|------------------------------------------|------------------------------------------|
| `docker save -o <file_name>.tar <image>` | Export an image to a tar file.           |
| `docker load -i <file_name>.tar`         | Import an image from a tar file.         |
| `docker export <container_id> > <file.tar>` | Export a container's filesystem to a tar file. |
| `docker import <file.tar>`               | Import a container's filesystem from a tar file as an image. |

---

### 10. Monitoring Docker

| **Command**                              | **Description**                          |
|------------------------------------------|------------------------------------------|
| `docker stats`                           | View real-time resource usage statistics for running containers. |
| `docker top <container_name>`            | Display running processes in a container. |





### `docker-compose.yml` Sample : 

```yml
services:

  laravel-docker:
    container_name: docker_test_project_2
    build: .
    volumes:
      - .:/var/www/html
    ports:
      - 8000:8000

  mysql_db:
    image: mysql:latest
    environment:
      MYSQL_ROOT_PASSWORD: irfan95
      MYSQL_DATABASE: docker_test_project_2
    ports:
      - 3307:3306
    volumes:
      - db_data:/var/lib/mysql

  phpmyadmin:
    image: phpmyadmin:latest
    ports:
      - 9003:80
    environment:
      PMA_HOST: mysql_db
      PMA_PORT: 3306

volumes:
  db_data:

```

### `Dockerfile` file Sample : 

```bash
FROM php:8.2-apache
WORKDIR /var/www/html

# Mod Rewrite
RUN a2enmod rewrite

# Linux Library
RUN apt-get update -y && apt-get install -y \
    libicu-dev \
    libmariadb-dev \
    unzip zip \
    zlib1g-dev \
    libpng-dev \
    libjpeg-dev \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev

# Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# PHP Extension
RUN docker-php-ext-install gettext intl pdo_mysql gd

RUN docker-php-ext-configure gd --enable-gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd
```

### `Makefile` Sample : 
```bash
setup:
	@make build
	@make up
	@make composer-update
build:
	docker-compose build --no-cache --force-rm
stop:
	docker-compose stop
up:
	docker-compose up -d
composer-update:
	docker exec docker-php-task bash -c "composer update"
data:
	docker exec docker-php-task bash -c "php artisan migrate"
	docker exec docker-php-task bash -c "php artisan db:seed"
```


## When I start docker for a new project :
- Create folder 
- create files for `docker-compose.yml`, `Dockerfile` and `Makefile`. Then put the data where I already mentioned.
- Run : `docker-compose build` for build or rebuild services.
- Run : `docker-compose up` for creating and start containers.
- To Check Container Run: `docker ps`
- Enter Container : `docker exec -it cartproshop_v3 bash`
- Exit from container when you need : exit
- To Access Database : http://localhost:9003/
- If you face any port related issues
    - Stop existing Apache Serve
    - run : docker exec cartproshop_v3 bash -c "php artisan serve --host=0.0.0.0 --port=8003"


## Reference :
- Initial Setup : https://www.youtube.com/watch?v=_iLwTmaUU-g&t=719s
- Professional Setup (Laravel) : https://www.youtube.com/watch?v=V-MDfE1I6u0