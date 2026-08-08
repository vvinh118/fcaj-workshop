---
title: "Prerequisites"
date: 2026-08-07
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---

#### Required Accounts & Tools

Before starting the hands-on deployment of the **Cloud Finance Platform**, ensure you have prepared the following prerequisites:

1. **AWS Account:** Prepare an AWS account (preferably with full Administrator access or necessary IAM management permissions enabled).
2. **Local Workstation Tools:**
   * **Docker & Docker Compose:** Used for building and testing microservice containers locally.
   * **AWS CLI:** Installed and configured with your credentials (`aws configure`) linked to your AWS account.
   * **Code Editor:** VS Code or any preferred IDE.
3. **Project Source Code:** Have the complete codebase ready, including:
   * Frontend interface (ReactJS / Vite).
   * 9 Backend microservices built with FastAPI (*Gateway, Auth, Finance, AI Agent, Notification API, Notification Worker, Planning, Recurring, and OCR*).

#### IAM Permissions
Ensure your AWS account holds sufficient permissions to interact with the core services utilized throughout this workshop: **Amazon VPC, Amazon RDS, Amazon ElastiCache, Amazon ECS (Fargate), Amazon ECR, Amazon S3, Amazon CloudFront, AWS Secrets Manager, and CloudWatch**.