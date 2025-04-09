# 🚀 Assignment – Full Stack Deployment

This repository contains a full-stack CRUD application built with **Angular**, **Node.js**, **Express**, **MongoDB**, and deployed using **Docker**, **Docker Compose**, **Nginx**, and **GitHub Actions (CI/CD)**.

---

## Step-by-Step Setup & Deployment Instructions

### 1. Clone the Repository

```bash
git clone https://github.com/<your-username>/Discover-Dollar-Assignment.git
cd Discover-Dollar-Assignment
```
### 2. Docker Image Build & Push (via GitHub Actions)
On every push to the main branch, GitHub Actions:
- Builds Docker images for frontend, backend, and nginx
- Pushes them to Docker Hub
- SSHs into the EC2 instance
- Pulls updated images and restarts containers
- Deploys on EC2

### 3. CI/CD Configuration
GitHub Actions (.github/workflows/deployment.yml) automates the full pipeline:
🔨 Docker build
📦 Docker push
🚀 Remote deployment via SSH

Secrets used:
`DOCKER_USERNAME`, `DOCKER_PASSWORD`, `SERVER_IP`, `SERVER_USER`, `SSH_KEY`

### 4. Docker Image Build & Push Process

### 🔧 Frontend
```bash
docker build -t prajwalnav/frontend ./frontend
docker push prajwalnav/frontend
```
### 🔧 Backend
```bash
docker build -t prajwalnav/backend ./backend
docker push prajwalnav/backend
```
### 🔧 Nginx(Reverse Proxy)
```bash
docker build -t prajwalnav/nginx ./nginx
docker push prajwalnav/nginx
```
- Each service (frontend, backend, nginx) is containerized.
- Frontend: Angular app served using `http-server`
- Backend: Node.js with Express and Mongoose
- Nginx: Acts as reverse proxy to frontend (port 3000) and backend (port 8080)


### 5. Nginx Setup & Infrastructure Details
nginx.conf
```nginx
server {
    listen 80;

    location / {
        proxy_pass http://frontend:3000;
    }

    location /api/ {
        proxy_pass http://backend:8080;
    }
}
```

### 6. UI
Final Working UI has:
- 🌐 Accessible at: http://51.21.152.35/
- ✅ Angular frontend with full CRUD operations
- 🔗 Connected to Express backend and MongoDB
- 🔁 Reverse proxied through NGINX for clean routing



