# Docker Compose Complete Guide

# What is Docker Compose?

Docker Compose is a tool used to **define and manage multiple Docker containers** using a single YAML file (`docker-compose.yml`).

Instead of running multiple `docker run` commands, Docker Compose allows you to start the entire application with a single command.

---

# Without Docker Compose

```bash
docker run nginx
docker run mysql
docker run ubuntu
```

Every container requires its own command.

---

# With Docker Compose

```bash
docker compose up -d
```

One command starts the complete project.

---

# Workflow

```text
docker-compose.yml
        │
        ▼
docker compose up -d
        │
        ▼
Creates
• Containers
• Networks
• Volumes
        │
        ▼
Application Running
```

---

# Docker Compose File Location

The compose file should be placed in the project root.

Example

```text
Docker-Monitoring-System
│
├── docker-compose.yml
├── nginx
│   ├── Dockerfile
│   └── index.html
└── README.md
```

---

# Basic Structure

```yaml
services:

  web:
    image: nginx

  db:
    image: mysql
```

---

# What is a Service?

A **Service** represents **one container** and its complete configuration.

Each service tells Docker:

- Which image to use
- What the container name will be
- Which ports to expose
- Which network to join
- Which volume to mount
- Which environment variables to use
- How the container should start

---

# Common Service Options

```yaml
services:

  web:
    image:
    build:
    container_name:
    hostname:
    ports:
    environment:
    env_file:
    volumes:
    networks:
    depends_on:
    restart:
    command:
    entrypoint:
    working_dir:
    user:
    tty:
    stdin_open:
```

---

# Compose Keywords

---

# image

```yaml
image: nginx
```

## Why?

Uses an existing image from Docker Hub.

Equivalent Command

```bash
docker run nginx
```

---

# build

```yaml
build: ./nginx
```

## Why?

Instead of downloading an image, Docker builds a custom image from the Dockerfile inside the specified folder.

Equivalent Command

```bash
docker build -t my-image ./nginx
```

---

# container_name

```yaml
container_name: web
```

## Why?

Assigns a custom name to the container.

Equivalent Command

```bash
docker run --name web
```

---

# ports

```yaml
ports:
  - "8080:80"
```

## Why?

Maps the host port to the container port.

```text
Host
8080
 │
 ▼
Container
80
```

Equivalent Command

```bash
docker run -p 8080:80
```

---

# environment

```yaml
environment:
  MYSQL_ROOT_PASSWORD: root123
```

## Why?

Passes environment variables to the container.

Equivalent Command

```bash
docker run -e MYSQL_ROOT_PASSWORD=root123
```

---

# volumes

```yaml
volumes:
  - mysql-data:/var/lib/mysql
```

## Why?

Stores data permanently.

Without a volume:

Container deleted

↓

Database deleted.

With a volume:

Container deleted

↓

Database remains safe.

Equivalent Command

```bash
docker volume create mysql-data
```

---

# networks

```yaml
networks:
  - devops-net
```

## Why?

Connects the container to a Docker network.

Containers inside the same network can communicate with each other.

Equivalent Command

```bash
docker network create devops-net
```

---

# Is Network Mandatory?

**No.**

Docker Compose automatically creates a default network.

Example

```text
project_default
```

However, creating your own custom network is considered a best practice because it provides:

- Better organization
- Better security
- Better isolation
- Easier management

---

# depends_on

```yaml
depends_on:
  - db
```

## Why?

Starts the database before starting the application.

```text
db
 │
 ▼
web
```

---

# restart

```yaml
restart: always
```

## Why?

Automatically restarts the container if it crashes.

---

# command

```yaml
command: python app.py
```

## Why?

Overrides the default command executed when the container starts.

---

# entrypoint

```yaml
entrypoint: python
```

## Why?

Defines the main executable for the container.

---

# working_dir

```yaml
working_dir: /app
```

## Why?

Sets the current working directory.

Equivalent to:

```bash
cd /app
```

inside the container.

---

# user

```yaml
user: root
```

## Why?

Runs the container using a specific user.

Usually used for permissions and security.

---

# tty

```yaml
tty: true
```

## Why?

Keeps the terminal interactive.

Mostly used for Ubuntu or Linux containers.

---

# stdin_open

```yaml
stdin_open: true
```

## Why?

Keeps standard input open for interactive applications.

Equivalent to:

```bash
docker run -i
```

---

# Complete Project Example

```yaml
services:

  web:
    build: ./nginx
    container_name: web

    ports:
      - "8080:80"

    networks:
      - devops-net

  db:
    image: mysql

    container_name: mysql-db

    environment:
      MYSQL_ROOT_PASSWORD: root123

    volumes:
      - mysql-data:/var/lib/mysql

    networks:
      - devops-net

  client:
    image: ubuntu

    container_name: client

    tty: true

    networks:
      - devops-net

volumes:
  mysql-data:

networks:
  devops-net:
```

---

# Docker Compose Commands

## Start Everything

```bash
docker compose up -d
```

Creates and starts all containers.

---

## Stop Containers

```bash
docker compose stop
```

Stops all running containers.

---

## Start Again

```bash
docker compose start
```

Starts previously stopped containers.

---

## Restart

```bash
docker compose restart
```

Restarts all containers.

---

## Check Status

```bash
docker compose ps
```

Displays running containers.

---

## View Logs

```bash
docker compose logs
```

Shows logs from all services.

---

## View Logs of One Service

```bash
docker compose logs web
```

Shows logs only for the `web` service.

---

## Enter a Running Container

```bash
docker compose exec client bash
```

Equivalent to:

```bash
docker exec -it client bash
```

---

## Rebuild Images

```bash
docker compose build
```

Rebuilds images defined with `build:`.

---

## Build and Start

```bash
docker compose up -d --build
```

Rebuilds images and starts containers.

---

## Stop and Remove Everything

```bash
docker compose down
```

Removes:

- Containers
- Networks

---

## Remove Everything Including Volumes

```bash
docker compose down -v
```

Removes:

- Containers
- Networks
- Volumes

⚠️ Warning: Database data stored in volumes will also be deleted.

---

# Interview Questions

## What is Docker Compose?

Docker Compose is a tool that allows you to define and manage multiple Docker containers using a single YAML configuration file.

---

## Why use Docker Compose?

- Manage multiple containers easily.
- Start the entire application with one command.
- Keep configuration in one file.
- Easy deployment and collaboration.
- Ideal for development and testing.

---

# Most Important Docker Compose Keywords

- services
- image
- build
- container_name
- ports
- environment
- volumes
- networks
- depends_on
- restart
- command
- working_dir
- tty

These are the most commonly used options in real-world Docker Compose projects.
