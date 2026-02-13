# 🚀 Jenkins Docker Dev Stage Prod Implementation

## 📌 Project Overview

This project demonstrates a complete CI/CD pipeline using **Jenkins and Docker** with environment-based deployments (Dev → Stage → Production).

A static website built using HTML and CSS is containerized using Docker and deployed automatically to different AWS EC2 servers based on Git branches.

This project simulates a real-world DevOps workflow where code moves across multiple environments before reaching production.

---

## 🏗️ Architecture Flow

Developer pushes code to GitHub  
        ↓  
Jenkins pipeline triggers automatically  
        ↓  
Docker image builds  
        ↓  
Application deploys to target environment (Dev / Stage / Prod)

### 🌿 Branch-Based Deployment Strategy

- `dev` branch  → Deploys to Dev Server  
- `stage` branch → Deploys to Stage Server  
- `main` branch → Deploys to Production Server  

---

## 🛠️ Technologies Used

- Jenkins (Declarative Pipeline)
- Docker
- Nginx (nginx:alpine)
- AWS EC2
- Git & GitHub
- Linux
- SSH Automation

---

## 🐳 Docker Implementation

### 🔹 Dockerfile Configuration

- Base Image: `nginx:alpine`
- Working Directory: `/usr/share/nginx/html`
- Copies website files into container
- Exposes Port 80

### 🔹 Build Image

docker build -t myapp:<branch_name> .


Each branch creates a uniquely tagged Docker image.

---

## ⚙️ Jenkins Pipeline Logic

The Jenkins pipeline:

✔ Uses declarative pipeline syntax
✔ Defines environment variables for Dev, Stage, and Prod servers
✔ Detects Git branch automatically
✔ Deploys to correct EC2 instance
✔ Removes old container before deploying new one

### 🔹 Deployment Steps Automated by Jenkins

1. SSH into target server
2. Clone latest repository
3. Build Docker image
4. Remove existing container
5. Run updated container

This ensures zero manual deployment and consistent releases.

---

## 🔐 Environment Variables Example

DEV_SERVER = "Dev EC2 Public IP"
STAGE_SERVER = "Stage EC2 Public IP"
PROD_SERVER = "Prod EC2 Public IP"
APP_NAME = "myapp"


Deployment decision is made based on:

if (env.BRANCH_NAME == 'dev')
if (env.BRANCH_NAME == 'stage')
if (env.BRANCH_NAME == 'main')


---

## 🧠 DevOps Concepts Demonstrated

- CI/CD Pipeline Automation
- Environment Separation
- Branch-Based Deployment
- Docker Container Lifecycle Management
- SSH-Based Automated Deployment
- Infrastructure-Level Automation
- Zero Manual Production Deployment

---

## ▶️ Run Locally

### 1️⃣ Clone Repository

git clone https://github.com/Shubham-3177/Jenkins-Docker-Dev-Stage-Prod-Implementation.git

cd Jenkins-Docker-Dev-Stage-Prod-Implementation



### 2️⃣ Build Docker Image

docker build -t myapp .


### 3️⃣ Run Container

docker run -d -p 8080:80 myapp


### 4️⃣ Access Application

Open in browser:

http://localhost:8080


---

## 🚀 Future Improvements

- Push Docker image to Docker Hub
- Add automated testing stage
- Implement rollback strategy
- Add monitoring using Prometheus & Grafana
- Use Terraform or Ansible for infrastructure provisioning

---

## 👨‍💻 Author

**Shubham S Kadatare**
Aspiring DevOps Engineer

GitHub: https://github.com/Shubham-3177

---

⭐ If you found this project useful, feel free to star the repository!



