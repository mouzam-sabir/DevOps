# Docker Complete Notes

## What is Docker?

Docker is a **Containerization Platform** that packages an application along with all its dependencies into a **Container**, allowing it to run consistently on any system.

### Simple Definition

> Docker is a tool used to package, deploy, and run applications inside lightweight containers.

---

# Why Do We Use Docker?

- Easy application deployment
- Eliminates "It works on my machine" problems
- Fast deployment
- Lightweight
- Same environment everywhere
- Used in DevOps and CI/CD automation

---

# Where is Docker Used?

- DevOps
- Cloud (AWS, Azure, GCP)
- CI/CD Pipelines
- Microservices
- Web Applications
- Software Testing

---

# Docker Workflow

```text
Developer
    │
    ▼
Write Dockerfile
    │
    ▼
Build Image
(docker build)
    │
    ▼
Docker Image
    │
docker run
    ▼
Docker Container
    │
Application Running
```

---

# Docker Architecture

```text
Docker Client
      │
      ▼
Docker Engine (Daemon)
      │
      ▼
Docker Image
      │
docker run
      ▼
Docker Container
      │
Application Running
```

---

# Docker Components

## 1. Docker Engine

### What is it?

The main Docker software that manages everything.

### Purpose

- Creates Images
- Creates Containers
- Starts/Stops Containers

---

## 2. Docker Client

### What is it?

The command-line interface where users execute Docker commands.

### Example

```bash
docker run ubuntu
```

The client sends this command to the Docker Engine.

---

## 3. Docker Daemon (dockerd)

### What is it?

A background service responsible for Docker operations.

### Responsibilities

- Manage Images
- Manage Containers
- Manage Networks
- Manage Volumes

---

## 4. Docker Image

### What is it?

A **read-only template** used to create containers.

### Examples

- Ubuntu Image
- Nginx Image
- MySQL Image

### Command

```bash
docker pull ubuntu
```

---

## 5. Docker Container

### What is it?

A **running instance of a Docker Image**.

### Example

```
Ubuntu Image
      │
      ▼
Ubuntu Container
```

### Command

```bash
docker run -it ubuntu
```

---

## 6. Dockerfile

### What is it?

A text file containing instructions for building a Docker Image.

### Example

```dockerfile
FROM ubuntu

RUN apt update

CMD ["bash"]
```

### Build Image

```bash
docker build -t myimage .
```

---

## 7. Docker Hub

### What is it?

Docker's online repository where images are stored.

### Examples

- Ubuntu
- Nginx
- Redis
- MySQL
- Python

### Command

```bash
docker pull nginx
```

---

## 8. Docker Volume

### What is it?

Permanent storage for Docker containers.

Even if the container is deleted, the data remains safe.

### Example

```
MySQL Database Data
```

### Command

```bash
docker volume ls
```

---

## 9. Docker Network

### What is it?

Allows multiple containers to communicate with each other.

### Example

```
Web Container
      │
      ▼
Database Container
```

### Command

```bash
docker network ls
```

---

## 10. Docker Compose

### What is it?

A tool used to run multiple containers from a single configuration file.

### Example

```
Web

Database

Redis
```

### Command

```bash
docker compose up
```

---

# Docker Image vs Docker Container

| Docker Image | Docker Container |
|--------------|------------------|
| Template | Running Instance |
| Read Only | Writable |
| Cannot Execute | Can Execute |
| Created using Dockerfile | Created from Image |

### Example

```
Ubuntu Image

├── Container 1
├── Container 2
└── Container 3
```

One Image can create multiple Containers.

---

# Real World Example

## Without Docker

```
Developer

↓

Code

↓

Server

↓

Python Missing ❌

Library Missing ❌

Application Crash ❌
```

---

## With Docker

```
Developer

↓

Docker Image

↓

Server

↓

docker run

↓

Application Works ✅
```

---

# Advantages of Docker

- Lightweight
- Fast Startup
- Portable
- Consistent Environment
- Easy Deployment
- Easy Scaling
- DevOps Friendly
- CI/CD Support

---

# Disadvantages of Docker

- Not a complete Operating System
- Windows applications cannot run directly
- Requires proper security configuration
- Less suitable for GUI applications

---

# Docker vs Virtual Machine

| Docker | Virtual Machine |
|---------|-----------------|
| Uses Containers | Uses Virtual Machines |
| Shares Host OS | Each VM has its own OS |
| Lightweight | Heavy |
| Fast Startup | Slow Startup |
| Low RAM Usage | High RAM Usage |
| Best for Deployment | Best for Multiple Operating Systems |

---

# Interview Definition

**Docker is a containerization platform used to package, deploy, and run applications inside lightweight containers with all required dependencies.**

---

# Complete Docker Flow

```text
Developer
     │
Write Dockerfile
     │
docker build
     ▼
Docker Image
     │
docker push (Optional)
     ▼
Docker Hub
     │
docker pull
     ▼
Docker Image
     │
docker run
     ▼
Docker Container
     │
Application Running
     │
Logs
     │
Volumes
     │
Networks
---

# Quick Revision

- Docker → Containerization Platform
- Docker Image → Template
- Docker Container → Running Image
- Dockerfile → Instructions to build Image
- Docker Hub → Online Image Repository
- Docker Volume → Permanent Storage
- Docker Network → Container Communication
- Docker Compose → Run Multiple Containers
- Docker Engine → Core Docker Service
- Docker Client → Command Line Interface
- Docker Daemon → Background Service
