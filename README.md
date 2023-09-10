# Spring Boot based Java web application
 
This is a simple Sprint Boot based Java application that can be built using Maven. Sprint Boot dependencies are handled using the pom.xml 
at the root directory of the repository.

Goal
Goal Of the project to deploy Sprint Boot based Java application on docker using CICD pipeline on jenkins.

Pre-Requisites
Sprint Boot based Java application Source Code. You can get it from this github repository Branch: docker-cicd
https://github.com/arifislam007/spring-bot-jenkins-k8s.git
2. Jenkins Environment

3. Docker Hub Account.

4. Docker Environment

Processes:
First Clone Repository from the github
Build with Maven
Build Docker Image and Push to Docker Hub
Remove previous docker container running on remote docker host and run docker container with updated image pulling from docker hub.
Steps:
Integrated Jenkins with Docker hub login and auto push
Integrated Jenkins to execute command on remote docker host. To execute command on remote host you need to install SSH Pipeline Steps plugin on your jenkins system.


