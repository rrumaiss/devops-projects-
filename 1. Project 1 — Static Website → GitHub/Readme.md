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
Website
   ↓
GitHub
   ↓
AWS EC2
   ↓
Docker
   ↓
Nginx
   ↓
Website
```

## Project Structure

```text
Project 1/
├── Dockerfile
├── index.html
├── style.css
├── README.md
└── images/
```

## Dockerfile

```dockerfile
FROM nginx:alpine

COPY index.html /usr/share/nginx/html/index.html
COPY style.css /usr/share/nginx/html/style.css

EXPOSE 80
```

## Docker Commands

```bash
docker build -t devops-static-website:v1 .
docker run -d --name devops-website -p 80:80 devops-static-website:v1
docker ps
```

## AWS EC2

The Docker container runs on an Amazon Linux 2023 EC2 instance.

HTTP port:

```text
80
```

Website:

```text
http://3.129.6.194
```
