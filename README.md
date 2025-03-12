# Cloud Engineering Technical Assessment


---

## Setup and Deployment Instructions

### Prerequisites
1. **AWS Account**: Ensure you have an AWS account with the necessary permissions.
2. **Terraform**: Install Terraform on your local machine.
3. **Docker**: Install Docker to build and test the container locally.
4. **GitHub Repository**: Fork or clone this repository.

### Step 1: Clone the Repository
git clone https://github.com/AlexOOP/DockerizeFlask.git
cd DockerizeFlask

### Step 2: Set Up AWS Credentials
1. Create an IAM user with the following permissions:
   - AmazonEC2FullAccess
   - AmazonECS_FullAccess
   - AmazonECRFullAccess

### 2. Store the AWS credentials as GitHub secrets:
   - AWS_ACCESS_KEY_ID
   - AWS_SECRET_ACCESS_KEY
   - AWS_REGION (e.g., eu-west-2)
   - ECR_REPOSITORY (e.g., lockwood-flask-app)
   - ECS_CLUSTER (e.g., lockwood-cluster)
   - ECS_SERVICE (e.g., lockwood-service)

### Step 3: Build and Test the Docker Image Locally
1. Build the Docker image:
   docker build -t flask-app ./app
2. Run the container locally:
   docker run -d -p 5000:5000 --name flask-container flask-app
3. Test the application:
   curl http://localhost:5000

### Step 4: Deploy Infrastructure with Terraform
1. Navigate to the "terraform/" directory:
   cd terraform
2. Initialize Terraform:
   terraform init
3. Plan and apply the Terraform configuration:
   terraform plan
   terraform apply

### Step 5: Set Up CI/CD Pipeline

1. Push changes to the "main" branch of your GitHub repository.
2. The GitHub Actions workflow will:
   - Build and push the Docker image to Amazon ECR.
   - Deploy the updated image to ECS.

####################################################

## Potential Improvements for a Production Environment

1. Add an Application Load Balancer (ALB):
    Distribute traffic across multiple ECS tasks.
    Enable HTTPS using an ACM certificate.

2. Enable Auto Scaling:
    Configure ECS service auto-scaling based on CPU/memory usage or request count.

3. Use Secrets Management:
    Store sensitive data (e.g., database credentials) in AWS Secrets Manager or Parameter Store.

4. Enable CloudWatch Logs:
    Stream container logs to CloudWatch for centralized logging and monitoring.

5. mplement Blue/Green Deployments:
    Use AWS CodeDeploy to minimize downtime during deployments.

6. Optimize Docker Image:
    Regularly update base images to include security patches.






























## Overview
This assessment evaluates your proficiency with Docker, Terraform, AWS (specifically ECS), and CI/CD pipelines. You'll be containerizing a simple Python application and deploying it to AWS ECS using Terraform. If you are not familiar with any of the technologies, feel free to complete as much as you can.

## Time Expectation
This assessment should take approximately 3-4 hours to complete.

## Requirements

### Part 1: Containerization
- Containerize the provided Python Flask application
- Create an optimized Dockerfile that follows security best practices
- Ensure the container properly runs the application on port 5000

### Part 2: Infrastructure as Code
- Create Terraform configurations to deploy the application to AWS ECS
- Set up the following AWS resources:
  - VPC with public and private subnets
  - ECS Cluster (Fargate launch type)
  - ECS Task Definition and Service for the containerized application
  - All necessary security groups, IAM roles, etc.
- Feel free to use any ready-made open-source terraform modules available

### Part 3: CI/CD Implementation
- Create a CI/CD pipeline configuration using GitHub Actions
- The pipeline should:
  - Build and tag the Docker image
  - Push the image to Amazon ECR
  - Deploy the updated image to ECS

### Part 4: Documentation
- Provide a README.md with:
  - Setup and deployment instructions
  - Potential improvements for a production environment
- Optionally include a simple architecture diagram (can be created with any tool)

## Deliverables
Please provide:
1. All source code in a GitHub repository (public or private with access shared)
2. Complete Terraform configurations
3. CI/CD pipeline configuration files
4. Documentation and architecture diagram (if you have any)
5. Any additional scripts or configurations you created

## Evaluation Criteria
Your submission will be evaluated based on:
- Docker best practices (security, optimization, multi-stage builds)
- Terraform organization, structure, and best practices
- AWS resource configuration and security
- Code quality and documentation
- CI/CD pipeline effectiveness

## Optional Extensions
If you have additional time and would like to demonstrate more of your skills, consider implementing these optional features:
- Adding an Application Load Balancer to distribute traffic to your service
- Configuring CloudWatch Logs for container logging

## Files Included in This Package
1. `app/` - Directory containing the Python Flask application
   - `app.py` - The main application file
   - `requirements.txt` - Python dependencies
2. `README.md` - This file with instructions

Good luck!