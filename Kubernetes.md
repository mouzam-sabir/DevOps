# Kubernetes - Beginner Friendly Notes

---

# Part 1 – Kubernetes Fundamentals

---

# What is Kubernetes?

Kubernetes (also called **K8s**) is an **open-source container orchestration platform** used to deploy, manage, scale, and monitor containerized applications automatically.

It was originally developed by **Google** and is now maintained by the **Cloud Native Computing Foundation (CNCF).**

In simple words:

- Docker creates containers.
- Kubernetes manages those containers.

Think of Kubernetes as a manager that controls hundreds or even thousands of Docker containers.

---

# Why Kubernetes?

Suppose you have only one Docker container.

Everything works perfectly.

Now imagine your application grows.

You have:

- 100 Docker containers
- 20 servers
- Thousands of users

Managing them manually becomes almost impossible.

Questions like these start appearing:

- Which server should run the container?
- What if a server crashes?
- What if traffic suddenly increases?
- How do I update my application without downtime?

Kubernetes solves all these problems automatically.

It can:

- Deploy applications
- Restart failed containers
- Scale applications automatically
- Balance traffic
- Update applications without downtime
- Keep applications highly available

---

# Why Not Docker Alone?

Docker is excellent for creating and running containers.

However, Docker does not manage large-scale infrastructure efficiently.

Imagine this situation.

Without Kubernetes:

```text
Server 1

├── Container A
├── Container B
└── Container C

↓

Server crashes

↓

Application becomes unavailable.
```

Now with Kubernetes:

```text
Server 1

├── Container A
├── Container B

↓

Server crashes

↓

Kubernetes detects failure

↓

Containers start automatically on another server.
```

The users continue using the application without noticing the failure.

---

# Docker vs Kubernetes

| Docker | Kubernetes |
|---------|------------|
| Creates containers | Manages containers |
| Runs containers | Manages applications running in containers |
| Works mainly on a single machine | Works across multiple machines |
| Manual scaling | Automatic scaling |
| Manual recovery | Automatic recovery |
| Container engine | Container orchestration platform |

Think of it like this:

```
Docker

↓

Creates Container

-------------------------

Kubernetes

↓

Manages Containers
```

---

# What is Container Orchestration?

Container orchestration means **automatically managing containers**.

Instead of manually performing tasks like:

- Starting containers
- Stopping containers
- Restarting containers
- Scaling containers
- Monitoring containers

Kubernetes performs all these tasks automatically.

---

# Real World Example

Imagine you own an online shopping website.

During normal days:

```
3 Containers
```

During a big sale:

```
100 Containers Required
```

Without Kubernetes:

You would need to create every container manually.

With Kubernetes:

Traffic increases.

↓

Kubernetes automatically creates more Pods.

↓

Traffic decreases.

↓

Kubernetes removes unnecessary Pods.

Everything happens automatically.

---

# High-Level Kubernetes Workflow

Before learning Kubernetes components, understand the overall workflow.

```text
Developer

↓

Writes Application

↓

Builds Docker Image

↓

Pushes Image to Docker Registry

↓

Kubernetes Deploys the Application

↓

Users Access the Application
```

Later, we'll understand every step in detail.

---

# Why Companies Use Kubernetes?

Most companies use Kubernetes because it provides:

- High Availability
- Automatic Scaling
- Self-Healing
- Load Balancing
- Rolling Updates
- Rollbacks
- Easy Cloud Deployment
- Better Resource Utilization

Examples:

- Google
- Netflix
- Spotify
- Airbnb
- Shopify
- Adobe

---

# Summary

Kubernetes is an open-source platform used to automatically deploy, manage, monitor, and scale containerized applications. It works with Docker containers and makes applications highly available by providing automation, self-healing, scaling, and load balancing.

---

# Part 2 – Kubernetes Architecture

---

# What is a Kubernetes Cluster?

A **Cluster** is a collection of machines working together to run applications.

A Kubernetes Cluster contains:

- One Control Plane (Master Node)
- One or more Worker Nodes

Example:

```text
Kubernetes Cluster

├── Control Plane
├── Worker Node 1
├── Worker Node 2
└── Worker Node 3
```

The cluster is the complete Kubernetes environment.

---

# Kubernetes Architecture

The architecture looks like this:

```text
                Kubernetes Cluster

        +---------------------------+
        |      Control Plane        |
        +---------------------------+
                   |
                   |
----------------------------------------------------
|                  |                  |
▼                  ▼                  ▼

+------------+   +------------+   +------------+
| Worker 1   |   | Worker 2   |   | Worker 3   |
+------------+   +------------+   +------------+

      |                |                 |

     Pods             Pods              Pods

      |                |                 |

 Containers       Containers       Containers
```

---

# Control Plane (Master Node)

The Control Plane is the **brain** of Kubernetes.

It controls the entire cluster.

It makes decisions such as:

- Which Worker Node should run a Pod?
- Is any Pod unhealthy?
- Should new Pods be created?
- Should traffic be balanced?
- Is the cluster healthy?

The Control Plane does **not** run application containers.

It only manages them.

The Control Plane contains:

- API Server
- Scheduler
- Controller Manager
- ETCD

---

# Worker Node

Worker Nodes are the machines where your applications actually run.

Every Worker Node contains:

- Kubelet
- Container Runtime
- Kube Proxy
- Pods

Example:

```text
Worker Node

├── Kubelet
├── Container Runtime
├── Kube Proxy
└── Pods
```

---

# API Server

The API Server is the **main entry point** of Kubernetes.

Every request first goes to the API Server.

Example:

```text
kubectl apply

↓

API Server

↓

Processes Request
```

Responsibilities:

- Accepts API requests
- Authenticates users
- Authorizes requests
- Communicates with other Kubernetes components

Without the API Server, Kubernetes cannot function.

---

# Scheduler

The Scheduler decides **where a Pod should run**.

Suppose a new Pod is created.

The Scheduler checks:

- CPU availability
- Memory availability
- Node health
- Available resources

Then it selects the best Worker Node.

Example:

```text
Pod Created

↓

Scheduler

↓

Worker Node 2 Selected

↓

Pod Starts
```

---

# Controller Manager

The Controller Manager continuously checks whether the cluster is in the desired state.

Example:

Desired State:

```text
3 Pods
```

Current State:

```text
2 Pods
```

Controller Manager notices the difference.

↓

Creates one more Pod.

This process is called **Self-Healing**.

---

# ETCD

ETCD is the Kubernetes database.

It stores all cluster information.

Examples:

- Nodes
- Pods
- Services
- Deployments
- Secrets
- ConfigMaps
- Namespaces

Everything is stored as **Key-Value pairs**.

Example:

```text
Node Status

↓

ETCD

↓

Saved
```

If ETCD is lost, Kubernetes loses the cluster configuration.

---

# Kubelet

Kubelet is an agent running on every Worker Node.

Responsibilities:

- Receives instructions from API Server
- Starts Pods
- Stops Pods
- Monitors Pod health
- Reports status back to the Control Plane

Workflow:

```text
API Server

↓

Kubelet

↓

Starts Pod
```

---

# Container Runtime

Container Runtime actually runs containers.

Examples:

- containerd
- CRI-O
- Docker (older Kubernetes versions)

Responsibilities:

- Pull Images
- Create Containers
- Start Containers
- Stop Containers

Workflow:

```text
Docker Image

↓

Container Runtime

↓

Running Container
```

---

# Kube Proxy

Kube Proxy manages networking inside the Kubernetes Cluster.

Responsibilities:

- Pod-to-Pod communication
- Service networking
- Internal load balancing

Example:

```text
User

↓

Service

↓

Kube Proxy

↓

Pod 1

or

↓

Pod 2

or

↓

Pod 3
```

---

# Complete Kubernetes Architecture Workflow

Whenever a developer deploys an application, Kubernetes follows this flow:

```text
Developer

↓

kubectl apply

↓

API Server

↓

Scheduler

↓

Worker Node Selected

↓

Kubelet

↓

Container Runtime

↓

Pod Starts Running
```

Later we'll learn how Deployments, ReplicaSets, and Services are involved.

---

# Architecture Summary

| Component | Responsibility |
|------------|----------------|
| Cluster | Complete Kubernetes environment |
| Control Plane | Manages the cluster |
| Worker Node | Runs applications |
| API Server | Entry point of Kubernetes |
| Scheduler | Selects the best Worker Node |
| Controller Manager | Maintains desired state |
| ETCD | Stores cluster information |
| Kubelet | Runs Pods on Worker Nodes |
| Container Runtime | Runs containers |
| Kube Proxy | Handles networking |

---

# Interview Questions

## Q1. What is a Kubernetes Cluster?

A Kubernetes Cluster is a collection of one Control Plane and one or more Worker Nodes that work together to run containerized applications.

---

## Q2. What is the Control Plane?

The Control Plane is the brain of Kubernetes that manages the cluster and controls scheduling, monitoring, scaling, and health of applications.

---

## Q3. What is a Worker Node?

A Worker Node is the machine where Pods and application containers actually run.

---

## Q4. What is the role of the API Server?

The API Server is the main entry point of Kubernetes. Every request passes through it before being processed.

---

## Q5. What does the Scheduler do?

The Scheduler decides which Worker Node should run a newly created Pod based on available resources.

---

## Q6. What is ETCD?

ETCD is Kubernetes' distributed key-value database that stores all cluster configuration and state information.

---
# Part 3 – Kubernetes Workloads

---

# What is a Container?

Before understanding Pods, let's first understand containers.

A **Container** is a lightweight package that contains everything an application needs to run.

It includes:

- Application Code
- Libraries
- Dependencies
- Runtime
- Configuration

Example:

```
Container

├── Application
├── Python
├── Required Libraries
└── Configuration
```

A container can run on any machine that has a container runtime.

---

# Why Kubernetes Doesn't Manage Containers Directly?

Although containers run applications, Kubernetes **never manages containers directly**.

Instead, Kubernetes manages **Pods**.

Think like this:

```
Container

↓

Pod

↓

Kubernetes
```

A Pod acts as a wrapper around one or more containers.

---

# What is a Pod?

A **Pod** is the **smallest deployable unit** in Kubernetes.

Every application running inside Kubernetes runs inside a Pod.

Example:

```
Pod

┌─────────────────────┐
│     Container       │
└─────────────────────┘
```

---

# Why Pod?

Kubernetes needs a standard object to manage applications.

Instead of managing individual containers, it manages Pods.

A Pod provides:

- Shared Network
- Shared Storage
- Shared Lifecycle

---

# Single Container Pod

Most applications use one container per Pod.

Example:

```
Pod

└── Nginx Container
```

---

# Multi-Container Pod

Sometimes one Pod contains multiple containers.

Example:

```
Pod

├── Application Container
└── Logging Container
```

Both containers:

- Share the same IP
- Share storage
- Communicate using localhost

---

# Pod Lifecycle

Every Pod goes through different states.

```
Pending

↓

Running

↓

Succeeded

OR

Failed
```

### Pending

Pod has been created but hasn't started yet.

### Running

Container is successfully running.

### Succeeded

Application completed successfully.

### Failed

Application exited with an error.

---

# Labels

Labels are **key-value pairs** attached to Kubernetes objects.

Example:

```yaml
labels:
  app: nginx
  env: production
```

Here:

```
app = nginx

env = production
```

---

# Why Labels?

Suppose you have 100 Pods.

How does Kubernetes know which Pods belong to which application?

Labels solve this problem.

Example:

```
Pod 1

app=frontend

-----------------

Pod 2

app=frontend

-----------------

Pod 3

app=database
```

---

# Selectors

Selectors use Labels to select Pods.

Example:

```
Selector

app=frontend

↓

Pod 1

Pod 2
```

Pod 3 is ignored because its label is different.

---

# ReplicaSet

A ReplicaSet ensures that the desired number of Pods are always running.

Example:

Desired State:

```
3 Pods
```

Current State:

```
2 Pods
```

ReplicaSet automatically creates one more Pod.

```
ReplicaSet

↓

Checks Pods

↓

Missing Pod

↓

Creates New Pod
```

---

# Why ReplicaSet?

Without ReplicaSet

```
Pod crashes

↓

Application stops
```

With ReplicaSet

```
Pod crashes

↓

ReplicaSet detects failure

↓

Creates New Pod

↓

Application keeps running
```

This feature is called **Self-Healing**.

---

# Deployment

A Deployment is the Kubernetes object used in real-world projects.

Instead of creating Pods manually, developers create a Deployment.

Deployment automatically manages:

- ReplicaSets
- Pods

Architecture:

```
Deployment

↓

ReplicaSet

↓

Pods

↓

Containers
```

---

# Why Deployment?

Suppose your application currently runs Version 1.

Now you release Version 2.

Deployment updates the application automatically without downtime.

---

# Rolling Update

Rolling Update updates Pods one by one.

Current Version:

```
Pod 1 → v1

Pod 2 → v1

Pod 3 → v1
```

Update Begins

```
Pod 1 → v2

Pod 2 → v1

Pod 3 → v1
```

↓

```
Pod 1 → v2

Pod 2 → v2

Pod 3 → v1
```

↓

```
Pod 1 → v2

Pod 2 → v2

Pod 3 → v2
```

Users continue using the application without downtime.

---

# Rollback

Suppose Version 2 contains a bug.

Deployment can immediately restore Version 1.

```
Version 1

↓

Update

↓

Version 2

↓

Bug Found

↓

Rollback

↓

Version 1
```

---

# Scaling

Scaling means increasing or decreasing the number of Pods.

Example:

Current

```
3 Pods
```

Traffic increases

↓

```
10 Pods
```

Traffic decreases

↓

```
3 Pods
```

---

# Manual Scaling

Example:

```bash
kubectl scale deployment nginx --replicas=5
```

Result:

```
3 Pods

↓

5 Pods
```

---

# Self-Healing

Suppose one Pod crashes.

```
Deployment

↓

ReplicaSet

↓

Missing Pod

↓

Creates New Pod
```

Application continues running.

---

# Complete Workload Flow

```
Container

↓

Pod

↓

Labels

↓

Selectors

↓

ReplicaSet

↓

Deployment

↓

Application Running
```

---

# Part 4 – Kubernetes Networking

---

# Why Do We Need Services?

Pods are temporary.

If a Pod crashes, Kubernetes creates a new Pod with a different IP address.

Without a Service:

```
Pod

↓

IP = 10.1.0.5

↓

Pod crashes

↓

New Pod

↓

IP = 10.1.0.8
```

Applications would lose communication.

A Service provides one stable endpoint.

---

# What is a Service?

A **Service** is a Kubernetes object that provides a permanent IP address and DNS name for Pods.

```
Users

↓

Service

↓

Pods
```

Even if Pods change, the Service remains the same.

---

# Service Types

## 1. ClusterIP (Default)

Used only inside the Kubernetes cluster.

Example:

```
Frontend

↓

ClusterIP

↓

Backend Pods
```

Users outside the cluster cannot access it.

---

## 2. NodePort

Exposes an application outside the cluster using a Worker Node's IP and a specific port.

Example:

```
http://NodeIP:30080
```

Flow:

```
User

↓

NodePort

↓

Pods
```

---

## 3. LoadBalancer

Used mainly in cloud environments.

Cloud providers automatically create an external Load Balancer.

Flow:

```
Internet

↓

Load Balancer

↓

Pods
```

---

# Ingress

Ingress acts as a smart router.

Instead of exposing many ports, it routes requests based on domain names or URLs.

Example:

```
shop.example.com

↓

Shopping App

-------------------

blog.example.com

↓

Blog App
```

One IP can serve multiple applications.

---

# Role of Kube Proxy

Kube Proxy handles networking on every Worker Node.

Responsibilities:

- Pod-to-Pod communication
- Service networking
- Internal load balancing

Flow:

```
User

↓

Service

↓

Kube Proxy

↓

Pod 1

or

↓

Pod 2

or

↓

Pod 3
```

---

# Complete Networking Flow

```
Users

↓

Ingress

↓

Service

↓

Kube Proxy

↓

Pods

↓

Containers
```

---

# Networking Summary

| Component | Purpose |
|------------|---------|
| Service | Provides a stable IP and DNS for Pods |
| ClusterIP | Internal communication |
| NodePort | External access using Node IP |
| LoadBalancer | External access using cloud load balancer |
| Ingress | Routes HTTP/HTTPS traffic |
| Kube Proxy | Handles networking and load balancing |

---

# Interview Questions

## Q1. Why do we need a Service?

Because Pods are temporary and their IP addresses change. A Service provides a stable IP and DNS name.

---

## Q2. What is ClusterIP?

ClusterIP is the default Service type used for communication inside the Kubernetes cluster.

---

## Q3. What is NodePort?

NodePort exposes an application outside the cluster using a Worker Node's IP address and a port.

---

## Q4. What is LoadBalancer?

LoadBalancer exposes an application to the internet using a cloud provider's load balancer.

---

## Q5. What is Ingress?

Ingress routes external HTTP/HTTPS traffic to different Services using domain names or URL paths.

---
# Part 5 – Configuration & Storage

---

# Why Do We Need Configuration?

Applications require configuration to run properly.

Examples:

- Database Host
- Port Number
- Environment
- API URL
- Username
- Password

Instead of hardcoding these values inside the application, Kubernetes provides ConfigMaps and Secrets.

---

# Namespace

A **Namespace** is a logical partition inside a Kubernetes Cluster.

It allows multiple teams or applications to share the same cluster without interfering with each other.

Example:

```text
Kubernetes Cluster

├── Default Namespace
├── Development Namespace
├── Testing Namespace
└── Production Namespace
```

Each Namespace has its own resources like:

- Pods
- Deployments
- Services
- ConfigMaps
- Secrets

---

# Why Namespace?

Suppose two teams deploy an application named **nginx**.

Without Namespaces:

```
nginx

↓

Name Conflict
```

With Namespaces:

```
Development

↓

nginx

-----------------

Production

↓

nginx
```

Both applications can exist without conflicts.

---

# ConfigMap

A **ConfigMap** stores **non-sensitive configuration**.

Examples:

- Database Host
- Application Port
- Environment Variables
- API URL

Example:

```text
DATABASE_HOST=db.example.com

PORT=8080

APP_ENV=production
```

Instead of writing these values inside the application, Kubernetes provides them using a ConfigMap.

---

# Why ConfigMap?

Without ConfigMap

```
Application

↓

Database Host Hardcoded

↓

Need to rebuild application if host changes.
```

With ConfigMap

```
Application

↓

Reads ConfigMap

↓

Configuration changes without rebuilding application.
```

---

# Secret

A **Secret** stores sensitive information securely.

Examples:

- Passwords
- API Keys
- Tokens
- Certificates
- Database Credentials

Example:

```text
Database Password

API Token

JWT Secret
```

Secrets should never be hardcoded into the application.

---

# ConfigMap vs Secret

| ConfigMap | Secret |
|------------|---------|
| Non-sensitive data | Sensitive data |
| Plain configuration | Passwords, Tokens, API Keys |
| Readable | Stored securely (Base64 encoded by default) |

---

# Volume

Containers are temporary.

If a container is deleted, all data stored inside it is also deleted.

Volumes provide storage that survives container restarts.

```
Container

↓

Volume

↓

Data Stored
```

---

# Why Volume?

Without Volume

```
Container

↓

Stores Files

↓

Container Deleted

↓

Files Lost
```

With Volume

```
Container

↓

Volume

↓

Files Remain Safe
```

---

# Persistent Volume (PV)

A **Persistent Volume (PV)** is the actual storage available in the Kubernetes Cluster.

Examples:

- SSD
- HDD
- NFS
- AWS EBS
- Azure Disk
- Google Persistent Disk

Think of a PV as physical storage.

---

# Persistent Volume Claim (PVC)

Applications do not use a PV directly.

Instead, they request storage through a **Persistent Volume Claim (PVC).**

Flow:

```text
Application

↓

PVC

↓

PV

↓

Physical Disk
```

---

# Why PVC?

Applications don't need to know where storage exists.

They simply request:

```
10 GB Storage
```

Kubernetes automatically provides an available PV.

---

# StorageClass

A **StorageClass** automatically creates storage whenever a PVC requests it.

Without StorageClass

```text
Admin

↓

Creates PV Manually

↓

Application Uses It
```

With StorageClass

```text
Application

↓

PVC

↓

StorageClass

↓

PV Created Automatically

↓

Application Uses Storage
```

---

# Complete Storage Workflow

```text
Application

↓

ConfigMap

↓

Secret

↓

PVC

↓

StorageClass

↓

PV

↓

Physical Disk
```

---

# Real DevOps Example

Suppose you deploy MySQL inside Kubernetes.

MySQL stores data in a Persistent Volume.

```
MySQL Pod

↓

PVC

↓

Persistent Volume

↓

SSD Storage
```

If the Pod crashes:

```
Old Pod Deleted

↓

New Pod Created

↓

Same Persistent Volume Attached

↓

Database Remains Safe
```

---

# Storage Summary

| Component | Purpose |
|------------|---------|
| Namespace | Separates cluster resources |
| ConfigMap | Stores configuration |
| Secret | Stores sensitive data |
| Volume | Temporary storage |
| Persistent Volume | Actual storage |
| PVC | Requests storage |
| StorageClass | Automatically provisions storage |

---

# Interview Questions

## Q1. What is a Namespace?

A Namespace is a logical partition inside a Kubernetes Cluster used to organize and isolate resources.

---

## Q2. What is ConfigMap?

ConfigMap stores non-sensitive configuration such as environment variables, URLs, and application settings.

---

## Q3. What is Secret?

Secret stores sensitive information such as passwords, API keys, and tokens securely.

---

## Q4. What is the difference between PV and PVC?

- Persistent Volume (PV) is the actual storage resource.
- Persistent Volume Claim (PVC) is a request made by an application to use storage.

---

## Q5. What is StorageClass?

StorageClass automatically provisions Persistent Volumes when a PVC requests storage.

---

# Part 6 – Complete Kubernetes Workflow

---

# End-to-End Kubernetes Workflow

Now let's connect everything we've learned.

Imagine a developer wants to deploy a web application.

The complete process looks like this:

```text
Developer

↓

Writes Application Code

↓

Builds Docker Image

↓

Pushes Image to Docker Registry

↓

kubectl apply

↓

API Server

↓

ETCD stores configuration

↓

Scheduler selects Worker Node

↓

Kubelet receives instructions

↓

Container Runtime pulls Docker Image

↓

Pod Created

↓

ReplicaSet checks desired Pods

↓

Deployment manages ReplicaSet

↓

Service exposes Pods

↓

Ingress routes external requests

↓

Users Access Application
```

---

# What Happens If a Pod Crashes?

```
Pod Crashes

↓

ReplicaSet Detects Failure

↓

Creates New Pod

↓

Deployment Maintains Desired State

↓

Users Continue Accessing Application
```

This feature is called **Self-Healing**.

---

# What Happens During High Traffic?

Current Pods

```
3 Pods
```

Traffic increases

↓

Deployment scales

↓

```
10 Pods
```

Traffic decreases

↓

Deployment scales down

↓

```
3 Pods
```

This is called **Scaling**.

---

# What Happens During an Application Update?

Current Version

```
Version 1
```

Developer deploys Version 2

↓

Deployment performs Rolling Update

↓

Old Pods are replaced one by one

↓

No Downtime

If Version 2 has a bug

↓

Rollback

↓

Version 1 Restored

---

# Complete Kubernetes Component Relationship

```text
Kubernetes Cluster

│

├── Control Plane

│     ├── API Server
│     ├── Scheduler
│     ├── Controller Manager
│     └── ETCD

│

└── Worker Node

      ├── Kubelet
      ├── Container Runtime
      ├── Kube Proxy
      └── Pods

            └── Containers
```

---

# Kubernetes Learning Roadmap

```text
Docker

↓

Container

↓

Kubernetes

↓

Cluster

↓

Control Plane

↓

Worker Node

↓

Pod

↓

Labels

↓

Selectors

↓

ReplicaSet

↓

Deployment

↓

Service

↓

Ingress

↓

Namespace

↓

ConfigMap

↓

Secret

↓

Volume

↓

Persistent Volume

↓

Persistent Volume Claim

↓

StorageClass
```

---

# Final Summary

Kubernetes is an open-source container orchestration platform that automates the deployment, management, scaling, networking, monitoring, and recovery of containerized applications.

It provides:

- High Availability
- Self-Healing
- Automatic Scaling
- Rolling Updates
- Rollbacks
- Load Balancing
- Persistent Storage
- Configuration Management
- Secure Secret Management

These features make Kubernetes the industry-standard platform for running modern cloud-native applications.

---

# Kubernetes Interview Questions (Final Revision)

## Q1. What is Kubernetes?

Kubernetes is an open-source container orchestration platform used to deploy, manage, scale, and monitor containerized applications automatically.

---

## Q2. What is a Pod?

A Pod is the smallest deployable unit in Kubernetes that contains one or more containers sharing the same network and storage.

---

## Q3. What is ReplicaSet?

ReplicaSet ensures the desired number of Pods are always running and automatically recreates Pods if they fail.

---

## Q4. What is Deployment?

Deployment manages ReplicaSets and provides rolling updates, rollbacks, scaling, and self-healing.

---

## Q5. Why do we use Services?

Services provide a stable IP address and DNS name for Pods because Pod IP addresses are temporary.

---

## Q6. What is Ingress?

Ingress routes external HTTP/HTTPS traffic to Kubernetes Services using domains or URL paths.

---

## Q7. What is ConfigMap?

ConfigMap stores non-sensitive configuration such as environment variables and application settings.

---

## Q8. What is Secret?

Secret securely stores sensitive data such as passwords, API keys, and tokens.

---

## Q9. What is Persistent Volume?

Persistent Volume is the actual storage resource available in the Kubernetes Cluster.

---

## Q10. What is Persistent Volume Claim?

PVC is a request made by an application to use Persistent Storage.

---
