3-Tier Application Stack using Docker Compose – Complete Notes

📌 Project Overview



This project demonstrates how to build and manage a 3-tier architecture using Docker Compose.



Architecture:



User → Web Application → Cache → Database



Stack Components:



Web App: Python Flask



Database: PostgreSQL



Cache: Redis



Orchestration: Docker Compose



✅ Task 1: Build Your Own App Stack

Objective



Create a docker-compose.yml file with:



A Web application (Flask)



A Database (Postgres)



A Cache (Redis)



A custom Dockerfile for the web app



🐳 Dockerfile for Web App

FROM python:3.11

WORKDIR /app

COPY . .

RUN pip install -r requirements.txt

CMD ["python", "app.py"]



Why use Dockerfile?



Custom build process



Control over dependencies



Reproducibility



Production-ready workflow



🧩 Basic docker-compose.yml



version: "3.9"



services:

  web:

    build: .

    ports:

      - "5000:5000"



  db:

    image: postgres:16



  cache:

    image: redis:latest



Key Learning:



Each service runs in its own container.



Services communicate using service names (db, cache).



Docker automatically creates a default network.



✅ Task 2: depends_on & Healthchecks

Problem



depends_on only ensures container startup order, NOT service readiness.



Database may start but still not be ready to accept connections.



Add Healthcheck to Database



db:

  image: postgres:16

  healthcheck:

    test: ["CMD-SHELL", "pg_isready -U user -d mydb"]

    interval: 5s

    timeout: 5s

    retries: 5

Make Web Wait for Healthy DB

web:

  depends_on:

    db:

      condition: service_healthy



Result:



Web waits until DB is fully ready.



No startup race condition.



Stable application boot.



✅ Task 3: Restart Policies

restart: always

restart: always



Restarts container if it crashes.



Restarts after Docker daemon restart.



Best for production databases.



restart: on-failure

restart: on-failure



Restarts only if exit code ≠ 0.



Does not restart if manually stopped.



When to Use Which?



restart: always → Databases, critical services

restart: on-failure → Jobs, background workers

restart: no → Debugging



✅ Task 4: Custom Dockerfiles in Compose



Instead of using pre-built images:



image: myapp



Use:



build: .

Rebuild After Code Change

docker compose up --build



Single command:



Rebuild image



Restart containers



✅ Task 5: Named Networks & Volumes

Custom Network

networks:

  app-network:



Attach services:



services:

  web:

    networks:

      - app-network



Why?



Isolation



Clean architecture



Better control



Named Volume for Database

volumes:

  db-data:



Attach to DB:



db:

  volumes:

    - db-data:/var/lib/postgresql/data



Why?



Data persists after container removal.



Critical for database durability.



Add Labels (Optional)

labels:

  project: app-stack

  tier: database



Used for:



Monitoring



Filtering



Organization



✅ Task 6: Scaling (Bonus)



Scale web service:



docker compose up --scale web=3

What Breaks?



Port mapping conflict:



5000:5000



Only one container can bind to host port 5000.



Why Simple Scaling Fails?



All replicas try to use same host port.



No load balancer.



No reverse proxy.



Docker Compose alone is not full orchestration.



Real-World Solution



Add Nginx reverse proxy.



Use Docker Swarm.



Use Kubernetes.



Remove direct port mapping.



Use internal networking + load balancing.



🧠 DevOps Learnings from This Project



You learned:



Multi-container architecture



Docker networking



Service discovery using service names



Healthchecks and startup sequencing



Restart policies



Data persistence using volumes



Scaling limitations



Production-aware thinking



Infrastructure as Code principles



🔥 Production Improvements (Next Level)



To make this production-ready:



Replace Flask dev server with Gunicorn



Add Nginx reverse proxy



Use environment variables



Implement logging strategy



Add monitoring (Prometheus/Grafana)



Add CI/CD pipeline



Deploy to cloud (AWS EC2 or ECS)



Convert to Kubernetes
