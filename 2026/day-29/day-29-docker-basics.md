# Day 29 – Docker Basics & Hands-On

# Task 1 – What is Docker?

# What is a Container?
A container is a lightweight, portable environment that packages:
- Application code
- Dependencies
- Libraries
- Runtime

Containers ensure:
"Works on my machine" → Works everywhere ✅

---

# Why Do We Need Containers?
- Consistent environments
- Faster deployment
- Lightweight compared to VMs
- Easy scaling
- Isolation between applications

---

# Containers vs Virtual Machines

## Virtual Machine (VM)
- Includes full OS
- Heavy
- Slower boot time
- Uses hypervisor

## Container
- Shares host OS kernel
- Lightweight
- Starts in seconds
- Uses container runtime (Docker)

---

# Docker Architecture

Docker uses client-server architecture:

User → Docker Client → Docker Daemon → Containers

---

# Components

## Docker Client
Command line tool (`docker` command)

## Docker Daemon (dockerd)
Background service that:
- Builds images
- Runs containers
- Manages networks & volumes

## Docker Image
Blueprint/template for container

## Docker Container
Running instance of an image

## Docker Registry
Stores images (example: Docker Hub)

---

# Architecture Flow (Simple Diagram)

User  
↓  
Docker CLI  
↓  
Docker Daemon  
↓  
Images → Containers  
↑  
Docker Hub (Registry)

---

# Task 2 – Install Docker

# Verify Installation
`docker --version`

---

# Run Hello World
`docker run hello-world`

## What Happened?
- Docker checked locally for image
- Pulled image from Docker Hub
- Created container
- Executed it
- Displayed message
- Container stopped

---

# Task 3 – Run Real Containers

# Run Nginx
`docker run -d -p 8080:80 --name my-nginx nginx`

Access in browser:
`http://localhost:8080`

---

# Run Ubuntu (Interactive Mode)
`docker run -it ubuntu bash`

Now you're inside a mini Linux system.

Exit:
`exit`

---

# List Running Containers
`docker ps`

---

# List All Containers (Including Stopped)
`docker ps -a`

---

# Stop Container
`docker stop my-nginx`

---

# Remove Container
`docker rm my-nginx`

---

# Task 4 – Explore

# Detached Mode (-d)
`docker run -d nginx`

Runs container in background.

Difference:
- No terminal attached
- Runs silently

---

# Custom Name
`docker run -d --name web-server nginx`

---

# Port Mapping
`docker run -d -p 3000:80 nginx`

Format:
`-p host_port:container_port`

---

# Check Logs
`docker logs web-server`

---

# Execute Command Inside Running Container
`docker exec -it web-server bash`

---

# Important Commands Summary

`docker run` → Create container  
`docker ps` → List running  
`docker stop` → Stop container  
`docker rm` → Remove container  
`-it` → Interactive  
`-d` → Detached  
`-p` → Port mapping  
`--name` → Custom name  
`docker logs` → View logs  
`docker exec` → Run command inside container  
