---
title: "Proposal"
date: 2026-08-07
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# AI-Powered Personal Finance Platform
## A Cloud-Native Microservices Solution for Intelligent Expense Management on AWS

### 1. Executive Summary
The project develops an intelligent personal finance management platform leveraging Artificial Intelligence (AI/NLP) and Optical Character Recognition (OCR). The system is structured following a Microservices architecture and deployed entirely on AWS cloud infrastructure. By utilizing AWS Serverless and Managed Services, the project delivers an automated solution for expense tracking characterized by high availability, flexible scalability, and absolute security.

### 2. Problem Statement
#### What’s the Problem?
Personal finance management typically demands patience due to manual transaction data entry. Users easily fall into skipping receipts, experiencing fatigue after short-term usage, and lacking a holistic overview of cash flow. Traditional applications lack active data analytics capabilities and fail to understand natural user conversational language.

#### The Solution
Build a web platform integrated with an AI assistant enabling users to input data via natural Vietnamese conversational language (e.g., "Sáng nay ăn phở hết 45k") or upload receipt images for automated data extraction via OCR. The backend is partitioned into independent services (Auth, Finance, AI Agent, Planning, etc.) to handle specialized workloads and deliver real-time alerts and financial insights.

#### Benefits and Return on Investment
* Significantly reduces manual data entry time through automation via OCR (Tesseract) and NLP (Gemini API).
* Delivers a seamless, intelligent, and highly personalized financial management experience.
* Microservices architecture on AWS isolates risks, facilitates effortless scaling under surging user traffic, and optimizes operational costs via a pay-as-you-go model.

### 3. Solution Architecture
The architecture overview of the system is detailed below:

![Cloud Finance Platform Architecture](architecture.png)

### AWS Services Used
- **Amazon CloudFront & S3**: High-speed static content distribution (SPA Origin) and storage for receipt/export images.
- **Application Load Balancer (ALB)**: Positioned in public subnets to route internet traffic into internal containers.
- **Amazon ECS (AWS Fargate)**: Serverless compute environment running 9 microservices (Gateway, Auth, Finance, AI Agent, Notification API, Notification Worker, Planning, Recurring, OCR).
- **Amazon RDS PostgreSQL**: Relational database management implementing the Database-per-service pattern (isolated logical databases like auth_db, finance_db, ai_db...).
- **Amazon ElastiCache for Redis**: Acts as a cache and message queue to asynchronously route messages (consumed by the Notification Worker).
- **AWS Secrets Manager**: Securely manages and injects sensitive configurations (credentials, Gemini API key) into containers.
- **Amazon CloudWatch & SES**: Centralized log monitoring, metrics tracking, and transactional email/OTP dispatch for users.

### Component Design & Data Flow
- **User Request**: Requests from the frontend traverse Amazon CloudFront (protected by AWS WAF) to the Application Load Balancer.
- **API Gateway Routing**: ALB routes requests to the Gateway Service on ECS Fargate. Here, the Gateway performs authorization and utilizes AWS Cloud Map (Service Connect) to invoke internal business REST APIs.
- **Asynchronous Workflow**: Upon triggering events (e.g., dispatching notifications), the Notification API pushes a message into Amazon ElastiCache (Redis). The Notification Worker consumes the queue asynchronously to process via Amazon SES.
- **External Integrations**: The AI Agent Service communicates directly with the Google Gemini API for advanced NLP and data extraction.

### 4. Technical Implementation
**Networking & Security**
Designed with an isolated VPC containing Public Subnets (for ALB and NAT Gateway) and Private Subnets (for ECS, RDS, and Redis). All computational tasks and data are completely shielded from direct public internet access. Outbound requests to external endpoints (such as Gemini API) strictly traverse the NAT Gateway. AWS Secrets Manager safeguards API keys without embedding static credentials into source code or task definitions.

**Containerization & CI/CD Pipeline**
Backend FastAPI/Python APIs are containerized using Docker and optimized for lightweight image size (v3). Automated CI/CD workflows are established via GitHub Actions, authenticating through OIDC to automatically build and push Docker images to Amazon ECR, followed by seamless ECS Service deployment updates without downtime.

### 5. Timeline & Milestones
- **Weeks 1-3 (Cloud Infrastructure)**: Finalized architectural diagrams, configured AWS VPC, Security Groups, initialized Amazon RDS (PostgreSQL) and Amazon ElastiCache (Redis).
- **Weeks 4-5 (Container & Compute)**: Optimized Dockerfiles for 9 microservices. Built and pushed v3 images to Amazon ECR. Launched the stack on Amazon ECS Fargate and configured ALB.
- **Week 6 (Edge & CI/CD)**: Deployed the ReactJS frontend to Amazon S3, configured CloudFront and OAC. Successfully established automated CI/CD pipelines via GitHub Actions (OIDC).
- **Weeks 7-8 (Testing & Workshop)**: Integrated Amazon CloudWatch for log tracking. Conducted internal workshops, ran cloud-based demo testings for AI/OCR features, and completed final reporting.

### 6. Budget Estimation
The project is deployed using an optimized architecture tailored for a cost-effective demo environment:
- **Amazon VPC & Compute**: Utilizes a Single-AZ NAT Gateway and single-task execution (Desired count = 1) per ECS Fargate service to minimize continuous running costs.
- **Database & Cache**: Amazon RDS PostgreSQL and Amazon ElastiCache (Redis) are configured under demo modes (Single-AZ, Replica = 0).
- **Cost Monitoring**: Enabled AWS Budgets to trigger automated alerts upon hitting 50%, 80%, and 100% threshold targets of the monthly projected budget.

### 7. Risk Assessment
#### Identified Risks
- Exposure of sensitive configuration secrets (Database Password, JWT Secret, Gemini API Key).
- External LLM API (Gemini) downtime disrupting natural language input features.

#### Mitigation Strategies
- **Configuration Security**: Strictly adhere to storing secrets via AWS Secrets Manager. Prohibit committing physical `.env` files to git repositories.
- **Fallback AI/OCR**: Implement fallback mechanisms: if Gemini API errors out, the system automatically falls back to regex-based processing or local Tesseract OCR for bill extraction.
- **Rollback Strategy**: Retain stable previous container image versions (v2) on ECR to swiftly rollback ECS Task Definitions if version v3 encounters deployment anomalies.

### 8. Expected Outcomes
#### Technical Improvements
Successfully migrated a localized monolith application to an AWS-standard cloud-native architecture. Outstandingly implemented Event-Driven patterns (Message Queuing via Redis) and Database-per-service principles while fully automating the DevOps pipeline through GitHub Actions.
#### Long-term Value
The system is primed to handle heavy workloads while preserving stability. This serves as a robust foundation to evolve into a personalized Fintech ecosystem where AI transcends data entry to actively analyze and forecast user financial health.