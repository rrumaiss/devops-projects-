# Project 1 — Static Website → GitHub → Docker → AWS EC2

## 📌 Project Overview

This is Project 1 of my DevOps learning journey.

The goal of this project is to build a simple static website and deploy it on an AWS EC2 instance using Docker and Nginx.

### Complete workflow

```text
Developer
    ↓
VS Code
    ↓
Git
    ↓
GitHub
    ↓
AWS EC2
    ↓
Docker
    ↓
Nginx
    ↓
Static Website
    ↓
Internet


1. Project Structure
Project 1/
│
├── Dockerfile
├── index.html
├── style.css
├── Readme.md
└── images/

Files
- index.html → Website structure
- style.css → Website styling
- images/ → Website images
- Dockerfile → Instructions for creating the Docker image
- Readme.md → Project documentation
2. Create the Website
The website is made using basic HTML and CSS.
index.html contains the website content.
style.css contains the styling.
The HTML connects to the CSS:
<link rel="stylesheet" href="style.css">

3. Dockerfile
The website is served using Nginx.
FROM nginx:alpine

COPY index.html /usr/share/nginx/html/index.html
COPY style.css /usr/share/nginx/html/style.css

EXPOSE 80

Understanding the Dockerfile
FROM
FROM nginx:alpine

This uses the official lightweight Nginx image.
Nginx will act as our web server.
COPY
COPY index.html /usr/share/nginx/html/index.html

Copies our HTML file into the directory where Nginx serves websites.
COPY style.css /usr/share/nginx/html/style.css

Copies our CSS file into the same Nginx web directory.
EXPOSE
EXPOSE 80

Documents that the application uses HTTP port 80.
4. Git — Store the Project
Git is used for version control.
Check Git:
git --version

Configure Git:
git config --global user.name "rrumaiss"
git config --global user.email "rumaismv@example.com"

Check repository status:
git status

Add files:
git add .

Commit:
git commit -m "Add Docker configuration"

5. GitHub
The GitHub repository is:
https://github.com/rrumaiss/devops-projects-.git

Configure the remote:
git remote add origin https://github.com/rrumaiss/devops-projects-.git

Check the remote:
git remote -v

Expected:
origin  https://github.com/rrumaiss/devops-projects-.git (fetch)
origin  https://github.com/rrumaiss/devops-projects-.git (push)

Push the project:
git branch -M main
git push -u origin main

Basic Git workflow
Edit files
    ↓
git add .
    ↓
git commit
    ↓
git push
    ↓
GitHub

6. AWS EC2
AWS EC2 is used as the server where the website will run.
Operating system:
Amazon Linux 2023

Check:
cat /etc/os-release

7. Install Git on EC2
Install Git:
sudo dnf install git -y

Check:
git --version

Output:
git version 2.50.1

8. Install Docker on EC2
Update packages:
sudo dnf update -y

Install Docker:
sudo dnf install -y docker

Start Docker:
sudo systemctl start docker

Enable Docker after reboot:
sudo systemctl enable docker

Allow ec2-user to use Docker:
sudo usermod -aG docker ec2-user

Reconnect to EC2 after running the above command.
Check Docker:
docker --version

Output:
Docker version 25.0.14, build 0bab007

9. Clone GitHub Repository on EC2
Instead of manually creating the files on EC2, download the project from GitHub.
cd ~

Clone:
git clone https://github.com/rrumaiss/devops-projects-.git

Enter the repository:
cd devops-projects-

Go to Project 1:
cd "1. Project 1 — Static Website → GitHub"

10. Verify the Files
Run:
find . -maxdepth 4 -type f

Output:
./Dockerfile
./Readme.md
./index.html
./style.css

This confirms that the project was successfully downloaded from GitHub to EC2.
11. Build the Docker Image
Run this from the Project 1 directory:
docker build -t devops-static-website:v1 .

What happens?
Dockerfile
    ↓
Docker reads instructions
    ↓
Downloads nginx:alpine
    ↓
Copies index.html
    ↓
Copies style.css
    ↓
Creates Docker Image

The image name is:
devops-static-website:v1

Check images:
docker images

12. Run the Docker Container
Start the container:
docker run -d --name devops-website -p 80:80 devops-static-website:v1

Important part
-p 80:80

means:
EC2 Host Port 80
       ↓
Docker Container Port 80

So traffic arriving at EC2 port 80 is forwarded to the Nginx container's port 80.
13. Check the Container
Run:
docker ps

You should see something similar to:
CONTAINER ID   IMAGE                       PORTS
xxxxxxxxxxxx   devops-static-website:v1   0.0.0.0:80->80/tcp

The important part is:
0.0.0.0:80->80/tcp

This means:
Host :80 → Container :80

14. Test the Website Inside EC2
Run:
curl http://localhost

If the website HTML appears, the application is working.
The request path is:
curl
 ↓
EC2 port 80
 ↓
Docker container
 ↓
Nginx
 ↓
index.html

15. AWS Security Group
The EC2 Security Group controls incoming network traffic.
For the website, allow HTTP:
Type:     HTTP
Protocol: TCP
Port:     80
Source:   0.0.0.0/0

This allows users from the Internet to access the website.
For SSH:
Type:     SSH
Protocol: TCP
Port:     22
Source:   Your IP

SSH should preferably be restricted to your own IP.
16. EC2 Public IP
EC2 public IP:
3.129.6.194

The website is accessed through:
http://3.129.6.194