Docker Image Optimization – Short Notes

✅ Task 1: Large Image Problem

Goal



Create simple app (Go / Node / Java)



Build using single-stage Dockerfile



Check image size



Single Stage Example

FROM node:18

WORKDIR /app

COPY . .

RUN npm install

CMD ["node", "app.js"]



Build:



docker build -t single-app .

docker images

Problem



Full runtime included



Build tools included



Dev dependencies included



Large OS base



Final image is very large



✅ Task 2: Multi-Stage Build

Goal



Separate build & runtime



Use minimal base image



Reduce image size



Multi-Stage Example

# Builder

FROM node:18 AS builder

WORKDIR /app

COPY . .

RUN npm install



# Runtime

FROM node:18-alpine

WORKDIR /app

COPY --from=builder /app .

CMD ["node", "app.js"]



Build:



docker build -t multi-app .

docker images

Why Smaller?



Build tools not included



Only final artifacts copied



Minimal OS (alpine)



Fewer layers



Result:

Single-stage → Large

Multi-stage → Much smaller



✅ Task 3: Push to Docker Hub



Login:



docker login



Tag:



docker tag multi-app username/app:v1



Push:



docker push username/app:v1



Verify:



docker pull username/app:v1

✅ Task 4: Docker Hub & Tags



Tags example:



v1



v2



latest



Pull specific version:



docker pull username/app:v1



Pull latest:



docker pull username/app:latest



⚠ Do NOT rely only on latest in production.



✅ Task 5: Image Best Practices

1️⃣ Use Minimal Base



node:18 → Large

node:18-alpine → Smaller



2️⃣ Don’t Run as Root

RUN adduser -D appuser

USER appuser



Improves security.



3️⃣ Combine RUN Commands



Bad:



RUN apt update

RUN apt install curl



Good:



RUN apt update && apt install -y curl



Reduces layers.



4️⃣ Use Specific Tags



Bad:



FROM node:latest



Good:



FROM node:18.19-alpine



Ensures stable builds.



🧠 Key Learnings



Multi-stage reduces image size



Smaller images = faster deployment



Always version your images



Use minimal base images



Avoid running as root



Optimize layers



Never depend on latest in production



🎯 DevOps Conclusion



Bad Image → Large, insecure, slow

Good Image → Small, secure, optimized



Multi-stage builds are production standard.



