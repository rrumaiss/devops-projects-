# Project 1 — Static Website → GitHub → Docker → AWS EC2

## Overview

A simple static website deployed on AWS EC2 using Docker and Nginx.

## Technologies

- HTML
- CSS
- Git
- GitHub
- Docker
- Nginx
- AWS EC2

## Architecture

```text
Website → GitHub → AWS EC2 → Docker → Nginx → Website
```

---

## Step 1 — Create Website

Create the website using HTML and CSS.

```text
index.html
style.css
images/
```

---

## Step 2 — Create Dockerfile

Create a `Dockerfile` to run the website using Nginx.

```dockerfile
FROM nginx:alpine

COPY index.html /usr/share/nginx/html/index.html
COPY style.css /usr/share/nginx/html/style.css

EXPOSE 80
```

---

## Step 3 — Git

Initialize Git and save the project.

```bash
git init
git add .
git commit -m "Initial project"
```

---

## Step 4 — Push to GitHub

Connect the local project to GitHub and push the code.

```bash
git remote add origin https://github.com/rrumaiss/devops-projects-.git
git branch -M main
git push -u origin main
```

---

## Step 5 — Create AWS EC2

Create an EC2 instance using:

```text
Amazon Linux 2023
```

Allow:

```text
SSH  → 22
HTTP → 80
```

---

## Step 6 — Install Docker

Install Docker on EC2.

```bash
sudo dnf install -y docker
sudo systemctl start docker
```

Check:

```bash
docker --version
```

---

## Step 7 — Clone GitHub Repository

Download the project to EC2.

```bash
git clone https://github.com/rrumaiss/devops-projects-.git
```

Move into the project directory.

---

## Step 8 — Build Docker Image

Create the Docker image from the Dockerfile.

```bash
docker build -t devops-static-website:v1 .
```

---

## Step 9 — Run Container

Start the website inside a Docker container.

```bash
docker run -d --name devops-website -p 80:80 devops-static-website:v1
```

---

## Step 10 — Check Website

Check the container:

```bash
docker ps
```

Test:

```bash
curl http://localhost
```

Open the EC2 public IP in a browser:

```text
http://3.129.6.194
```

---

## Result

```text
GitHub
   ↓
AWS EC2
   ↓
Docker
   ↓
Nginx
   ↓
Static Website
```

**Project 1 — Completed ✅**
