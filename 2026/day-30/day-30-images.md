# Day 30 – Docker Images, Layers & Container Lifecycle

# Task 1 – Docker Images

# Pull Images from Docker Hub
`docker pull nginx`  
`docker pull ubuntu`  
`docker pull alpine`

---

# List All Images
`docker images`

Observe:
- REPOSITORY
- TAG
- IMAGE ID
- SIZE

---

# Compare Ubuntu vs Alpine

`ubuntu` → ~70MB+  
`alpine` → ~5MB  

Reason:
Alpine is a minimal Linux distribution.
Ubuntu includes many packages and utilities.

---

# Inspect an Image
`docker inspect nginx`

You can see:
- Image ID
- Created date
- OS/Architecture
- Layers
- Environment variables
- Default command (CMD)

---

# Remove an Image
`docker rmi alpine`

If in use:
`docker rmi -f alpine`

---

# Task 2 – Image Layers

# View Image History
`docker image history nginx`

You will see:
- Multiple layers
- Some layers with size (MB)
- Some layers showing 0B

---

# What Are Layers?

Each Docker image is built in layers.
Every instruction in a Dockerfile creates a new layer.

Why Docker Uses Layers:
- Faster builds (layer caching)
- Reusability between images
- Efficient storage
- Faster downloads (only changed layers pulled)

0B layers usually represent metadata changes (like CMD, ENV).

---

# Task 3 – Container Lifecycle

# Create Container (Not Started)
`docker create --name my-container nginx`

Check:
`docker ps -a`

State → Created

---

# Start Container
`docker start my-container`

State → Running

---

# Pause Container
`docker pause my-container`

Check state:
`docker ps`

Status → Paused

---

# Unpause Container
`docker unpause my-container`

---

# Stop Container
`docker stop my-container`

State → Exited

---

# Restart Container
`docker restart my-container`

---

# Kill Container (Force Stop)
`docker kill my-container`

---

# Remove Container
`docker rm my-container`

---

# Task 4 – Working with Running Containers

# Run Nginx in Detached Mode
`docker run -d -p 8080:80 --name web nginx`

---

# View Logs
`docker logs web`

---

# View Real-Time Logs
`docker logs -f web`

---

# Exec Into Container
`docker exec -it web bash`

Explore:
`ls /`  
`cat /etc/nginx/nginx.conf`

Exit:
`exit`

---

# Run Single Command Inside Container
`docker exec web ls /usr/share/nginx/html`

---

# Inspect Container
`docker inspect web`

Look for:
- IP Address
- Port Bindings
- Mounts
- Network mode

Quick IP check:
`docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' web`

---

# Task 5 – Cleanup

# Stop All Running Containers
`docker stop $(docker ps -q)`

---

# Remove All Stopped Containers
`docker rm $(docker ps -a -q)`

---

# Remove Unused Images, Networks, Volumes
`docker system prune`

Force without confirmation:
`docker system prune -f`

---

# Check Docker Disk Usage
`docker system df`

Shows:
- Images space
- Containers space
- Volumes space
