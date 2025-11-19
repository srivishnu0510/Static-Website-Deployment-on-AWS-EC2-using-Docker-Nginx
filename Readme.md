⚡ Static Website Deployment on AWS EC2 using Docker & Nginx

This project demonstrates how to deploy a static website (HTML/CSS/JS) using
AWS EC2 + Docker + Nginx.
The website files are packaged into a Docker image and served by an Nginx container on EC2.


🚀 Features

Lightweight Nginx web server

Dockerized static site

Deployment on AWS EC2 (Amazon Linux 2)

Simple and fast setup

Beginner friendly

🛠️ Technologies Used

HTML

AWS EC2

Docker

Nginx

Linux / SSH

SCP File Transfer


⚙️ EC2 Setup Steps
1️⃣ Launch an EC2 Instance

AMI: Amazon Linux 2

Instance type: t2.micro / t3.micro

Security group:

SSH (22) → your IP

HTTP (80) → anywhere

2️⃣ Install Docker

SSH into EC2:

sudo yum update -y
sudo amazon-linux-extras install docker -y
sudo systemctl enable --now docker
sudo usermod -aG docker ec2-user
logout


Reconnect SSH.

📤 Upload Website Files to EC2

From your local system (Windows example):

scp -i "path/to/your-key.pem" -r . ec2-user@YOUR_PUBLIC_IP:/home/ec2-user/site

🏗️ Build & Run Docker Container on EC2

Inside EC2:

cd site
docker build -t mysite .
docker run -d --name mysite -p 80:80 --restart unless-stopped mysite

🌐 Visit the Website

Open in browser:

http://YOUR_PUBLIC_IP

🔁 Update Website

After editing files locally, re-upload:

scp -i "path/to/key.pem" -r . ec2-user@YOUR_PUBLIC_IP:/home/ec2-user/site


Rebuild & restart:

cd site
docker build -t mysite .
docker stop mysite
docker rm mysite
docker run -d --name mysite -p 80:80 --restart unless-stopped mysite



Add to Dockerfile:

COPY nginx.conf /etc/nginx/conf.d/default.conf

🔐 Security Best Practices

Restrict SSH access to your IP

Never push .pem files to GitHub

Enable --restart unless-stopped for auto-start

Use separate IAM roles if accessing AWS services



🎉 Project Completed!

Your static website is now fully deployable using EC2 + Docker + Nginx.
