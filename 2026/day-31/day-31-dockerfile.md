# Day 31 – Dockerfile & Image Building Challenge

# Task 1 – Your First Dockerfile

# Step 1 – Create Project Folder
`mkdir my-first-image`  
`cd my-first-image`

---

# Step 2 – Create Dockerfile

Create a file named `Dockerfile`:

FROM ubuntu  
RUN apt update && apt install -y curl  
CMD ["echo", "Hello from my custom image!"]

---

# Step 3 – Build Image
`docker build -t my-ubuntu:v1 .`

Note:
`.` → current directory (build context)

---

# Step 4 – Run Container
`docker run my-ubuntu:v1`

Verify:
Message prints:
Hello from my custom image!

---

# Task 2 – Dockerfile Instructions

# Example Dockerfile

FROM ubuntu  

RUN apt update && apt install -y curl  

WORKDIR /app  

COPY . .  

EXPOSE 8080  

CMD ["echo", "Dockerfile demo running"]

---

# Build Image
`docker build -t demo-image:v1 .`

# Run Container
`docker run demo-image:v1`

---

# What Each Instruction Does

FROM → Sets base image  
RUN → Executes command during build  
WORKDIR → Sets working directory inside image  
COPY → Copies files from host to image  
EXPOSE → Documents container port  
CMD → Default command when container runs  

---

# Task 3 – CMD vs ENTRYPOINT

# Example 1 – CMD

Dockerfile:

FROM ubuntu  
CMD ["echo", "hello"]

Build:
`docker build -t cmd-test .`

Run:
`docker run cmd-test`

Output:
hello

Run with custom command:
`docker run cmd-test echo bye`

Output:
bye  

CMD gets overridden.

---

# Example 2 – ENTRYPOINT

Dockerfile:

FROM ubuntu  
ENTRYPOINT ["echo"]

Build:
`docker build -t entry-test .`

Run:
`docker run entry-test hello`

Output:
hello

Run with more arguments:
`docker run entry-test hello world`

Output:
hello world  

ENTRYPOINT does NOT get replaced.
Arguments are appended.

---

# CMD vs ENTRYPOINT Summary

Use CMD:
- For default command
- When users may override it

Use ENTRYPOINT:
- When container must always run a specific executable
- For utility-style containers

---

# Task 4 – Build Simple Web App Image

# Step 1 – Create index.html

Example:

<html>  
  <h1>Hello from My Docker Website</h1>  
</html>

---

# Step 2 – Create Dockerfile

FROM nginx:alpine  
COPY index.html /usr/share/nginx/html/  
EXPOSE 80  

---

# Step 3 – Build Image
`docker build -t my-website:v1 .`

---

# Step 4 – Run Container
`docker run -d -p 8080:80 --name my-site my-website:v1`

Access:
http://localhost:8080

---

# Task 5 – .dockerignore

# Create .dockerignore File

node_modules  
.git  
*.md  
.env  

---

# Build Image Again
`docker build -t optimized-image:v1 .`

Verify:
Ignored files are NOT included in build context.

Why Important?
- Smaller image size
- Faster builds
- Better security

---

# Task 6 – Build Optimization

# Build Image
`docker build -t cache-test:v1 .`

---

# Change One Line and Rebuild
`docker build -t cache-test:v2 .`

Notice:
Docker reuses cached layers if unchanged.

---

# Why Layer Order Matters

Docker builds top → bottom.

If early layers change:
→ All layers after must rebuild.

Best Practice:
- Put rarely changing instructions first
- Put frequently changing code last

Example Good Order:

FROM ubuntu  
RUN apt install dependencies  
COPY app code (changes often)  

This improves build speed.

---

# Important Commands Summary

`docker build -t name:tag .`  
`docker run image`  
`docker run -d -p host:container`  
`docker images`  
`docker rmi image`  
