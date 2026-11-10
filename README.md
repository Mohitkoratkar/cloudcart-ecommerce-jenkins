# CloudCart – Containerized E-Commerce Website & CI/CD Pipeline

A DevOps project demonstrating the deployment of a containerized e-commerce website using **Docker, Jenkins, Docker Hub, Nginx, and AWS EC2**. The project implements an automated CI/CD pipeline to build, publish, and deploy a Dockerized web application.

## 🚀 Project Overview

CloudCart is a sample e-commerce website designed to demonstrate real-world DevOps practices.

The project uses Jenkins to automate the application deployment workflow. Whenever changes are pushed to the GitHub repository, Jenkins checks out the latest source code, builds a Docker image, pushes the image to Docker Hub, and deploys the container on an AWS EC2 instance.

The application is served using Nginx inside a Docker container.

## 🛠️ Technologies Used

- **AWS EC2** – Cloud infrastructure for hosting the application
- **Jenkins** – CI/CD pipeline automation
- **Docker** – Application containerization
- **Docker Hub** – Docker image repository
- **Nginx** – Web server for serving the application
- **Git & GitHub** – Source code management
- **Bash Scripting** – Deployment automation
- **HTML, CSS, JavaScript** – Frontend development
- **Docker Compose** – Container management

## 🏗️ Project Architecture

The deployment workflow follows these steps:

1. Developer pushes application code to GitHub.
2. Jenkins detects the code changes or starts the configured pipeline.
3. Jenkins checks out the latest source code.
4. Docker builds a new application image.
5. The image is pushed to Docker Hub.
6. Jenkins connects to the AWS EC2 deployment server.
7. The previous application container is replaced with the latest container.
8. Nginx serves the e-commerce website to users.

## 📂 Project Structure

```text
cloudcart-ecommerce-jenkins/
│
├── index.html
├── css/
│   └── style.css
│
├── js/
│   └── script.js
│
├── nginx/
│   └── default.conf
│
├── Dockerfile
├── docker-compose.yml
├── Jenkinsfile
├── .dockerignore
└── README.md
```

## ⚙️ Prerequisites

Make sure the following tools are installed and configured:

- Git
- Docker
- Jenkins
- Docker Hub account
- AWS EC2 instance
- SSH access to the EC2 instance

## 💻 Run Locally

**1. Clone the repository**

```bash
git clone https://github.com/Mohitkoratkar/cloudcart-ecommerce-jenkins.git
cd cloudcart-ecommerce-jenkins
```

**2. Build the Docker image**

```bash
docker build -t cloudcart .
```

**3. Run the container**

```bash
docker run -d -p 8080:80 --name cloudcart-app cloudcart
```

**4. Access the application**

Open your browser:

```text
http://localhost:8080
```

## 🐳 Docker Commands

Check running containers:

```bash
docker ps
```

View Docker images:

```bash
docker images
```

View container logs:

```bash
docker logs cloudcart-app
```

Stop the container:

```bash
docker stop cloudcart-app
```

Remove the container:

```bash
docker rm cloudcart-app
```

## 🔄 Jenkins CI/CD Pipeline

The project uses a `Jenkinsfile` to automate the deployment process.

### Pipeline Stages

| Stage | Description |
|---|---|
| Checkout | Pulls the latest source code from GitHub |
| Build | Builds the Docker image |
| Login | Authenticates with Docker Hub |
| Push | Publishes the Docker image to Docker Hub |
| Deploy | Deploys the latest container on AWS EC2 |

### Jenkins Configuration

1. Install the required Jenkins plugins, including Git and Pipeline.
2. Configure Docker Hub credentials in Jenkins.
3. Configure SSH access to the AWS EC2 deployment server.
4. Create a Jenkins Pipeline job.
5. Connect the job to the GitHub repository.
6. Select `Jenkinsfile` as the pipeline script.
7. Run the pipeline and verify each stage.

Store credentials securely in Jenkins Credentials. Do not hardcode passwords, Docker Hub tokens, or private SSH keys in the Jenkinsfile.

## ☁️ AWS EC2 Deployment

The application is deployed on an AWS EC2 instance.

**Basic deployment steps:**

1. Launch an EC2 instance.
2. Install and configure Docker.
3. Configure Jenkins to access the instance securely through SSH.
4. Pull the latest Docker image from Docker Hub.
5. Stop and remove the previous container.
6. Run the updated application container.
7. Configure the EC2 security group to allow HTTP traffic on port 80 or the port used by your deployment.

Access the application using:

```text
http://YOUR_EC2_PUBLIC_IP
```

Replace `YOUR_EC2_PUBLIC_IP` with your EC2 instance's public IP address or DNS name.

## 🎯 Key Learning Outcomes

- Understanding CI/CD pipeline implementation using Jenkins.
- Building and managing Docker images.
- Publishing images to Docker Hub.
- Automating application deployment using Jenkins.
- Deploying containerized applications on AWS EC2.
- Configuring Nginx as a web server.
- Managing application containers.
- Working with GitHub for source code management.
- Understanding end-to-end DevOps workflows.

## 🔮 Future Improvements

- Integrate GitHub webhooks for automatic pipeline triggering.
- Add automated testing before deployment.
- Implement HTTPS using SSL certificates.
- Add monitoring and logging
