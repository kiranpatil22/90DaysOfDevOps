flask-app-stack – Large Image & Multi-Stage Notes

✅ Task 1: The Problem with Large Images

🎯 Goal



Build flask-app-stack using single-stage Dockerfile



Check image size



Compare later



🐳 Single-Stage Dockerfile

FROM python:3.11

WORKDIR /app

COPY . .

RUN pip install -r requirements.txt

CMD ["python", "app.py"]



Build:



docker build -t flask-app-stack:single .

docker images



Example size:



flask-app-stack   single   ~1GB

❗ Why Is It Large?



Full Python image



Build dependencies included



pip cache included



OS tools included



All layers kept



Single-stage keeps everything.



✅ Task 2: Multi-Stage Build

🎯 Goal



Separate build & runtime



Use minimal base image



Reduce size



🐳 Multi-Stage Dockerfile

# Stage 1 - Builder

FROM python:3.11 AS builder

WORKDIR /app

COPY requirements.txt .

RUN pip install --user -r requirements.txt

COPY . .



# Stage 2 - Runtime

FROM python:3.11-alpine

WORKDIR /app

COPY --from=builder /root/.local /root/.local

COPY --from=builder /app /app

ENV PATH=/root/.local/bin:$PATH

CMD ["python", "app.py"]



Build:



docker build -t flask-app-stack:multi .

docker images



Example:



flask-app-stack   single   ~1GB

flask-app-stack   multi    ~200MB

🧠 Why Multi-Stage Is Smaller?



Build tools removed



Only required files copied



Alpine is lightweight



No unnecessary layers



Reduced attack surface



Multi-stage removes everything not needed at runtime.



✅ Task 3: Push to Docker Hub



Login:



docker login



Tag:



docker tag flask-app-stack:multi yourusername/flask-app-stack:v1



Push:



docker push yourusername/flask-app-stack:v1



Verify:



docker pull yourusername/flask-app-stack:v1

✅ Task 4: Docker Hub & Tags



Repository shows:



v1



latest (if pushed)



Pull specific version:



docker pull yourusername/flask-app-stack:v1



Pull latest:



docker pull yourusername/flask-app-stack:latest



⚠ Production Best Practice:

Use version tags (v1, v2) — do not rely only on latest.



✅ Task 5: Image Best Practices

1️⃣ Use Minimal Base Image



python:3.11 → Large

python:3.11-alpine → Smaller



2️⃣ Do Not Run as Root



Add:



RUN adduser -D appuser

USER appuser



Benefits:



Better security



Production standard



3️⃣ Combine RUN Commands



Bad:



RUN apt update

RUN apt install curl



Good:



RUN apt update && apt install -y curl



Reduces layers → smaller image.



4️⃣ Use Specific Tags



Bad:



FROM python:latest



Good:



FROM python:3.11.8-alpine



Ensures stable & predictable builds.



📊 Size Comparison Example

Version	Size

Single Stage	~1GB

Multi-Stage	~200MB

Optimized	~150MB

🧠 Key Learnings



Multi-stage drastically reduces image size



Smaller image = faster pull & deploy



Always version images



Avoid root user



Optimize layers



Avoid using latest in production



🎯 DevOps Summary



Large Image → Slow, insecure, inefficient

Optimized Image → Small, secure, production-ready



Multi-stage builds are mandatory for professional DevOps workflows.

