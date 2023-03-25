# Continuous Integration and Continuous Delivery of Vprofile Project

This is a DevOps project for [CI/CD](https://www.redhat.com/en/topics/devops/what-is-ci-cd) (_Continuous Integration and Continuous Delivery_) of a java-based vprofile project using Jenkins, Nexus, SonarQube, Docker, AWS Cloud Services and Slack. 

The pipeline created in the project makes use of multiple stages that involve: Cloning GitHub repository, testing code using maven, using code analysis tools like Checkstyle and SonarQube, building .var/.war artifact and storing in Nexus Repository or building Docker image and storing in Elastic Container Registry, hosting created image on Elastic Container Service, sending out success or failure notifications on specified Slack channels. 

The above pipeline is executed in the following three ways: 
- Whenever a user makes changes (eg. commit, push) to the repository. This is made possible by use of GitHub Webhooks.
- Remote execution using Jenkins API/Remote Trigger.
- Manual execution. 

[Link](https://github.com/Aranya7/vprofile-repo-for-devops-project) for vprofile app repository.

## Problem - Issues with Current Situation:

- In an Agile SDLC, there will be Frequent Code changes

- Manual Code Deployment is Time Consuming

- Involves Task Assignment / Ticketing / Approvals

- Dependency on Ops, Build and Release Teams

## Solution - Fix:

- Build, Test, Deploy and Test for Every Commit

- Automated Process

- Notify for Every Build Status

- Fix Code if Bugs or Errors found Instantly rather than waiting

## Benefits - CICD Pipeline:

- Short MTTR (Mean Time to Recovery)

- No Human Intervention

- Fault Isolation

- Agile

## Tools used in the Project:

- [**Jenkins**](https://www.jenkins.io/) - Continuous Integration and Continuous Delivery Server

- [**Git and GitHub**](https://github.com/) - Version Control System

- [**Maven**](https://maven.apache.org/) - Build Tool

- [**Checkstyle**](https://checkstyle.org/) - Code Analysis Tool

- [**Nexus Sonatype Repository**](https://www.sonatype.com/products/nexus-repository) - Artifact / Software Repository

- [**SonarQube**](https://www.sonarsource.com/products/sonarqube/) - Code Analysis Server

- [**Docker**](https://www.docker.com/) - Build Docker Images

- [**Amazon EC2**](https://aws.amazon.com/ec2/) - Compute Resource

- [**Amazon ECR**](https://aws.amazon.com/ecr/) - Elastic Container Registry

- [**Amazon ECS**](https://aws.amazon.com/ecs/) - Elastic Container Service

- [**AWS CLI**](https://aws.amazon.com/cli/) - AWS Command Line Interface

- [**Slack**](https://slack.com/) - Notifications

## Services Ports:
 - Jenkins Server - 8080

 - Nexus Server - 8081

 - SonarQube Server - 80
  (default port for SonarQube Server is 9000 , port 80 is used because a Nginx Server is configured to redirect the request to port 9000 )

## Jenkins Plugins used in the Project:

- [**Maven Integration**](https://plugins.jenkins.io/maven-plugin/)

- [**GitHub Integration**](https://plugins.jenkins.io/github-pullrequest/)

- [**Nexus Artifact Uploader**](https://plugins.jenkins.io/nexus-artifact-uploader/)

- [**SonarQube Scanner**](https://plugins.jenkins.io/sonar/)

- [**Build Timestamp**](https://plugins.jenkins.io/build-timestamp/)

- [**Docker Pipeline**](https://plugins.jenkins.io/docker-workflow/)

- [**CloudBees Docker Build and Publish**](https://plugins.jenkins.io/docker-build-publish/)

- [**Amazon ECR**](https://plugins.jenkins.io/amazon-ecr/)

- [**Pipeline: AWS Steps**](https://plugins.jenkins.io/pipeline-aws/)

- [**Slack Notification**](https://plugins.jenkins.io/slack/)

## Overall Architecture:
![Screenshot (1414)](https://user-images.githubusercontent.com/51438967/227660476-fdff73de-05e5-47cb-824d-d112c47abf3d.png)


## Usage (Flow of Execution) - Jenkins CICD Steps:

1. Login to AWS Account - [Link](https://aws.amazon.com/marketplace/management/signin) to Login to your AWS Account.

2. Create Key Pair

3. Create Security Groups

   a. Jenkins, Nexus and Sonarqube

4. Create EC2 Instances with Userdata

   a. Jenkins, Nexus and Sonarqube

5. Post Installation

   a. Jenkins Setup and Plugins

   b. Nexus Setup and Repository Setup

   c. SonarQube Login Test

6. Setup GitHub Webhook with Jenkins IP

7. Copy Docker Files from the Repository

8. Create Two Separate Jenkinsfile for staging and production in Source Code

9. AWS Steps

   a. IAM Setup

   b. ECR Repository Setup

10. Jenkins Steps

   a. Install Plugins

   - Docker Pipeline

   - CloudBees Docker Build and Publish

   - Amazon ECR

   - Pipeline: AWS Steps

11. Install Docker Engine and AWS CLI on Jenkins Server

12. Write Jenkinsfile for Building image and Publish it to ECR

13. ECS Setup

   a. Cluster Setup

   b. Task Definition Setup

   c. Service Setup

14. Code for Deploying Docker Image to ECS

15. Repeat the Steps for Production ECS Cluster

16. Promoting Docker Image for Production

17. Slack Notifications
