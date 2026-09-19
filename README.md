# React CI/CD Pipeline with Jenkins & Docker

A simple CI/CD project that demonstrates how to build and deploy a React application using **GitHub, Jenkins, Docker, and AWS EC2**.

## Architecture

Developer
   ↓
GitHub
   ↓
Jenkins
   ↓
Docker Build
   ↓
Docker Container
   ↓
AWS EC2
   ↓
React Application


## Technologies Used

* React
* Git & GitHub
* Jenkins
* Docker
* AWS EC2
* Linux
* JavaScript

## Project Structure

react-cicd-pipeline/
│
├── public/
├── src/
├── package.json
├── package-lock.json
├── Dockerfile
├── Jenkinsfile
├── azure-pipelines.yml
└── .gitignore

## CI/CD Flow

1. Developer makes changes to the React application.
2. Code is pushed to GitHub.
3. Jenkins pulls the latest source code.
4. Jenkins builds a Docker image.
5. A unique Docker image tag is created using the Jenkins build number.
6. Jenkins stops the previous application container.
7. Jenkins removes the old container.
8. Jenkins starts a new container.
9. The application becomes available through EC2.

## Docker Image

Docker images are created using:

docker build -t react:v${BUILD_NUMBER} .

For example:

react:v1
react:v2
react:v3

## Docker Container
The application runs using:
docker run -d  --name Reactapp -p 8081:3000 react:v${BUILD_NUMBER}

Port mapping:

EC2 Port 8081 → Container Port 3000

## Access Application

After a successful deployment:

http://<EC2-PUBLIC-IP>:8081

Make sure port **8081** is allowed in the EC2 Security Group.

## Jenkins Pipeline Stages

### 1. Code Pull

Jenkins pulls the React source code from GitHub.

### 2. Docker Image

Jenkins builds a new Docker image using the Dockerfile.

### 3. Docker Container

The existing container is stopped and removed, then the new version is deployed.

## Dockerfile

The Dockerfile:

* Uses Node.js
* Installs dependencies
* Builds the React application
* Installs `serve`
* Serves the production build on port 3000

## Jenkins

Jenkins is running on an AWS EC2 instance and has permission to execute Docker commands.

Jenkins also uses the built-in:

BUILD_NUMBER

variable to create unique Docker image tags.

## Security

Never commit the following to GitHub:

* Passwords
* API keys
* Access tokens
* SSH private keys
* AWS credentials
* Gmail App Passwords
* Jenkins secrets

Secrets should be stored using Jenkins Credentials or another secret-management solution.

## Future Improvements

Possible enhancements:

* GitHub Webhook
* Automatic Jenkins builds
* Docker Hub / Amazon ECR
* Jenkins Credentials
* SonarQube
* Docker image cleanup
* Nginx
* Kubernetes deployment
* AWS ECR + ECS/EKS
* Terraform infrastructure

## Author

**Kruthik Reddy**

DevOps Engineer | Azure | AWS | Docker | Kubernetes | Jenkins
