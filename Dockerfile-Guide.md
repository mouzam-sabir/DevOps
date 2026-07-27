# Dockerfile Complete Guide

## What is Dockerfile?

A **Dockerfile** is a text file that contains a set of instructions used to build a custom Docker image.

### Workflow

```text
Dockerfile
     │
docker build
     │
     ▼
Docker Image
     │
docker run
     ▼
Docker Container
```

---

# 1. FROM

```dockerfile
FROM ubuntu:22.04
```

## Why?

Docker must know **which base image** to start from.

Without a base image, Docker doesn't know what operating system or software to use.

### When to use?

| Requirement | Base Image |
|-------------|------------|
| Linux Environment | Ubuntu |
| Web Server | Nginx |
| Python Application | Python |
| Database | MySQL |
| Java Application | OpenJDK |

### Example

```dockerfile
FROM nginx:latest
```

Why Nginx?

- Nginx is already installed.
- Port 80 is already configured.
- Ready to host websites.

### If NOT used?

❌ Docker cannot build the image because every Dockerfile must start with a base image.

---

# 2. LABEL

```dockerfile
LABEL maintainer="Mouzam Sabir"
```

## Why?

Adds metadata about the image.

Example:

- Owner
- Company
- Version
- Description

### If NOT used?

The image still works.

Only metadata is missing.

---

# 3. ENV

```dockerfile
ENV APP_NAME="Docker Monitoring"
```

## Why?

Stores environment variables.

Instead of hardcoding values everywhere.

Examples:

- Database Password
- API Keys
- Port Number
- Environment (Dev / Production)

### If NOT used?

Values must be hardcoded inside the application.

---

# 4. WORKDIR

```dockerfile
WORKDIR /app
```

## Why?

Sets the default working directory.

Instead of writing:

```dockerfile
COPY app.py /app
RUN cd /app
RUN python app.py
```

Simply use:

```dockerfile
WORKDIR /app

COPY . .

RUN python app.py
```

### If NOT used?

You must write full paths in almost every command.

---

# 5. COPY

```dockerfile
COPY index.html /usr/share/nginx/html/
```

## Why?

Copies files from your computer into the Docker image.

Example

```
Local File
index.html

        │
     COPY
        ▼

Docker Image
/usr/share/nginx/html/index.html
```

### If NOT used?

Your project files will not exist inside the container.

---

# 6. ADD

```dockerfile
ADD project.zip /app/
```

## Why?

Similar to COPY but provides extra features.

It can:

- Extract local ZIP/TAR files automatically.
- Download files from URLs.

### Best Practice

Use **COPY** unless you specifically need ADD.

---

# 7. RUN

```dockerfile
RUN apt update
```

## Why?

Runs commands **while building the image**.

Examples

```dockerfile
RUN apt install -y curl
```

```dockerfile
RUN mkdir logs
```

### When to use?

- Install packages
- Create folders
- Change permissions
- Update packages

### If NOT used?

Required software won't be installed inside the image.

---

# 8. EXPOSE

```dockerfile
EXPOSE 80
```

## Why?

Documents which port the application uses.

Example

Nginx → Port 80

Flask → Port 5000

Node.js → Port 3000

### If NOT used?

The application may still work.

It simply won't document which port should be exposed.

---

# 9. CMD

```dockerfile
CMD ["nginx","-g","daemon off;"]
```

## Why?

Defines the default command that runs when the container starts.

### If NOT used?

The container may start and immediately stop because no main process is running.

---

# 10. ENTRYPOINT

```dockerfile
ENTRYPOINT ["python"]
```

## Why?

Defines the main executable that always runs.

### Difference

CMD

- Default command
- Easy to override

ENTRYPOINT

- Main executable
- Runs every time unless explicitly overridden

---

# 11. USER

```dockerfile
USER nginx
```

## Why?

Specifies which user runs the container.

### Why important?

Security.

Production containers should avoid running as **root** whenever possible.

### If NOT used?

Docker uses the default user (usually `root`).

---

# 12. VOLUME

```dockerfile
VOLUME /var/lib/mysql
```

## Why?

Stores data permanently.

Example

```
Container
     │
     ▼
Docker Volume
```

Even if the container is deleted, the data remains.

### If NOT used?

Deleting the container also deletes its data.

---

# 13. ARG

```dockerfile
ARG VERSION=1.0
```

## Why?

Creates build-time variables.

Example

```bash
docker build --build-arg VERSION=2.0 .
```

### Difference

ARG

- Available only during image build

ENV

- Available during build and runtime

---

# 14. HEALTHCHECK

```dockerfile
HEALTHCHECK CMD curl --fail http://localhost || exit 1
```

## Why?

Checks whether the application inside the container is healthy.

Docker continuously monitors the container.

---

# 15. SHELL

```dockerfile
SHELL ["/bin/bash","-c"]
```

## Why?

Changes the default shell.

Default:

```
/bin/sh
```

Custom:

```
/bin/bash
```

---

# 16. STOPSIGNAL

```dockerfile
STOPSIGNAL SIGTERM
```

## Why?

Specifies which signal Docker sends when stopping the container.

Useful for graceful shutdown.

---

# 17. ONBUILD

```dockerfile
ONBUILD COPY . /app
```

## Why?

Runs automatically when another Dockerfile uses this image as its base.

Mostly used for creating reusable base images.

---

# Real Project Example

```dockerfile
FROM nginx:latest

LABEL maintainer="Mouzam Sabir"

WORKDIR /usr/share/nginx/html

COPY index.html .

EXPOSE 80

CMD ["nginx","-g","daemon off;"]
```

---

# Why Each Command Was Used

## FROM nginx:latest

We need a web server.

Nginx already has:

- Nginx installed
- Port 80 configured
- Ready to serve web pages

No manual installation required.

---

## LABEL

Stores information about the image creator.

---

## WORKDIR

Sets the folder where the website files will be managed.

---

## COPY

Copies our custom website (`index.html`) into the Nginx web directory.

Without this, the default **Welcome to Nginx** page would appear.

---

## EXPOSE 80

Documents that Nginx serves traffic on port 80.

---

## CMD

Starts the Nginx server automatically when the container starts.

Without CMD, the container would exit immediately because no foreground process would be running.

---

# Dockerfile Writing Formula

Whenever you write a Dockerfile, ask yourself these questions:

1. Which base image do I need?
   → `FROM`

2. Who created this image?
   → `LABEL`

3. Do I need environment variables?
   → `ENV`

4. Which folder should Docker work in?
   → `WORKDIR`

5. Which files should be copied?
   → `COPY`

6. Do I need to install anything?
   → `RUN`

7. Do I need persistent storage?
   → `VOLUME`

8. Which port does my application use?
   → `EXPOSE`

9. What should run when the container starts?
   → `CMD` or `ENTRYPOINT`

---

# Most Frequently Used Dockerfile Commands

These are the commands you'll use in **95% of Dockerfiles**:

- FROM
- WORKDIR
- COPY
- RUN
- ENV
- EXPOSE
- CMD

The remaining commands are added only when the project specifically requires them.
