# Day 32 – Docker Volumes & Networking

# Task 1 – The Problem (Data Persistence)

# Run MySQL Container (Without Volume)
`docker run -d --name mysql-test -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=testdb mysql`

---

# Enter Container
`docker exec -it mysql-test mysql -uroot -p`

Inside MySQL:
CREATE TABLE users (id INT, name VARCHAR(50));
INSERT INTO users VALUES (1, 'Kiran');
SELECT * FROM users;

Exit.

---

# Stop & Remove Container
`docker stop mysql-test`
`docker rm mysql-test`

---

# Run New Container
`docker run -d --name mysql-test -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=testdb mysql`

Check data again.

Result:
❌ Data is gone.

---

# Why?
Containers are ephemeral.
When container is removed → its writable layer is deleted.

---

# Task 2 – Named Volumes

# Create Named Volume
`docker volume create my-db-volume`

---

# Run MySQL with Volume
`docker run -d --name mysql-vol -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=testdb -v my-db-volume:/var/lib/mysql mysql`

---

# Add Data Again
(Repeat table + insert)

---

# Stop & Remove Container
`docker stop mysql-vol`
`docker rm mysql-vol`

---

# Run New Container with Same Volume
`docker run -d --name mysql-vol2 \
-e MYSQL_ROOT_PASSWORD=root \
-e MYSQL_DATABASE=testdb \
-v my-db-volume:/var/lib/mysql \
mysql`

Result:
✅ Data is still there.

---

# Verify Volumes
`docker volume ls`
`docker volume inspect my-db-volume`

---

# Task 3 – Bind Mounts

# Create Folder on Host
`mkdir my-website`
Create index.html inside it.

---

# Run Nginx with Bind Mount
`docker run -d -p 8080:80 \
-v $(pwd)/my-website:/usr/share/nginx/html \
--name nginx-bind \
nginx`

Access:
http://localhost:8080

---

# Edit index.html on Host
Refresh browser → changes reflect immediately ✅

---

# Named Volume vs Bind Mount

Named Volume:
- Managed by Docker
- Stored in Docker directory
- Good for databases

Bind Mount:
- Directly maps host folder
- Good for development
- Live file sync

---

# Task 4 – Docker Networking Basics

# List Networks
`docker network ls`

---

# Inspect Default Bridge
`docker network inspect bridge`

---

# Run Two Containers on Default Bridge
`docker run -dit --name c1 alpine`
`docker run -dit --name c2 alpine`

---

# Try Ping by Name
Inside c1:
`docker exec -it c1 sh`
`ping c2`

Result:
❌ Name resolution usually fails.

---

# Ping by IP
Find IP:
`docker inspect c2`

Ping that IP:
`ping <ip-address>`

Result:
✅ Works

---

# Task 5 – Custom Networks

# Create Custom Network
`docker network create my-app-net`

---

# Run Containers on Custom Network
`docker run -dit --name app1 --network my-app-net alpine`
`docker run -dit --name app2 --network my-app-net alpine`

---

# Ping by Name
Inside app1:
`ping app2`

Result:
✅ Works

---

# Why Custom Network Allows Name-Based Communication?

Custom bridge networks use built-in DNS.
Docker automatically resolves container names.

Default bridge does NOT provide automatic DNS resolution.

---

# Task 6 – Put It Together

# Create Network
`docker network create project-net`

---

# Run Database with Volume
`docker volume create project-db`

`docker run -d --name mydb \
--network project-net \
-e MYSQL_ROOT_PASSWORD=root \
-v project-db:/var/lib/mysql \
mysql`

---

# Run App Container on Same Network
`docker run -dit --name myapp --network project-net alpine`

---

# Verify Connectivity

Inside myapp:
`docker exec -it myapp sh`
`ping mydb`

Result:
✅ Container can reach DB by name

---

# Key Concepts Summary

Containers → Ephemeral  
Volumes → Persistent storage  
Bind Mounts → Host-based development  
Default Bridge → No automatic DNS  
Custom Network → Built-in DNS & service discovery  
