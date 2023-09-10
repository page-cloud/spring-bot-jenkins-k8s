# Deploying a Spring Boot Java Application with Jenkins CI/CD Pipeline

## Goal
The goal of this project is to deploy a Spring Boot-based Java application on Docker using a CI/CD pipeline in Jenkins.

## Pre-Requisites
Before you begin, ensure you have the following pre-requisites in place:
1. **Spring Boot Java Application Source Code**: You can obtain it from this GitHub repository by checking out the `docker-cicd` branch:
   [GitHub Repository](https://github.com/arifislam007/spring-bot-jenkins-k8s.git)

2. **Jenkins Environment**

3. **Docker Hub Account**

4. **Docker Environment**

## Processes
The deployment process involves several steps as follows:

1. **Clone the Repository from GitHub**: Clone the Spring Boot Java application source code from the provided GitHub repository.

2. **Build with Maven**: Use Maven to build the Java application.

3. **Build Docker Image and Push to Docker Hub**: Create a Docker image of the application and push it to Docker Hub.

4. **Remove Previous Docker Container**: Remove any existing Docker container running on the remote Docker host.

5. **Run Docker Container with Updated Image**: Start a new Docker container on the remote host using the updated image pulled from Docker Hub.

## Steps
Here are the detailed steps to deploy your Spring Boot Java application using Jenkins CI/CD:

### 1. Clone Repository from GitHub
Clone the Spring Boot Java application source code from the GitHub repository by checking out the `docker-cicd` branch:
```bash
git clone -b docker-cicd https://github.com/arifislam007/spring-bot-jenkins-k8s.git
```

### 2. Build with Maven
Navigate to the project directory and build the Java application using Maven:
```bash
cd spring-bot-jenkins-k8s
mvn clean install
```

### 3. Build Docker Image and Push to Docker Hub
Build a Docker image for the application and push it to Docker Hub. Ensure that you have Docker Hub credentials configured in your Jenkins environment:
```bash
docker build -t spring-java:${BUILD_NUMBER} .
docker login -u YOUR_DOCKERHUB_USERNAME -p YOUR_DOCKERHUB_PASSWORD
docker tag spring-java:${BUILD_NUMBER} YOUR_DOCKERHUB_USERNAME/spring-java:${BUILD_NUMBER}
docker push YOUR_DOCKERHUB_USERNAME/spring-java:${BUILD_NUMBER}
```

### 4. Remove Previous Docker Container
Remove any existing Docker container running on the remote Docker host. This step will require SSH access to the remote host:
```bash
ssh dockeradmin@YOUR_REMOTE_HOST 'docker rm -f java-spring'
```

### 5. Run Docker Container with Updated Image
Start a new Docker container on the remote host using the updated image pulled from Docker Hub. Make sure to replace placeholders with your specific values:
```bash
ssh dockeradmin@YOUR_REMOTE_HOST 'docker run -itd --name java-spring -p 7054:8080 YOUR_DOCKERHUB_USERNAME/spring-java:${BUILD_NUMBER}'
```

### Additional Jenkins Configuration
- To enable Jenkins to interact with Docker Hub for automated image pushes, integrate Jenkins with Docker Hub login and auto push.

- For executing commands on a remote Docker host, you need to install the "SSH Pipeline Steps" plugin on your Jenkins system.

With these steps and configurations, you can automate the deployment of your Spring Boot Java application on Docker using Jenkins CI/CD pipeline.

Feel free to adapt and customize this guide to your specific project and environment. If you have any questions or need further assistance, please don't hesitate to ask.
