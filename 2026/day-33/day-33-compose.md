# Day 33 – Docker Compose Basics

# Task 1 – Check Docker Compose

# Verify Compose is Installed
`docker compose version`

If installed → shows version info.

If not → install Docker Desktop or Docker Compose plugin.

---

# Task 2 – Your First Compose File

# Create Project Folder
`mkdir compose-basics`
`cd compose-basics`

---

# Create docker-compose.yml

version: "3.9"

services:
  nginx:
    image: nginx
    ports:
      - "8080:80"

---

# Start Services
`docker compose up`

Access:
http://localhost:8080

---

# Start in Detached Mode
`docker compose up -d`

---

# Stop & Remove
`docker compose down`

---

# Task 3 – Two-Container Setup (WordPress + MySQL)

# docker-compose.yml

version: "3.9"

services:
  db:
    image: mysql:5.7
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wpuser
      MYSQL_PASSWORD: wppass
    volumes:
      - db-data:/var/lib/mysql

  wordpress:
    image: wordpress:latest
    ports:
      - "8081:80"
    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: wpuser
      WORDPRESS_DB_PASSWORD: wppass
      WORDPRESS_DB_NAME: wordpress
    depends_on:
      - db

volumes:
  db-data:

---

# Start Setup
`docker compose up -d`

Access:
http://localhost:8081

Complete WordPress installation.

---

# Test Persistence
`docker compose down`
`docker compose up -d`

Result:
✅ WordPress data still exists (because of named volume)

---

# Why It Works

- Compose automatically creates a network
- Service names act as DNS names
- WordPress connects to MySQL using `db`

---

# Task 4 – Compose Commands

# Start Detached
`docker compose up -d`

---

# View Running Services
`docker compose ps`

---

# View All Logs
`docker compose logs -f`

---

# View Specific Service Logs
`docker compose logs -f db`

---

# Stop Without Removing
`docker compose stop`

---

# Remove Containers & Network
`docker compose down`

---

# Rebuild Images After Change
`docker compose up -d --build`

---

# Task 5 – Environment Variables

# Add Directly in compose File

environment:
  MYSQL_ROOT_PASSWORD: root

---

# Use .env File

Create `.env` file:

MYSQL_ROOT_PASSWORD=root

MYSQL_DATABASE=wordpress

---

# Reference in docker-compose.yml

environment:

  MYSQL_ROOT_PASSWORD: ${MYSQL_ROOT_PASSWORD}
  
  MYSQL_DATABASE: ${MYSQL_DATABASE}

---

# Verify Variables

`docker compose config`

Shows resolved environment values.

---

# Key Concepts Summary

Compose:
- Manages multi-container apps
- Creates default network automatically
- Service names act as DNS
- Supports volumes & environment variables
- Simplifies complex setups
